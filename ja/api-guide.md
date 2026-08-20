<!-- machine_translated: true -->

## Data & Analytics > Log & Crash Search > APIガイド

### Appkey & SecretKey

Log & Crash Search APIを使用するには、AppkeyとSecretKeyが必要です。

Appkeyは、NHN Cloudの各サービスごとに発行される固有の認証キーであり、APIリクエスト時のサービス識別と有効性検証に使用されます。SecretKeyは、APIへのアクセスを制御するシークレットキーです。

Appkey および SecretKey の確認と使用方法の詳細については、[Appkey](/nhncloud/ja/public-api/appkey) を参照してください。

## ログ収集 API

HTTP プロトコルを使用して Log & Crash 収集サーバーにログを送信できます。

> - JSON/HTTP で Log & Crash 収集サーバーにログを送信する場合は、次のアドレスを使用する必要があります。
>     - Log & Crash: api-logncrash.nhncloudservice.com
>     - Method of Delivery: POST
>     - URI: /v2/log
>     - Content-Type: "application/json"
> - ログを送信する前に、Log & Crash にプロジェクトを登録済みであることを確認します。
> - "logTime" は Log & Crash システムで使用されます。このキーを使用した場合、Log & Crash では無視されます。
> - キー名にスペースが含まれないように注意してください。たとえば、"UserID" と "UserID " は異なるキーとして認識されます。
> - HTTP リクエスト 1 件あたりの最大サイズは 52MB です。
> - ログ (JSON) 1 件あたりの最大サイズは 8MB (8,388,608 バイト) です。

下記のようなJSON形式を使用します。

```
{
	"projectName": "__アプリケーションキー__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "This log message come from HTTP client.",
	"logSource": "http",
	"logType": "nelo2-log",
	"host": "localhost"
}
```

[基本パラメータ]

```
Log Search のためのパラメーター

projectName: string, 必須
	[in] アプリキー。

projectVersion: string, 必須
	[in] バージョン。ユーザー定義可能。"A~Z, a~z, 0~9, -._" のみ含む。

body: string, オプション
	[in] ログメッセージ。

logVersion: string, 必須
	[in] ログフォーマットバージョン。"v2"。

logSource: string, オプション
	[in] ログソース。Log Search でフィルタリングのために使用。定義されていない場合は "http"。

logType: string, オプション
	[in] ログタイプ。Log Search でフィルタリングのために使用。定義されていない場合は "log"。

host: string, オプション
	[in] ログを送信する端末のアドレス。定義されていない場合は、収集サーバーで peer-address を使用して自動的に入力されます。
```

[その他のパラメータ]

```
sendTime: string, オプション
	[in] 端末が送信した時刻。入力する場合は Unix タイムスタンプ形式で入力します。

logLevel: string, オプション
	[in] Syslog イベント用。

UserBinaryData: string, オプション
	[in] ログ検索画面に [ダウンロード|表示] リンクを表示します。base64 エンコードされた値を格納して送信します。

UserTxtData: string, オプション
	[in] ログ検索画面に [ダウンロード|表示] リンクを表示します。base64 エンコードされた値を格納して送信します。

txt*: string, オプション
	[in] フィールド名が txt で始まるフィールド（txtMessage、txt_description など）は、text フィールドとして保存されます。ログ検索画面でフィールド値の一部の文字列による検索（全文検索）が可能です。フィールドのサイズは 1MB に制限されます。

long*: long, オプション
	[in] フィールド名が long で始まるフィールド（longElapsedTime、long_elapsed_time など）は、long 型フィールドとして保存されます。ログ検索画面で long 型の範囲検索が可能です。

double*: double, オプション
	[in] フィールド名が double で始まるフィールド（doubleAvgScore、double_avg_score など）は、double 型フィールドとして保存されます。ログ検索画面で double 型の範囲検索が可能です。
```

[カスタムフィールド]

```
カスタムフィールド名は「A〜Z、a〜z」で始まり、「A〜Z、a〜z、0〜9、-、_」の文字を使用できます。

上記の基本パラメーター、Crash パラメーターと名前が重複しないようにしてください。

カスタムフィールドはフィールドの文字列全体と一致する検索のみ可能です（exact match）。

カスタムフィールドの長さは 1KB に制限されます。1KB を超えて送信する場合、またはフィールド値の一部の文字列を検索する必要がある場合は、`txt*` プレフィックスを付けてフィールドを作成する必要があります。
```

[返却値]
収集サーバーから次のように返却します。

```
Content-Type: application/json

{
	"header":{
		"isSuccessful":true,
		"resultCode":0,
		"resultMessage":"Success"
	}
}

isSuccessful: boolean
	[out]成功時はtrue、失敗時はfalse

resultCode: int
	[out]成功時は0、失敗時はエラーコード

resultMessage: string
	[out]成功時は"Success"、失敗時はエラーメッセージ
```

[Bulk転送]
Bulkで転送するにはJSON array形式で転送します。

```
[
    {
        "projectName": "__アプリケーションキー__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client. (1/2)",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost"
    },
    {
        "projectName": "__アプリケーションキー__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client. (2/2)",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost"
    }
]
```

* 注記
    * ウェブでは受信時刻を基準にログを並べ替えて表示しますが、Bulk 送信の場合は同一時刻に受信したものとみなされるため、ユーザーが送信した順序が維持されません。
        * Bulk で送信するログの順序を維持するには、各ログに `lncBulkIndex` フィールドを追加して Integer 値を指定した上で送信すると、サーバーではこの値を基準に降順で表示します。

```
[
    {
        "projectName": "__アプリキー__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "first message",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost",
        "lncBulkIndex":1
    },
    {
        "projectName": "__アプリキー__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "second message",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost",
        "lncBulkIndex":2
    }
]
```
        * 上記の例のように送信した場合、サーバーでは second message → first message の順で表示されます。

収集サーバーは、送信された順序に従って、それぞれの結果値を JSON 配列形式で返します。

```
Content-Type: application/json

{
    "header":{
        "isSuccessful":true,
        "resultCode":0,
        "resultMessage":"Success"
    },
    "body":{
        "data":{
            "total":5,
            "errors":2,
            "resultList":[
                {"isSuccessful":true, "resultMessage":"Success"},
                {"isSuccessful":true, "resultMessage":"Success"},
                {"isSuccessful":false, "resultMessage":"LogVersion Mismatch: v1, /v2/log"},
                {"isSuccessful":false, "resultMessage":"The project(invalidProject) is not registered"},
                {"isSuccessful":true, "resultMessage":"Success"}
            ]
        }
    }
}

total: int
    [out] 送信されたログの総数

errors: int
    [out] 送信されたログのうちエラーの数

resultList: array
    [out] 送信された各ログの結果値
```

### サンプル

[curlを使用して正常にログを転送した場合]

```
//POSTメソッドを使用してログを送信
$ curl -H "content-type:application/json" -XPOST 'https://api-logncrash.nhncloudservice.com/v2/log' -d '{
	"projectName": "__アプリキー__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http"
}'
```

[ログの転送に失敗する場合]

```
//URLが間違っている場合(log -> loggg)
$ curl -v -H 'content-type:application/json' -XPOST "api-logncrash.nhncloudservice.com/v2/loggg" -d '{
	"projectName": "__アプリキー__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http"
}'


//無効なフィールドキーを使用した場合(_xxx)
$ curl -v -H 'content-type:application/json' -XPOST "api-logncrash.nhncloudservice.com/v2/log" -d '{
	"projectName": "__アプリキー__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http",
	"_xxx": "this is a invalid key"
	}'
カスタムキーは「A〜Z、a〜z、0〜9、-_」を含み、アルファベットで始まる必要があります。
```

[curlを使用してログをBulk送信した場合]

```
//POST メソッドを使用してログ送信
$ curl -H "content-type:application/json" -XPOST 'https://api-logncrash.nhncloudservice.com/v2/log' -d '[
    {
        "projectName": "__アプリキー__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client, and it is a simple bulk sample. (1/2)",
        "logSource": "http",
        "logType": "nelo2-log"
    },
    {
        "projectName": "__アプリキー__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client, and it is a simple bulk sample. (2/2)",
        "logSource": "http",
        "logType": "nelo2-log"
    }
]'
```

## ログ検索API

> [注意] このAPIはサポート終了予定です。新規開発時には、以下の[v3 ログ検索 API](#v3-로그-검색-api)の使用をお勧めします。

保存されたログを Lucene クエリーを使用して検索できます。<br>
ログ検索 API は使用パターンに応じて、1 時間あたりにリクエストできる量を制限します。検索に使用可能なリソースはトークンで表され、検索 API を呼び出すたびに内部基準に従って一定量が差し引かれます。トークン残量が正の値のとき、検索 API を使用できます。<br>
検索時に差し引かれるトークン数は、検索期間および容量、クエリーの複雑さによって異なり、トークンは時間の経過とともに自動的に補充されます。<br>

![lncs-api-01-20230925](https://static.toastoven.net/prod_logncrash/lncs-api-01-20230925.png)

### 基本情報

```
API Endpoint: https://api-lncs-search.nhncloudservice.com
```
```
検索は最近90日以内のログのみ可能で、開始時間と終了時間の範囲は31日を超えることはできません。
```

### Search API

Luceneクエリーを使用して、指定した時間範囲のログを照会します。検索結果（totalItems）には制限はありませんが、ページングで照会できる範囲は最大 100,000 件（`pageNumber × pageSize ≤ 100,000`）までです。それ以上のログを照会するには、Search API（Cursorページネーション）または Scroll API を使用してください。
```
POST /api/v2/search/{appkey}

Content-Type: application/json
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリケーションキー | O | 

#### リクエストヘッダ

| 名前 | 形式 | 説明            | 必須 |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | プロジェクト SecretKey | O |

#### リクエスト本文

| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Luceneクエリ | O |  |
| from | String | 開始時間 | O | ISO8601形式日付(YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | 終了時間 | O | ISO8601形式日付(YYYY-MM-DDThh:mm:ss.sTZD) |
| pageNumber | Number | ページ番号 |  | デフォルト値0 |
| pageSize | Number | ページサイズ |  | デフォルト値10、最大値100 |
| sort | Object | ソート基準 |  | フィールドごとの昇順(ASC)および降順(DESC)設定 |

<details>
<summary>例</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2021-01-01T10:00:00+09:00",
  "to": "2021-01-01T11:00:00+09:00",
  "pageSize": 10,
  "pageNumber": 1,
  "sort": {
      "projectVersion": "asc"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| totalItems | Body | Number | ログ数 |
| pageNumber | Body | Number | ページ番号 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログリスト |

<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 50,
        "pageNumber": 1,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>


### Search API (Cursor ページネーション)

Search API と同じエンドポイントで URL クエリパラメーター `?cursor` を指定してオプトイン (opt-in) すると、cursor (search_after) ベースのページネーションを使用できます。深いページに移動しても、`pageNumber × pageSize` の result window の上限 (基本検索 API 100,000 件) の影響を受けずに、順番に次のページを照会できます。

```
POST /api/v2/search/{appkey}?cursor

Content-Type: application/json
```

> - URLクエリパラメータ `?cursor`、`?cursor=true` を指定すると、cursorページネーションが有効になります。オプトインしない場合は、既存の Search API の動作がそのまま維持されます。
> - cursorをオプトインした場合、`pageNumber` を同時に送信することはできません（同時に指定した場合は 400 レスポンスが返されます）。最初のページリクエスト時には `cursor` を空にし、以降のページでは直前のレスポンスの `nextCursor` 値をそのまま次のリクエストの `cursor` フィールドに渡します。
> - `cursor` 値は、サーバー内部のソート状態をエンコードした opaque 文字列です。クライアント側でパースまたは変形しないでください。
> - 1 回の呼び出しで受け取ることができるページサイズの上限（`pageSize` の最大値 100）は、通常の Search API と同様に適用されます。
> - 最後のページに到達すると、レスポンス本文に `nextCursor` フィールドは含まれません。

#### リクエストパラメータ

| 名前 | 位置 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- | --- |
| appkey | Path | String | プロジェクトアプリキー | O |
| cursor | Query | - | cursorベースのページネーションのオプトインフラグ。`?cursor`、`?cursor=true` を指定すると有効になります | O |
#### リクエストヘッダー

| 名前 | 形式 | 説明 | 必須 |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | プロジェクト SecretKey | O |
#### リクエスト本文

| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Luceneクエリー | O |  |
| from | String | 開始時間 | O | ISO8601 形式の日付 (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | 終了時間 | O | ISO8601 形式の日付 (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | ソート基準 |  | フィールドごとの昇順（ASC）および降順（DESC）の設定 |
| cursor | String | 次のページ照会用カーソル |  | 最初のページでは省略。以降のページでは、直前のレスポンスの `nextCursor` の値をそのまま渡します。`pageNumber` と同時に使用することはできません(400) |
<details>
<summary>例</summary>

最初のページリクエスト（`cursor` 未指定）：

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2021-01-01T10:00:00+09:00",
  "to": "2021-01-01T11:00:00+09:00",
  "pageSize": 10,
  "sort": {
      "logTime": "desc"
  }
}
```

次のページリクエスト（直前のレスポンスの `nextCursor` をそのまま渡す）:

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2021-01-01T10:00:00+09:00",
  "to": "2021-01-01T11:00:00+09:00",
  "pageSize": 10,
  "sort": {
      "logTime": "desc"
  },
  "cursor": "g2VleUlkLi4u"
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| totalItems | Body | Number | ログ数 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログリスト |
| nextCursor | Body | String | 次のページ照会用カーソル。次の結果が存在する場合にのみ含まれ、最後のページには含まれません |
<details>
<summary>例</summary>

次のページが存在するとき（レスポンスに `nextCursor` が含まれる場合）：

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 50,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ],
        "nextCursor": "g2VleUlkLi4u"
    }
}
```

最後のページの場合（レスポンスに `nextCursor` が含まれない場合）:

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 50,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Scroll Start API

Luceneクエリを使って指定した時間範囲のログをページ指定なしで全て照会します。Scroll Continue APIと一緒に使って複数回に渡って照会できます。
```
POST /api/v2/search/scroll/{appkey}
Content-Type: application/json
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリケーションキー | O | 

#### リクエストヘッダ

| 名前 | 形式 | 説明            | 必須 |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | プロジェクト SecretKey | O |

#### リクエスト本文

| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Luceneクエリ | O |  |
| from | String | 開始時間 | O | ISO8601形式日付(YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | 終了時間 | O | ISO8601形式日付(YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | ページサイズ |  | デフォルト値10、最大値100 |
| sort | Object | ソート基準 |  | フィールドごとの昇順(ASC)および降順(DESC)設定 |

<details>
<summary>例</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2021-01-01T10:00:00+09:00",
  "to": "2021-01-01T11:00:00+09:00",
  "pageSize": 10,
  "sort": {
      "projectVersion": "asc"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | ログ数 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログリスト |

<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "scrollKey": "51482f39-d499-394d-adca-462585a477e9",
        "totalItems": 60,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>


### Scroll Continue API

Scroll Start API または直前に呼び出した Scroll Continue API から取得した Scroll Key を指定して、ログ照会を継続します。<br>
Scroll Key は 1 分間有効です。
```
POST /api/v2/search/scroll/{appkey}/{scrollKey}

Content-Type: application/json
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリケーションキー | O |
| scrollKey | String | Scroll Key | O |

#### リクエストヘッダ

| 名前 | 形式 | 説明            | 必須 |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | プロジェクト SecretKey | O |

#### リクエスト本文

Scroll Continue APIはリクエスト本文が必要しません。

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | ログ数 |
| data | Body | List | ログリスト |

<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "scrollKey": "51482f39-d499-394d-adca-462585a477e9",
        "totalItems": 60,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Available Token API

使用可能なトークン数を照会します。
```
GET /api/v2/search/available-tokens/{appkey}
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリケーションキー | O |

#### リクエストヘッダ

| 名前 | 形式 | 説明            | 必須 |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | プロジェクト SecretKey | O |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| availableToken | Body | Number | 使用可能なトークン |

<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "availableToken": 9875
    }
}
```
</details>
## v3 ログ検索 API

保存されたログを Lucene クエリーを使用して検索できます。また、クラッシュ分析用の Symbol ファイルのアップロード・照会・削除機能を提供します。<br>
ログ検索 API は、使用パターンに応じて 1 時間あたりのリクエスト数を制限します。検索に使用できるリソースはトークンで表され、検索 API を呼び出すたびに内部基準に従って一定量が差し引かれます。トークン残量が正の値のとき、検索 API を使用できます。<br>
検索時に差し引かれるトークン数は、検索期間・容量・クエリーの複雑さによって異なります。トークンは時間の経過とともに自動的に補充されます。<br>

### 認証

API の呼び出しおよび認証のための方法として、User Access Key トークンをサポートしています。<br>
トークンの発行方法については、以下のリンクを参照してください。

[User Access Key Token](https://docs.nhncloud.com/ko/nhncloud/ko/public-api/user-access-key-token/)

#### API リクエストの HTTP ヘッダー例

```
X-NHN-Authorization: Bearer {Access Token}
```

### Search API

Luceneクエリーを使用して、指定した時間範囲のログを照会します。検索結果（totalItems）に件数の制限はありませんが、ページングで照会できる範囲は最大 100,000 件（`pageNumber × pageSize ≤ 100,000`）までです。それ以上のログを照会するには、Cursor Search API または Scroll API を使用してください。
```
POST /v3/{appkey}/logs/search

Content-Type: application/json
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |
#### リクエストヘッダー

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式のユーザーアクセスキートークン | O |
#### リクエスト本文

| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Luceneクエリー | O |  |
| from | String | 開始時間 | O | ISO8601 形式の日付 (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | 終了時間 | O | ISO8601 形式の日付 (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageNumber | Number | ページ番号 |  | デフォルト値 0 |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | ソート基準 |  | フィールドごとの昇順（ASC）および降順（DESC）の設定 |
<details>
<summary>例</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2026-03-24T00:00:00+09:00",
  "to": "2026-03-24T23:59:59.999+09:00",
  "pageSize": 10,
  "pageNumber": 0,
  "sort": {
      "logTime": "DESC"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| totalItems | Body | Number | ログ数 |
| pageNumber | Body | Number | ページ番号 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログリスト |
<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 20927,
        "pageNumber": 0,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Cursor Search API

cursor(opaque) ベースのページネーションでログを検索します。<br>
深いページに移動しても `pageNumber × pageSize` の result window の制限に影響されることなく、順次照会できます。

- 最初のページをリクエストする際は、body の `cursor` を省略します。
- 次のページをリクエストする際は、直前のレスポンスの `nextCursor` 値を body の `cursor` フィールドにそのまま渡します。
- 最後のページに到達すると、レスポンスの body に `nextCursor` は含まれません。
- `cursor` 値は、バックエンド内部のソート状態をエンコードした opaque 文字列です。クライアント側でパースや変形を行わないでください。
- `pageNumber` は使用しません。body に含めると 400 レスポンスが返されます。

```
POST /v3/{appkey}/logs/cursor

Content-Type: application/json
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |
#### リクエストヘッダー

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式のユーザーアクセスキートークン | O |
#### リクエスト本文

| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Luceneクエリー | O |  |
| from | String | 開始時間 | O | ISO8601 形式の日付 (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | 終了時間 | O | ISO8601 形式の日付 (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | ソート基準 |  | フィールドごとの昇順（ASC）および降順（DESC）の設定 |
| cursor | String | 前回のレスポンスの `nextCursor` 値 |  | 最初のページをリクエストする際は省略 |
<details>
<summary>例</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2026-03-24T00:00:00+09:00",
  "to": "2026-03-24T23:59:59.999+09:00",
  "pageSize": 10,
  "sort": {
      "logTime": "DESC"
  },
  "cursor": "g6JpdGVtc4123WsBYWKhYWOhYWQ"
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| totalItems | Body | Number | ログ数 |
| pageNumber | Body | Number | ページ番号（cursorモードでは常に `0` 固定、意味なし） |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログリスト |
| nextCursor | Body | String | 次のページ照会用の opaque カーソル（最終ページには含まれません） |
<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 20907,
        "pageNumber": 0,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ],
        "nextCursor": "ghsAAAGePyNW0XZpRnFtZm42Q31231pRcHJ2UC9MMGpR"
    }
}
```
</details>

### Scroll Start API

Luceneクエリーを使用して、指定した時間範囲のログをページ指定なしですべて照会します。Scroll Continue API と組み合わせて、複数回に分けて照会できます。
```
POST /v3/{appkey}/logs/scroll

Content-Type: application/json
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |
#### リクエストヘッダー

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式のユーザーアクセスキートークン | O |
#### リクエスト本文

| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Luceneクエリー | O |  |
| from | String | 開始時間 | O | ISO8601 形式の日付 (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | 終了時間 | O | ISO8601 形式の日付 (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | ソート基準 |  | フィールドごとの昇順（ASC）および降順（DESC）の設定 |
<details>
<summary>例</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2026-03-24T00:00:00+09:00",
  "to": "2026-03-24T23:59:59.999+09:00",
  "pageSize": 10,
  "sort": {
      "logTime": "DESC"
  }
}
```
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | ログ数 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログリスト |
<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "scrollKey": "12345bd8-d5a3-3d42-8711-16bc225b0e59",
        "totalItems": 20943,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Scroll Continue API

Scroll Start API または直前に呼び出した Scroll Continue API から取得した Scroll Key を指定して、ログ照会を継続します。<br>
Scroll Key は 1 分間有効です。
```
POST /v3/{appkey}/logs/scroll/{scrollKey}

Content-Type: application/json
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |
| scrollKey | String | Scroll Key | O |
#### リクエストヘッダー

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式のユーザーアクセスキートークン | O |
#### リクエスト本文

Scroll Continue API はリクエスト本文を必要としません。

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | ログ数 |
| data | Body | List | ログリスト |
<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "scrollKey": "12345bd8-d5a3-3d42-8711-16bc225b0e59",
        "totalItems": 20943,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Available Token API

使用可能なトークン数を照会します。
```
GET /v3/{appkey}/logs/available-token
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |
#### リクエストヘッダー

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式のユーザーアクセスキートークン | O |
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| availableToken | Body | Number | 使用可能なトークン |
<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "availableToken": 9975
    }
}
```
</details>

### Symbol Upload API

クラッシュ分析用のSymbolファイルをアップロードします。
```
POST /v3/{appkey}/symbols?platform={platform}&version={version}&description={description}

Content-Type: multipart/form-data
```

#### リクエストパラメータ

| 名前 | 位置 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- | -- |
| appkey | Path | String | プロジェクトアプリキー | O |
| platform | Query | String | Symbolの対象プラットフォーム（`iOS`、`Android`、`Android-NDK`、`Windows` のいずれか） | O |
| version | Query | String | Symbolバージョン | O |
| description | Query | String | シンボルの説明（空白などの特殊文字はURLエンコードが必要） |  |
#### リクエストヘッダー

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式のユーザーアクセスキートークン | O |
#### リクエスト本文

| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| symbolfile | Binary | シンボルファイル | O | multipart/form-data 形式で送信 |
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| result.data.id | Body | List | アップロードされた Symbol ファイルの識別子リスト |
<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "result": {
        "data": {
            "id": [
                "1239aaba9c74f678c6df8b8"
            ]
        }
    }
}
```
</details>

### Symbol List API

アップロードされた Symbol ファイルの一覧を照会します。`platform`/`version` の値でフィルタリングし、全件照会する場合は両方の値を `all` として呼び出します。
```
GET /v3/{appkey}/symbols/{platform}/{version}
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |
| platform | String | Symbolプラットフォームフィルター（全件取得の場合は `all`） | O |
| version | String | Symbolバージョンフィルター（全件取得時は`all`） | O |
#### リクエストヘッダー

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式のユーザーアクセスキートークン | O |
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| result.data | Body | List | Symbolファイルリスト |
<details>
<summary>例</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "result": {
        "data": [
            {
                ...
            }
        ]
    }
}
```
</details>

### Symbol Delete API

Symbol ファイルを1件削除します。
```
DELETE /v3/{appkey}/symbols/{sid}
```

#### リクエストパラメータ

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |
| sid | String | シンボルファイル ID | O |
#### リクエストヘッダー

| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式のユーザーアクセスキートークン | O |
#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| header.isSuccessful | Body | Boolean | 成功かどうか |
| header.resultCode | Body | Number | 結果コード |
| header.resultMessage | Body | String | 結果メッセージ |
<details>
<summary>例</summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultMessage": "success",
    "resultCode": 0
  }
}
```
</details>
