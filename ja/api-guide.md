<!-- machine_translated: true -->

<!-- pre-align:aligned sig=876ecae2be90 -->

<a id="foundry.api.guide"></a>
## Machine Learning > NHN Cloud Foundry > API ガイド { #foundry.api.guide }

NHN Cloud Foundry が提供する API について説明します。

| API | 説明 |
| --- | --- |
| Ingest API | 作成済みのデータソースへのデータ取り込み。スナップショットファイルのアップロードを提供 |
| レコメンデーション照会 API | 作成したレコメンデーションシステムアプリへの推薦結果のリクエスト |
| レコメンデーションイベント API | 推薦結果に対するユーザーの反応イベントの収集 |

<a id="auth.common"></a>
## 認証および共通事項 { #auth.common }

<a id="auth.common.preparation"></a>
### 事前準備 { #auth.common.preparation }

API を使用するには、**Appkey** と**認証トークン**が必要です。

- Appkey は、NHN Cloud コンソールの **[Machine Learning > NHN Cloud Foundry]** ページ上部の **[URL & Appkey]** メニューで確認できます。
- API は **gateway-public** エンドポイントを使用します。
- 認証トークン（`X-NHN-Authorization` ヘッダーの Bearer トークン）の発行方法については、[User Access Key トークン](https://docs.nhncloud.com/ko/nhncloud/ko/public-api/user-access-key-token/) ガイドを参照してください。

<a id="auth.common.request"></a>
### リクエスト共通事項 { #auth.common.request }

必須ヘッダー:

```plaintext
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {ACCESS_TOKEN}
Content-Type: application/json
```

Base URL:

```plaintext
https://{gateway-public-host}/api/v1.0
```

<a id="auth.common.response"></a>
### レスポンス共通事項 { #auth.common.response }

すべての API レスポンスは `header` と `body` で構成されます。

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {}
}
```

| フィールド | タイプ | 説明 |
| --- | --- | --- |
| header.isSuccessful | Boolean | リクエストの成否 |
| header.resultCode | Integer | 結果コード。成功時は 0、失敗時はエラーコード |
| header.resultMessage | String | 結果メッセージ。成功時は SUCCESS、失敗時はエラー詳細 |
| body | Object/Array | API ごとのレスポンスデータ |

リクエストが拒否されても、HTTP ステータスコードは `200` で返される場合があります。成功の可否は HTTP ステータスコードではなく、`header.isSuccessful` と `header.resultCode` で判定します。認証トークンがない場合または有効期限が切れている場合、HTTP `401` を返します。

<a id="ingest.api"></a>
## Ingest API { #ingest.api }

Ingest API は、コンソールで作成済みのデータソースにデータを取り込むための API です。
アップロードしたファイルでデータソースのデータをすべて置き換えるスナップショットアップロード方式を提供します。

!!! danger "注意"
    データソースを新規に作成する API は提供していません。Ingest API を使用するには、コンソールであらかじめデータソースを作成する必要があります。また、FILE タイプのデータソースのみ使用できます。

<a id="ingest.snapshot"></a>
### スナップショットアップロード（ファイルアップロード） { #ingest.snapshot }

アップロードしたファイルの内容でデータソースのデータを**すべて置き換え**ます。アップロードは 3 段階で進みます。

!!! danger "注意"
    スナップショットアップロードは、データソースにすでに取り込まれているデータをすべて置き換えます。既存のデータは復元できません。

アップロード制限:

- 最大アップロードサイズ: **10GB**
- `100MB` 以下 → **単一アップロード（SINGLE）**
- `100MB` 超 → **マルチパートアップロード（MULTIPART）**
- `formPost` フィールドの値は、レスポンスに含まれる値を**そのまま**リクエストに使用します。

<a id="ingest.snapshot.init"></a>
#### 1. アップロード初期化（init） { #ingest.snapshot.init }

| メソッド | URI |
| --- | --- |
| POST | /api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/init |

大容量ファイルをストレージに直接アップロードするための署名済み一時 URL を発行します。ファイルサイズに応じて、単一 URL（SINGLE）またはマルチパート URL（MULTIPART）を返します。

curl の例:

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/init" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "fileName": "data.csv",
    "fileSize": 52428800,
    "contentType": "text/csv"
  }'
```

| フィールド | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| fileName | String | O | ファイル名。使用可能文字: 英字、数字、ピリオド（.）、アンダースコア（_）、ハイフン（-） |
| fileSize | Long | O | ファイルサイズ（bytes）。最小 1、最大 10GB |
| contentType | String | X | Content-Type（デフォルト値: application/octet-stream） |

レスポンス例（SINGLE）:

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "uploadType": "SINGLE",
    "uploadUrl": "{upload-url}",
    "uploadId": null,
    "partSize": null,
    "parts": null,
    "expiresAt": "2025-01-20T11:00:00Z",
    "formPost": {
      "objectPrefix": "{appKey}/{dataSourceId}/snapshot/{jobId}/",
      "signature": "{SIGNATURE}",
      "expires": 1737370800,
      "maxFileSize": 10737418240,
      "maxFileCount": 1
    }
  }
}
```

レスポンス例（MULTIPART）:

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "uploadType": "MULTIPART",
    "uploadUrl": null,
    "uploadId": "{appKey}/{dataSourceId}/snapshot/{jobId}/data.csv_segments/",
    "partSize": 104857600,
    "parts": [
      {
        "partNumber": 1,
        "uploadUrl": "{part-upload-url}?signature={SIG}&expires={TS}&max_file_size=104857600&max_file_count=1",
        "headUrl": "{part-head-url}?temp_url_sig={SIG}&temp_url_expires={TS}"
      }
    ],
    "expiresAt": "2025-01-20T11:00:00Z",
    "formPost": {
      "objectPrefix": "{appKey}/{dataSourceId}/snapshot/{jobId}/",
      "signature": "{SIGNATURE}",
      "expires": 1737370800,
      "maxFileSize": 104857600,
      "maxFileCount": 1
    }
  }
}
```

!!! tip "ヒント"
    MULTIPART レスポンスにも `formPost` が含まれます。ただし、マルチパートアップロードでは `parts[].uploadUrl` のクエリパラメータ（`signature`/`expires`/`max_file_size`/`max_file_count`）でパートを送信するため、`formPost` は参考用であり、パートアップロード自体には使用しません。

| フィールド | 説明 |
| --- | --- |
| body.jobId | ジョブ ID。以降の complete/ステータス確認リクエストに使用 |
| body.uploadType | アップロードタイプ。SINGLE（100MB 以下）または MULTIPART（100MB 超） |
| body.uploadUrl | アップロード URL（単一アップロード時） |
| body.uploadId | マルチパートアップロード ID（マルチパートアップロード時） |
| body.partSize | パートサイズ（bytes、マルチパートアップロード時） |
| body.parts[].partNumber | パート番号（1 から開始） |
| body.parts[].uploadUrl | パートアップロード URL |
| body.parts[].headUrl | ETag 取得用 URL（アップロード完了後に HEAD リクエスト） |
| body.expiresAt | URL の有効期限 |
| body.formPost.objectPrefix | オブジェクト prefix（ファイル名の前に付くパス） |
| body.formPost.signature | HMAC-SHA1 署名 |
| body.formPost.expires | 有効期限（UNIX タイムスタンプ） |
| body.formPost.maxFileSize | 最大ファイルサイズ（bytes） |
| body.formPost.maxFileCount | 最大ファイル数 |

<a id="ingest.snapshot.upload.single"></a>
#### 2-A. 単一ファイルアップロード（100MB 以下） { #ingest.snapshot.upload.single }

init レスポンスの `uploadUrl` に multipart/form-data POST を送信します。
このリクエストは Object Storage に直接送信するため、別途の認証は不要です（`signature` が認証の役割を担います）。

curl の例:

```bash
curl -X POST "{uploadUrl}" \
  -F "redirect=" \
  -F "max_file_size={formPost.maxFileSize}" \
  -F "max_file_count={formPost.maxFileCount}" \
  -F "expires={formPost.expires}" \
  -F "signature={formPost.signature}" \
  -F "file=@./data.csv;filename=data.csv"
```

!!! danger "注意"
    `file` フィールドは必ずフォームデータの**末尾**に追加する必要があります。成功時は HTTP `201 Created` レスポンスを受け取ります。

<a id="ingest.snapshot.upload.multipart"></a>
#### 2-B. 大容量ファイルアップロード（100MB 超、MULTIPART） { #ingest.snapshot.upload.multipart }

レスポンスの `parts[]` 配列を受け取り、パートごとにアップロードします。
各パートは **(1) アップロード → (2) HEAD で ETag 取得 → (3) `partETags[]` に `partNumber` 昇順で収集** の順で処理します。

1. ファイルを `partSize`（デフォルト 100MB）単位で分割します。
2. パートごとに `parts[i].uploadUrl` のクエリパラメータ（`signature`、`expires`、`max_file_size`、`max_file_count`）を解析し、multipart/form-data で送信します（フィールド名 `file`、ファイル名は固定で `part`）。
3. アップロード成功後、`parts[i].headUrl` に `HEAD` リクエストを送信し、レスポンスヘッダーの `ETag` 値を収集します。
4. すべてのパートが完了したら、`partETags` 配列を `partNumber` 昇順で構成し、アップロード完了（complete）リクエストに含めて送信します。

パートアップロードの curl 例:

```bash
# 1) アップロード
curl -X POST "{parts[i].uploadUrl}" \
  -F "redirect=" \
  -F "max_file_size={max_file_size-from-query}" \
  -F "max_file_count={max_file_count-from-query}" \
  -F "expires={expires-from-query}" \
  -F "signature={signature-from-query}" \
  -F "file=@./part_i.bin;filename=part"

# 2) ETag の照会
curl -I "{parts[i].headUrl}" | grep -i '^etag:'
```

<a id="ingest.snapshot.complete"></a>
#### 3. アップロード完了（complete） { #ingest.snapshot.complete }

| メソッド | URI |
| --- | --- |
| POST | /api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/complete |

curl の例（単一アップロード）:

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/complete" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "fileName": "data.csv"
  }'
```

curl の例（マルチパートアップロード）:

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/complete" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "fileName": "data.csv",
    "uploadId": "{multipart-upload-id}",
    "partETags": ["etag-part1", "etag-part2", "etag-part3"]
  }'
```

| フィールド | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| jobId | String | O | ジョブ ID（init レスポンスの jobId） |
| fileName | String | O | ファイル名 |
| uploadId | String | X | マルチパートアップロード ID（マルチパートアップロード時のみ必要） |
| partETags | Array | X | パートごとの ETag リスト（マルチパートアップロード時のみ必要、partNumber 順） |

レスポンス例:

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
  }
}
```

| フィールド | 説明 |
| --- | --- |
| body.jobId | ジョブ ID。[ジョブステータス確認](#ingest.snapshot.job.status)に使用 |

<a id="ingest.snapshot.cancel"></a>
#### アップロードキャンセル { #ingest.snapshot.cancel }

| メソッド | URI |
| --- | --- |
| DELETE | /api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/{jobId} |

curl の例（単一アップロード）:

```bash
curl -X DELETE "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/{jobId}" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}"
```

curl の例（マルチパートアップロード）- クエリパラメータで `uploadId` を併せて渡します:

```bash
curl -X DELETE "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/{jobId}?uploadId={uploadId}" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}"
```

<a id="ingest.snapshot.job.status"></a>
#### ジョブステータス確認 { #ingest.snapshot.job.status }

| メソッド | URI |
| --- | --- |
| GET | /api/v1.0/data-sources/{dataSourceId}/ingest/jobs/{jobId} |

curl の例:

```bash
curl "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/jobs/{jobId}" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}"
```

レスポンス例:

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "dataSourceId": "ds-001",
    "jobType": "SNAPSHOT",
    "status": "COMPLETED",
    "obsFilePath": "s3a://{bucket}/{path}/file.csv",
    "statistics": {
      "totalRecords": 10000,
      "failedRecords": 5,
      "successfulRecords": 9995,
      "successRate": 0.9995
    },
    "errorMessage": null,
    "createdDatetime": "2025-01-20T10:00:00Z",
    "startedDatetime": "2025-01-20T10:01:00Z",
    "completedDatetime": "2025-01-20T10:05:00Z",
    "modifiedDatetime": "2025-01-20T10:05:00Z"
  }
}
```

| フィールド | 説明 |
| --- | --- |
| body.jobId | ジョブ ID |
| body.dataSourceId | 対象データソース ID |
| body.jobType | ジョブタイプ。SNAPSHOT（スナップショット取り込み）または EVENT（変更イベント） |
| body.status | ジョブステータス。下記のステータス値を参照 |
| body.obsFilePath | OBS ファイルパス |
| body.statistics.totalRecords | 総レコード数 |
| body.statistics.failedRecords | 失敗レコード数 |
| body.statistics.successfulRecords | 成功レコード数 |
| body.statistics.successRate | 成功率（0.0〜1.0） |
| body.errorMessage | エラーメッセージ（失敗時） |
| body.createdDatetime | ジョブ作成日時 |
| body.startedDatetime | ジョブ開始日時 |
| body.completedDatetime | ジョブ完了日時 |
| body.modifiedDatetime | 最終更新日時 |

ジョブステータス（`status`）は次の値を取ります。

| 値 | 説明 |
| --- | --- |
| UPLOADING | ファイルアップロード中 |
| QUEUED | アップロード完了、取り込み待ち |
| STAGED | 処理準備完了 |
| RUNNING | データ取り込み中 |
| COMPLETED | ジョブ正常完了 |
| FAILED | ジョブ失敗 |

<a id="metrics.ingest.api"></a>
### 指標収集 { #metrics.ingest.api }

タイプが Prometheus API であるデータソースに指標データを転送します。転送した指標は単変量異常検出アプリの入力として使用します。

| メソッド | URI |
| --- | --- |
| POST | /api/v1.0/data-sources/{dataSourceId}/ingest/metrics |

curl 例：

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/metrics" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "metrics": [
      {
        "timestamp": 1776149886528,
        "value": 4.99,
        "labels": [
          { "name": "__name__", "value": "cpu_usage" },
          { "name": "instance_id", "value": "instance-001" }
        ],
        "metadata": { "resourceType": "Instance" }
      }
    ]
  }'
```

| フィールド | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| metrics | Array | O | 指標リスト。空にすることはできず、1 回のリクエストあたり最大 5,000 件 |
| metrics[].timestamp | Long | O | メトリクスの時刻。ミリ秒単位の epoch |
| metrics[].value | Double | O | 測定値 |
| metrics[].labels | Array | O | ラベルリスト。ラベルの組み合わせが時系列を、グループラベルがグループを決定 |
| metrics[].labels[].name | String | O | ラベル名。英文字または _ で始まり、英文字、数字、_ のみを使用 |
| metrics[].labels[].value | String | O | ラベル値。コンマと等号は使用不可 |
| metrics[].metadata | Object | X | 付加情報。解釈せず、そのまま保存・転送。identityKey キーはシステムが使用するため使用不可 |

成功した場合は HTTP `202 Accepted` を返します。リクエストが却下された場合は HTTP `200` で `header.isSuccessful` が `false` で返されるため、`header` で成功の有無を判定します。

収集ルールは次のとおりです。

- 必須フィールドの不足、ラベル名・値のルール違反、1 回のリクエストで 5,000 件を超過、必須ヘッダの不足は、リクエスト全体が却下され、どの項目も保存されません。
- 1 つのリクエストに複数の時系列の指標を含めることができます。時系列はラベルの組み合わせで区分されるため、時系列ごとにリクエストを分ける必要はありません。
- 同じ時系列は 1 分に 1 回だけ送信します。より短い周期で収集する場合は、1 分平均に合算して送信します。同じ分に複数の値が到着した場合、最初に到着した値のみが分析に使用され、残りは破棄されます。
- `timestamp` はミリ秒単位の epoch です。秒単位で送信すると、誤った時刻として保存されます。
- データソースにグループラベルを指定した場合は、常にそのラベルを含めて転送します。ラベルが不足した場合は、意図したグループに属しません。
- `value` が NaN または Infinity の項目は保存されず、スキップされます。同じリクエストの残りの項目は正常に処理されます。
- `202` レスポンスは受信完了を意味します。保存は少し後で反映され、同じリクエストを再度送信した場合、同じデータが重複保存される可能性があります。
- 転送が遅延したデータは保存されますが、リアルタイム推論の対象から除外される可能性があります。

!!! tip "ヒント"
    取り込みは転送周期と無関係です。ただし、このデータソースを単変量異常検出アプリに接続した場合は、同じ時系列を 1 分に 1 つずつ途切れなく送信する必要があります。アプリが指標を 1 分単位で集約して判定するため、それより長い間隔で送信すると、空白の期間が生じ、精度モードで準備が終了しない可能性があります。

<a id="univariate.api"></a>
## 単変量異常検出 API { #univariate.api }

<a id="univariate.group.api"></a>
### グループの使用開始·停止·削除 { #univariate.group.api }

単変量異常検出アプリのグループの使用を開始、停止、削除します。3つのAPIのリクエスト形式は同じで、パスのみが異なります。

| メソッド | URI |
| --- | --- |
| POST | /api/v1.0/serving-pipelines/{servingPipelineId}/groups/enable |
| POST | /api/v1.0/serving-pipelines/{servingPipelineId}/groups/disable |
| POST | /api/v1.0/serving-pipelines/{servingPipelineId}/groups/delete |

`servingPipelineId` はコンソールアプリの詳細に表示されるアプリ ID です。

curl の例:

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/serving-pipelines/{servingPipelineId}/groups/enable" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "groupKey": [
      { "name": "region", "value": ["kr1", "jp1"] }
    ]
  }'
```

| フィールド | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| groupKey | Array | 条件付き | 対象グループを指定するラベルリスト。データソースにグループラベルを指定した場合にのみ使用 |
| groupKey[].name | String | O | グループラベル名。データソースに指定したグループラベルと名前が正確に一致する必要があります。 |
| groupKey[].value | Array | O | そのラベルの値のリスト。値1つがグループ1つに対応します。 |

成功すると、header.isSuccessful が true として返され、body は存在しません。

リクエスト規則は次のとおりです。

- データソースにグループラベルを指定していない場合、groupKey を送信しません。データソース全体が1つのグループであるため、そのグループが対象になります。groupKey を一緒に送信すると、リクエストが拒否されます。
- データソースにグループラベルを指定した場合、groupKey は必須であり、送信されたラベル名のセットがデータソースのグループラベルと正確に一致する必要があります。同じラベル名を2回送信すると、拒否されます。
- グループラベルが複数ある場合、値のリストを同じ順序でまとめてグループを作成します。たとえば、rule_id に ["a", "b"]、instance_id に ["q", "w"] を送信した場合、(a, q) と (b, w) の2つのグループが対象です。すべてのラベルの値の数が同じである必要があり、異なる場合は拒否されます。
- 値のリストが空の場合、拒否されます。同じグループが複数回指定されている場合、1回だけ処理されます。
- 登録されていないグループを停止または削除すると、エラーが返されます。

!!! tip "ヒント"
    指標が到着すると、グループは自動的に登録されて動作します。このAPIは特定のグループだけを選んで使用開始、停止、削除するときに使用され、コンソールにはこの操作はありません。登録されたグループと状態は、コンソールアプリの詳細の **グループ一覧** タブで確認します。

!!! danger "注意"
    グループを停止しても、検出結果の転送は停止しません。グループ一覧に表示される状態が無効に変わるだけです。
    削除したグループは状態履歴とともに消え、復旧することはできません。

<a id="recommendation.api"></a>
## レコメンデーション照会 API { #recommendation.api }

作成したレコメンデーションシステムアプリにレコメンデーション結果をリクエストします。ユーザーの履歴が十分な場合はモデルベース (Sequential)、不足している場合は属性ベース (Cold Start) で推論します。

<a id="recommendation.api.recommend"></a>
### レコメンデーションリクエスト { #recommendation.api.recommend }

| メソッド | URI |
| --- | --- |
| POST | /api/v1.0/recommendation-apps/{appId}/recommend |

curl 例:

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/recommendation-apps/{appId}/recommend" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "userId": "user_12345",
    "context": {
      "currentItemKey": "CONT0001",
      "recentlyViewed": ["CONT0010", "CONT0023"],
      "pageType": "course_detail",
      "sessionId": "session_abc123"
    },
    "options": {
      "maxRecommendations": 10
    }
  }'
```

| フィールド | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| userId | String | O | レコメンデーション対象のユーザーID。匿名ユーザーにレコメンデーションをリクエストする場合は、空の文字列 ("") を指定します。 |
| context.currentItemKey | String | X | 現在表示中のアイテムキー |
| context.recentlyViewed | Array | X | 最近閲覧したアイテムキーのリスト |
| context.availableItems | Array | X | レコメンデーション対象のアイテムキーのリスト。指定した場合、このリストに含まれるアイテムの中からのみレコメンデーションします。 |
| context.pageType | String | X | 現在のページタイプ (自由形式。例: home、item_detail) |
| context.sessionId | String | X | セッションID |
| userAttributes | Object | X | ユーザー属性情報 (Cold Start 推論に使用) |
| options.maxRecommendations | Integer | X | 最大レコメンデーション数 (1〜100)。100を超える値はエラーなく100に調整されます。未指定の場合は100が適用されます。レコメンデーション可能なアイテムがこの値より少ない場合は、実際のアイテム数のみ返します。 |
| options.mode | String | X | 推論方式を指定します。sequential (履歴ベース)、cold_start (属性ベース)、popular (人気ベース) のいずれか。未指定の場合はサーバーが自動で決定します。 |
| options.longtail | Boolean | X | 人気の低いアイテムも含めてレコメンデーションの多様性を向上させます。sequential の場合のみ適用されます。 |
| options.excludeItemKeys | Array | X | レコメンデーションから除外するアイテムキーのリスト。除外したアイテムは最大レコメンデーション数に含まれません。 |

!!! tip "ヒント"
    `userAttributes` スキーマは、今後の選好度誘導 (Preference Elicitation) の実装方向に応じて、収集方式やフィールドの種類が変更される可能性があります。

レスポンス例:

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "userId": "user_12345",
    "recommendations": [
      { "itemKey": "CONT0023", "score": 0.95, "position": 1 },
      { "itemKey": "CONT0045", "score": 0.89, "position": 2 }
    ],
    "metadata": {
      "modelVersion": "v1.2.0",
      "requestId": "req_xyz789",
      "inferenceType": "sequential",
      "abTestGroup": ""
    }
  }
}
```

| フィールド | 説明 |
| --- | --- |
| body.userId | リクエストしたユーザーID |
| body.recommendations[].itemKey | レコメンデーションアイテムキー |
| body.recommendations[].score | レコメンデーションスコア (0.0〜1.0) |
| body.recommendations[].position | レコメンデーション順位 |
| body.metadata.modelVersion | 使用されたモデルバージョン |
| body.metadata.requestId | リクエスト追跡ID。レコメンデーションイベントAPI送信時にこの値を使用します。 |
| body.metadata.inferenceType | 推論タイプ。sequential (履歴ベース)、cold_start (属性ベース)、popular (人気ベース) |
| body.metadata.abTestGroup | A/B テストグループ (現在は空の値を返します) |

<a id="recommendation.event.api"></a>
## 推薦イベント API { #recommendation.event.api }

推薦結果に対するユーザーの反応（クリックなど）のイベントを収集します。収集されたイベントデータを使用して、推薦の成功率を分析できます。

<a id="recommendation.event.api.send"></a>
### 推薦イベント送信 { #recommendation.event.api.send }

| メソッド | URI |
| --- | --- |
| POST | /api/v1.0/recommendation-apps/{appId}/events |

curl の例:

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/recommendation-apps/{appId}/events" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "eventType": "CLICK",
    "requestId": "req_xyz789",
    "itemKey": "CONT0023",
    "userId": "user_12345",
    "context": {
      "sessionId": "sess_abc",
      "placement": "home_main"
    }
  }'
```

`requestId`、`itemKey`、`userId` は、推薦照会 API のレスポンスで受け取った値をそのまま渡します。

| フィールド | 必須 | 説明 |
| --- | --- | --- |
| eventType | O | イベントの種類。自由に定義できます（例: CLICK、PURCHASE、IMPRESSION）。英字・数字・アンダースコア（_）のみ使用可能（^[A-Za-z0-9_]+$）、最大 64 文字。大文字小文字を区別せず大文字に正規化して保存されます。REQUEST、RESPONSE は予約語のため使用不可 |
| requestId | O | 推薦 API レスポンスの body.metadata.requestId の値（opaque string、最大 128 文字） |
| itemKey | O | ユーザーが反応した推薦アイテムの itemKey |
| userId | X | 推薦 API レスポンスの body.userId の値 |
| context | X | イベントの付加情報（自由形式のキー値。例: 表示位置 position、掲載面 placement） |
| userAttributes | X | ユーザー属性情報（自由形式のキー値） |
| options | X | 付加オプション（自由形式のキー値） |

成功レスポンス（200）は `header` のみを返します。

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

!!! tip "ヒント"
    - 成功レスポンス（200）は、収集パイプラインがイベントを受信したことを意味し、分析テーブルへの書き込み完了を保証するものではありません。
    - イベント API リクエスト後、データセットへの書き込みまで最大 10 分かかる場合があります。
    - タイムアウト後に再試行すると、同じイベントが重複して書き込まれる場合があります。分析時には重複排除を考慮してください。