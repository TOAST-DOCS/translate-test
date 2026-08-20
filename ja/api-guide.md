<!-- machine_translated: true -->

<a id="foundry.api.guide"></a>

## Machine Learning > NHN Cloud Foundry > APIガイド { #foundry.api.guide }

NHN Cloud Foundryが提供するAPIについて説明します。

| API | 説明 |
| --- | --- |
| Ingest API | 既存のデータソースにデータを収集します。スナップショットファイルのアップロードを提供します。 |
| 推薦照会 API | 作成した推薦システムアプリに推薦結果を要請します。 |
| 推薦イベント API | 推薦結果に対してユーザーが示した反応イベントを収集します。 |
<a id="auth.common"></a>

## 認証および共通事項 { #auth.common }

<a id="auth.common.preparation"></a>

### 事前準備 { #auth.common.preparation }

APIを使用するには、**Appkey** と**認証トークン**が必要です。

- AppkeyはNHN Cloudコンソールの**Machine Learning > NHN Cloud Foundry**ページ上部の**URL & Appkey**メニューで確認できます。
- APIは**gateway-public**エンドポイントを使用します。
- 認証トークン（`X-NHN-Authorization`ヘッダのBearerトークン）の発行方法については、[User Access Keyトークン](https://docs.nhncloud.com/ko/nhncloud/ko/public-api/user-access-key-token/)ガイドを参照してください。

<a id="auth.common.request"></a>

### リクエスト共通事項 { #auth.common.request }

必須ヘッダ:

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
| header.isSuccessful | Boolean | 요求の成否 |
| header.resultCode | Integer | 結果コード。成功時は 0、失敗時はエラーコード |
| header.resultMessage | String | 結果メッセージ。成功時は SUCCESS、失敗時はエラーの詳細 |
| body | Object/Array | APIごとのレスポンスデータ |
<a id="ingest.api"></a>

## Ingest API { #ingest.api }

Ingest APIは、コンソールで作成済みのデータソースにデータを積載するAPIです。
アップロードしたファイルでデータソースのデータをすべて置き換えるスナップショットアップロード方式を提供します。

!!! danger "注意"
    データソースを新規作成する API は提供していません。Ingest API を使用するには、コンソールでデータソースを先に作成する必要があり、FILE タイプのデータソースのみ使用できます。

<a id="ingest.snapshot"></a>

### スナップショットアップロード(ファイルアップロード) { #ingest.snapshot }

アップロードしたファイルの内容でデータソースのデータを**すべて置き換え**ます。アップロードは3段階で進みます。

!!! danger "注意"
    スナップショットのアップロードは、データソースにすでに積載されているデータをすべて置き換えます。既存のデータは復旧できません。

アップロード制限:

- 最大アップロードサイズ: **10GB**
- `100MB` 以下 → **単一アップロード (SINGLE)**
- `100MB` 超過 → **マルチパートアップロード (MULTIPART)**
- `formPost` フィールドの値は、レスポンスに含まれる値を**そのまま**リクエストに使用します。

<a id="ingest.snapshot.init"></a>

#### 1. アップロードの初期化 (init) { #ingest.snapshot.init }

| メソッド | URI |
| --- | --- |
| POST | /api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/init |
大容量ファイルをストレージに直接アップロードするための署名済み一時URLを発行します。ファイルサイズに応じて、単一URL（SINGLE）またはマルチパートURL（MULTIPART）を返します。

curl 例:

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
| fileName | String | O | ファイル名。使用可能な文字: 英字、数字、ピリオド(.)、アンダースコア(_)、ハイフン(-) |
| fileSize | Long | O | ファイルサイズ（bytes）。最小 1、最大 10GB |
| contentType | String | X | Content-Type（デフォルト: application/octet-stream） |
Response(SINGLE):

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

Response(MULTIPART):

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
    MULTIPART レスポンスにも `formPost` が含まれます。ただし、マルチパートアップロードは `parts[].uploadUrl` のクエリパラメータ（`signature`/`expires`/`max_file_size`/`max_file_count`）でパートを転送するため、`formPost` は参考用であり、パートのアップロード自体には使用しません。

| フィールド | 説明 |
| --- | --- |
| body.jobId | 作業ID。以降の complete / 状態照会リクエストに使用します |
| body.uploadType | アップロードタイプ。SINGLE（100MB 以下）または MULTIPART（100MB 超過） |
| body.uploadUrl | アップロードURL（単一アップロード時）|
| body.uploadId | マルチパートアップロードID（マルチパートアップロード時） |
| body.partSize | パート サイズ (bytes、マルチパートアップロード時) |
| body.parts[].partNumber | パート番号 (1から開始) |
| body.parts[].uploadUrl | パートアップロードURL |
| body.parts[].headUrl | ETag照会用URL（アップロード完了後にHEADリクエスト） |
| body.expiresAt | URLの有効期限 |
| body.formPost.objectPrefix | オブジェクトのプレフィックス（ファイル名の前に付くパス） |
| body.formPost.signature | HMAC-SHA1 署名 |
| body.formPost.expires | 有効期限（UNIX timestamp） |
| body.formPost.maxFileSize | 最大ファイルサイズ(bytes) |
| body.formPost.maxFileCount | 最大ファイル数 |
<a id="ingest.snapshot.upload.single"></a>

#### 2-A. 単一ファイルアップロード(100MB以下) { #ingest.snapshot.upload.single }

init レスポンスの `uploadUrl` に multipart/form-data POST を送信します。
このリクエストは Object Storage に直接送信されるため、別途認証は不要です（`signature` が認証の役割を担います）。

curl 例:

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
    `file` フィールドは必ずフォームデータの**最後**に追加する必要があります。成功時は HTTP `201 Created` レスポンスを受信します。

<a id="ingest.snapshot.upload.multipart"></a>

#### 2-B. 大容量ファイルのアップロード（100MB超、MULTIPART） { #ingest.snapshot.upload.multipart }

レスポンスの `parts[]` 配列を受け取り、パートごとにアップロードします。
各パートは **(1) アップロード → (2) HEAD で ETag を照会 → (3) `partETags[]` に `partNumber` の昇順で収集** の順序で処理します。

1. ファイルを `partSize`（デフォルト 100MB）単位で分割します。
2. パートごとに `parts[i].uploadUrl` のクエリパラメータ（`signature`、`expires`、`max_file_size`、`max_file_count`）をパースし、multipart/form-data で送信します（フィールド名 `file`、ファイル名固定 `part`）。
3. アップロード成功後、`parts[i].headUrl` に `HEAD` リクエストを送信し、レスポンスヘッダの `ETag` 値を収集します。
4. すべてのパートが完了したら、`partETags` 配列を `partNumber` の昇順で構成し、アップロード完了（complete）リクエストに含めて送信します。

パートアップロード curl の例:

```bash
# 1) アップロード
curl -X POST "{parts[i].uploadUrl}" \
  -F "redirect=" \
  -F "max_file_size={max_file_size-from-query}" \
  -F "max_file_count={max_file_count-from-query}" \
  -F "expires={expires-from-query}" \
  -F "signature={signature-from-query}" \
  -F "file=@./part_i.bin;filename=part"

# 2) ETag 照会
curl -I "{parts[i].headUrl}" | grep -i '^etag:'
```

<a id="ingest.snapshot.complete"></a>

#### 3. アップロード完了(complete) { #ingest.snapshot.complete }

| メソッド | URI |
| --- | --- |
| POST | /api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/complete |
curl 例(単一アップロード):

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

curl 예示(マルチパートアップロード):

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
| jobId | String | O | 作業ID（initレスポンスのjobId） |
| fileName | String | O | ファイル名 |
| uploadId | String | X | マルチパートアップロードID（マルチパートアップロード時のみ必要） |
| partETags | Array | X | パートごとのETagリスト（マルチパートアップロード時のみ必要、partNumber順） |
Response:

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
| body.jobId | 作業ID。[作業状態照会](#ingest.snapshot.job.status)に使用します |
<a id="ingest.snapshot.cancel"></a>

#### アップロード取消 { #ingest.snapshot.cancel }

| メソッド | URI |
| --- | --- |
| DELETE | /api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/{jobId} |
curl 例(単一アップロード):

```bash
curl -X DELETE "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/{jobId}" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}"
```

curl 例(マルチパートアップロード) - クエリパラメータで `uploadId` を一緒に渡します:

```bash
curl -X DELETE "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/{jobId}?uploadId={uploadId}" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}"
```

<a id="ingest.snapshot.job.status"></a>

#### 作業状態照会 { #ingest.snapshot.job.status }

| メソッド | URI |
| --- | --- |
| GET | /api/v1.0/data-sources/{dataSourceId}/ingest/jobs/{jobId} |
curl 例:

```bash
curl "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/jobs/{jobId}" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}"
```

Response:

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
| body.jobId | 作業ID |
| body.dataSourceId | 対象データソースID |
| body.jobType | 作業タイプ。SNAPSHOT（スナップショット積載）またはEVENT（変更イベント） |
| body.status | 作業状態。以下のステータス値を参照 |
| body.obsFilePath | OBS ファイルパス |
| body.statistics.totalRecords | 総レコード数 |
| body.statistics.failedRecords | 失敗レコード数 |
| body.statistics.successfulRecords | 成功レコード数 |
| body.statistics.successRate | 成功率（0.0〜1.0） |
| body.errorMessage | エラーメッセージ(失敗時) |
| body.createdDatetime | 作業作成日時 |
| body.startedDatetime | 作業開始日時 |
| body.completedDatetime | 作業完了日時 |
| body.modifiedDatetime | 最終更新日時 |
作業状態（`status`）は次の値を持ちます。

| 値 | 説明 |
| --- | --- |
| UPLOADING | ファイルをアップロードしています。 |
| STAGED | 処理の準備が完了しました。 |
| RUNNING | データを積載中です。|
| COMPLETED | 作業が正常に完了しました。 |
| FAILED | 作業が失敗しました。 |
<a id="recommendation.api"></a>

## 推薦照会 API { #recommendation.api }

作成した推薦システムアプリに推薦結果をリクエストします。ユーザーの履歴が十分な場合はモデルベース（Normal Flow）、不足している場合は属性ベース（Cold Start）で推論します。

<a id="recommendation.api.recommend"></a>

### 推薦リクエスト { #recommendation.api.recommend }

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
| userId | String | O | 推薦対象のユーザーID |
| context | Object | X | リクエストのコンテキスト情報 |
| context.currentItemKey | String | X | 現在表示しているアイテムキー |
| context.recentlyViewed | Array | X | 最近閲覧したアイテムキーのリスト |
| context.pageType | String | X | 現在のページタイプ。home、course_detail、course_list、search_result、my_page |
| context.sessionId | String | X | セッションID |
| userAttributes | Object | X | ユーザーの属性情報。Cold Start 推論に使用されます |
| userAttributes.jobCategory | String | X | 職業/職種 |
| userAttributes.interestArea | Array | X | 関心分野リスト |
| userAttributes.experienceYears | Integer | X | 経験年数 |
| options.maxRecommendations | Integer | X | 最大推薦数（1〜100、デフォルト 10） |
| options.excludeItemKeys | Array | X | 推薦から除外するアイテムキーの一覧 |
!!! tip "ヒント"
    `userAttributes` スキーマは、今後の選好度導出 (Preference Elicitation) の実装方針によって、収集方法やフィールドの種類が変更される場合があります。

Response:

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
      "inferenceType": "normal",
      "abTestGroup": "treatment"
    }
  }
}
```

| フィールド | 説明 |
| --- | --- |
| body.userId | リクエストしたユーザーID |
| body.recommendations[].itemKey | 推薦アイテムキー |
| body.recommendations[].score | 推薦スコア(0.0〜1.0) |
| body.recommendations[].position | 推薦順位 |
| body.metadata.modelVersion | 使用されたモデルバージョン |
| body.metadata.requestId | リクエスト追跡ID。推薦イベントAPIの送信時にこの値を使用します |
| body.metadata.inferenceType | 推論タイプ。normal（履歴ベース）またはcold_start（属性ベース） |
| body.metadata.abTestGroup | A/B テストグループ。treatment、control、none |
<a id="recommendation.event.api"></a>

## 推薦イベント API { #recommendation.event.api }

推薦結果に対してユーザーが示した反応（クリックなど）のイベントを収集します。積載されたイベントデータで推薦の成功率を分析できます。

<a id="recommendation.event.api.send"></a>

### 推薦イベント転送 { #recommendation.event.api.send }

| メソッド | URI |
| --- | --- |
| POST | /api/v1.0/recommendation-apps/{appId}/events |
curl 例:

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

`requestId`、`itemKey`、`userId`は、推薦照会 API レスポンスで受け取った値をそのまま渡します。

| フィールド | 必須 | 説明 |
| --- | --- | --- |
| eventType | O | イベントタイプ。自由に定義できます（例: CLICK、PURCHASE、IMPRESSION）。英字・数字・アンダースコアのみ使用可（^[A-Za-z0-9_]+$）、最大 64 文字。大文字・小文字は区別されず、大文字に正規化されて保存されます。REQUEST、RESPONSE は予約語のため使用できません |
| requestId | O | 推薦 API レスポンスの body.metadata.requestId の値(opaque string、最大 128 文字) |
| itemKey | O | ユーザーが反応した推薦アイテムのitemKey |
| userId | X | 推薦 API レスポンスの body.userId の値 |
| context | X | イベント付加情報（自由形式のキーと値。例: 表示位置 position、面 placement） |
| userAttributes | X | ユーザー属性情報（自由形式のキーと値） |
| options | X | 追加オプション（自由形式のキーと値） |
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
    - 成功レスポンス（200）は、収集パイプラインがイベントを受信したことを意味し、分析テーブルへの積載完了を保証するものではありません。
    - イベント API リクエスト後、データセットへの積載まで最大 10 分かかる場合があります。
    - タイムアウト後にリトライすると、同じイベントが重複して積載される可能性があります。分析時には重複除去を考慮してください。