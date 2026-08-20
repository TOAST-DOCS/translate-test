<!-- machine_translated: true -->

<!-- pre-align:aligned sig=a929413d0034 -->

## Data & Analytics > Log & Crash Search > API 가이드
### Appkey と SecretKey
Log & Crash Search API を使用するには、Appkey と SecretKey が必要です。

Appkey は NHN Cloud の各サービスごとに発行される固有の認証キーで、API リクエスト時にサービスの識別と有効性検証に使用されます。SecretKey は API へのアクセスを制御するシークレットキーです。

Appkey および SecretKey の確認と使用方法の詳細については、[Appkey](/nhncloud/ja/public-api/appkey-gov) を参照してください。

## ログ収集 API

HTTP プロトコルを使用して Log & Crash 収集サーバーにログを送信できます。

> - JSON/HTTP で Log & Crash 収集サーバーにログを送信する際は、次のアドレスを使用する必要があります。
>     - Log & Crash: api-logncrash.gov-nhncloudservice.com
>     - Method of Delivery: POST
>     - URI: /v2/log
>     - Content-Type: "application/json"
> - ログを送信する前に、Log & Crash にプロジェクトを登録済みであることを確認します。
> - "logTime" は Log & Crash システムで使用されます。このキーを使用すると、Log & Crash では無視されます。
> - キー名に空白文字が含まれないよう注意してください。たとえば、"UserID" と "UserID " は異なるキーとして認識されます。
> - HTTP リクエスト 1 件の最大サイズは 52MB です。
> - ログ (JSON) 1 件の最大サイズは 8MB (8,388,608 バイト) です。

以下の JSON 形式を使用します。

```
{
	"projectName": "__アプリキー__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "This log message come from HTTP client.",
	"logSource": "http",
	"logType": "nelo2-log",
	"host": "localhost"
}
```

[基本パラメーター]

```
Log Search のためのパラメーター

projectName: string, 必須
	[in] アプリキー。

projectVersion: string, 必須
	[in] バージョン。ユーザー定義可能。"A~Z, a~z, 0~9, -._" のみを含む。

body: string, オプション
	[in] ログメッセージ。

logVersion: string, 必須
	[in] ログフォーマットバージョン。"v2"。

logSource: string, オプション
	[in] ログソース。Log Search でのフィルタリングに使用。定義されていない場合は "http"。

logType: string, オプション
	[in] ログタイプ。Log Search でのフィルタリングに使用。定義されていない場合は "log"。

host: string, オプション
	[in] ログを送信する端末のアドレス。定義されていない場合は、収集サーバーが peer-address を使用して自動的に入力します。
```

[その他のパラメーター]

```
sendTime: string, オプション
	[in] 端末が送信した時刻。入力時は Unix timestamp 形式で入力します。

logLevel: string, オプション
	[in] Syslog イベント用。

UserBinaryData: string, オプション
	[in] ログ検索画面に [ダウンロード|表示] リンクを表示します。base64 エンコードされた値を格納して送信します。

UserTxtData: string, オプション
	[in] ログ検索画面に [ダウンロード|表示] リンクを表示します。base64 エンコードされた値を格納して送信します。

txt*: string, オプション
	[in] フィールド名が txt で始まるフィールド (txtMessage、txt_description など) は text フィールドとして保存されます。ログ検索画面でフィールド値の一部の文字列で検索 (全文検索) できます。フィールドのサイズは 1MB に制限されます。

long*: long, オプション
	[in] フィールド名が long で始まるフィールド (longElapsedTime、long_elapsed_time など) は long 型フィールドとして保存されます。ログ検索画面で long 型の範囲検索が可能です。

double*: double, オプション
	[in] フィールド名が double で始まるフィールド (doubleAvgScore、double_avg_score など) は double 型フィールドとして保存されます。ログ検索画面で double 型の範囲検索が可能です。
```

[カスタムフィールド]

```
カスタムフィールド名は "A〜Z、a〜z" で始まり、"A〜Z、a〜z、0〜9、-、_" の文字を使用できます。

上記の基本パラメーター、Crash パラメーターと名前が重複しないようにしてください。

カスタムフィールドは、フィールドの文字列全体と一致する検索のみ可能です（完全一致）。

カスタムフィールドの長さは 1 KB に制限されます。1 KB を超えて送信する場合、またはフィールド値の一部の文字列を検索する必要がある場合は、txt* プレフィックスを付けてフィールドを作成する必要があります。
```

[戻り値]  
収集サーバーから次のように返されます。

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
	[out] 成功時は true、失敗時は false

resultCode: int
	[out] 成功時は 0、失敗時はエラーコード

resultMessage: string
	[out] 成功時は "Success"、失敗時はエラーメッセージ
```

[Bulk 送信]
Bulk で送信するには、JSON array 形式で送信します。

```
[
    {
        "projectName": "__アプリキー__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client. (1/2)",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost"
    },
    {
        "projectName": "__アプリキー__",
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
    * Web では受信時刻を基準にログを並べて表示しますが、Bulk 送信の場合は同じ時刻に受信したものとみなされるため、ユーザーが送信した順序が維持されません。
        * Bulk で送信するログの順序を維持するには、各ログに `lncBulkIndex` フィールドを追加して Integer 値を指定して送信すると、サーバーではこの値を基準に降順で表示されます。

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
        * 上記の例のように送信した場合、サーバーでは second message → first message の順序で表示されます。

収集サーバーでは、送信された順序に従って各結果値を JSON array 形式で返します。

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
    [out] 送信されたログのうち、エラーの数

resultList: array
    [out] 送信された各ログの結果値
```

### サンプル

[curl を使用して正常にログを送信した場合]

```
//POSTメソッドを使用してログ送信
$ curl -H "content-type:application/json" -XPOST 'https://api-logncrash.gov-nhncloudservice.com/v2/log' -d '{
	"projectName": "__アプリキー__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http"
}'
```

[ログ送信に失敗する場合]

```
//URLが間違っている場合(log -> loggg)
$ curl -v -H 'content-type:application/json' -XPOST "api-logncrash.gov-nhncloudservice.com/v2/loggg" -d '{
	"projectName": "__앱키__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http"
}'


//不正なフィールドキーを使用した場合(_xxx)
$ curl -v -H 'content-type:application/json' -XPOST "api-logncrash.gov-nhncloudservice.com/v2/log" -d '{
	"projectName": "__앱키__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http",
	"_xxx": "this is a invalid key"
	}'
カスタムキーは「A〜Z、a〜z、0〜9、-_」を含み、アルファベットで始まる必要があります。
```

[curl を使用してログを Bulk 送信した場合]

```
//POST メソッドを使用してログ送信
$ curl -H "content-type:application/json" -XPOST 'https://api-logncrash.gov-nhncloudservice.com/v2/log' -d '[
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

## ログ検索 API

> [注意] この API はサポート終了予定です。新規開発の際は、以下の [v3 ログ検索 API](#v3-ログ検索-api) の使用をお勧めします。

保存されたログを Luceneクエリーを使用して検索できます。<br>
ログ検索 API は使用パターンに応じて、1 時間あたりにリクエストできる量を制限します。検索に使用できるリソースはトークンで表現され、検索 API を呼び出すたびに内部基準に従って一定量が差し引かれます。トークン残量が正の値のときに検索 API を使用できます。<br>
検索時に差し引かれるトークン数は、検索期間および容量、クエリーの複雑さによって異なり、トークンは時間の経過とともに自動的に補充されます。<br>

![lncs-api-01-20230925](https://static.toastoven.net/prod_logncrash/lncs-api-01-20230925.png)

### 基本情報
```
API Endpoint: https://api-lncs-search.gov-nhncloudservice.com
```
```
検索できるのは直近 90 日以内のログのみで、開始時刻と終了時刻の範囲は 31 日を超えることはできません。
```

### Search API
Luceneクエリーを使用して、指定した時間範囲のログを照会します。検索結果（totalItems）に制限はありませんが、ページングで照会できる範囲は最大 100,000 件（`pageNumber × pageSize ≤ 100,000`）までです。それ以上のログを照会するには、Search API（Cursor ページネーション）または Scroll API を使用してください。
```
POST /api/v2/search/{appkey}

Content-Type: application/json
```

#### リクエストパラメーター
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明             | 必須 |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | プロジェクト SecretKey | O |

#### リクエスト本文
| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Luceneクエリー | O |  |
| from | String | 開始時間 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| to | String | 終了時間 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| pageNumber | Number | ページ番号 |  | デフォルト値 0 |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | 並び替え基準 |  | フィールドごとの昇順（ASC）および降順（DESC）設定 |

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
| totalItems | Body | Number | ログ件数 |
| pageNumber | Body | Number | ページ番号 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログ一覧 |

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


### Search API（Cursor ページネーション）
Search API と同じエンドポイントで URL クエリーパラメーター `?cursor` を指定してオプトイン（opt-in）すると、cursor（search_after）ベースのページネーションを使用できます。深いページに移動しても `pageNumber × pageSize` の result window の制限（通常の Search API の 100,000 件）の影響を受けず、順次次のページを照会できます。

```
POST /api/v2/search/{appkey}?cursor

Content-Type: application/json
```

> - URL クエリーパラメーター `?cursor`、`?cursor=true` を指定すると cursor ページネーションが有効になります。オプトインがない場合は既存の Search API の動作がそのまま維持されます。
> - cursor オプトイン時には `pageNumber` を同時に送ることはできません（同時指定時は 400 レスポンス）。最初のページリクエスト時には `cursor` を空にし、以降のページでは直前のレスポンスの `nextCursor` の値をそのまま次のリクエストの `cursor` フィールドに渡します。
> - `cursor` の値はサーバー内部の並び替え状態をエンコードした opaque 文字列です。クライアントで解析・変形しないでください。
> - 1 回の呼び出しで受け取れるページサイズの制限（`pageSize` 最大値 100）は通常の Search API と同様に適用されます。
> - 最後のページに到達すると、レスポンス本文に `nextCursor` フィールドは含まれません。

#### リクエストパラメーター
| 名前 | 位置 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- | --- |
| appkey | Path | String | プロジェクトアプリキー | O |
| cursor | Query | - | cursor ベースのページネーションのオプトインフラグ。`?cursor`、`?cursor=true` 指定時に有効化 | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明             | 必須 |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | プロジェクト SecretKey | O |

#### リクエスト本文
| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Luceneクエリー | O |  |
| from | String | 開始時間 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| to | String | 終了時間 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | 並び替え基準 |  | フィールドごとの昇順（ASC）および降順（DESC）設定 |
| cursor | String | 次のページ照会用カーソル |  | 最初のページでは省略。以降のページでは直前のレスポンスの `nextCursor` の値をそのまま渡す。`pageNumber` との同時使用不可（400） |

<details>
<summary>例</summary>

最初のページリクエスト（`cursor` 未指定）:

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
| totalItems | Body | Number | ログ件数 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログ一覧 |
| nextCursor | Body | String | 次のページ照会用カーソル。次の結果が存在する場合のみ含まれ、最後のページには含まれない |

<details>
<summary>例</summary>

次のページが存在する場合（レスポンスに `nextCursor` を含む）:

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

最後のページの場合（レスポンスに `nextCursor` を含まない）:

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
Luceneクエリーを使用して、指定した時間範囲のログをページ指定なしにすべて照会します。Scroll Continue API と組み合わせて使用することで、複数回に分けて照会できます。
```
POST /api/v2/search/scroll/{appkey}

Content-Type: application/json
```

#### リクエストパラメーター
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明             | 必須 |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | プロジェクト SecretKey | O |

#### リクエスト本文
| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Luceneクエリー | O |  |
| from | String | 開始時間 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| to | String | 終了時間 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | 並び替え基準 |  | フィールドごとの昇順（ASC）および降順（DESC）設定 |

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
| totalItems | Body | Number | ログ件数 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログ一覧 |

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
Scroll Start API または直前に呼び出した Scroll Continue API から取得した Scroll Key を指定して、ログの照会を継続します。<br>
Scroll Key は 1 分間有効です。
```
POST /api/v2/search/scroll/{appkey}/{scrollKey}

Content-Type: application/json
```

#### リクエストパラメーター
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |
| scrollKey | String | Scroll Key | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明             | 必須 |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | プロジェクト SecretKey | O |

#### リクエスト本文
Scroll Continue API はリクエスト本文を必要としません。

#### レスポンス
| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | ログ件数 |
| data | Body | List | ログ一覧 |

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

#### リクエストパラメーター
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明             | 必須 |
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

保存されたログを Lucene クエリーを使用して検索できます。また、クラッシュ分析用の Symbol ファイルのアップロード/取得/削除機能を提供します。<br>
ログ検索 API は使用パターンに応じて、1 時間あたりにリクエストできる量を制限します。検索に使用できるリソースはトークンで表され、検索 API を呼び出すたびに内部基準に従って一定量が差し引かれます。トークン残量が正の値のとき、検索 API を使用できます。<br>
検索時に差し引かれるトークン数は、検索期間および容量、クエリーの複雑さによって異なります。トークンは時間の経過とともに自動的に補充されます。<br>

### 認証

API の呼び出しおよび認証の方法として、User Access Key トークンをサポートしています。<br>
トークンの発行方法については、以下のリンクを参照してください。

[User Access Key Token](https://docs.gov-nhncloud.com/ko/nhncloud/ko/public-api/user-access-key-token/)

#### API リクエストの HTTP ヘッダー例
```
X-NHN-Authorization: Bearer {Access Token}
```

### Search API
Lucene クエリーを使用して、指定した時間範囲のログを取得します。検索結果（totalItems）に上限はありませんが、ページングで取得できる範囲は最大 100,000 件（`pageNumber × pageSize ≤ 100,000`）までです。それ以上のログを取得するには、Cursor Search API または Scroll API を使用してください。
```
POST /v3/{appkey}/logs/search

Content-Type: application/json
```

#### リクエストパラメーター
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式の User Access Key トークン | O |

#### リクエスト本文
| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Lucene クエリー | O |  |
| from | String | 開始時刻 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| to | String | 終了時刻 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| pageNumber | Number | ページ番号 |  | デフォルト値 0 |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | 並び替え基準 |  | フィールドごとの昇順（ASC）および降順（DESC）設定 |

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
| totalItems | Body | Number | ログ件数 |
| pageNumber | Body | Number | ページ番号 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログ一覧 |

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
cursor（opaque）ベースのページネーションでログを検索します。<br>
深いページに移動しても `pageNumber × pageSize` の result window の制限に影響されることなく、順次取得できます。

- 最初のページをリクエストする際は、body の `cursor` を省略します。
- 次のページをリクエストする際は、直前のレスポンスの `nextCursor` 値を body の `cursor` フィールドにそのまま渡します。
- 最後のページに到達すると、レスポンス body に `nextCursor` は含まれません。
- `cursor` 値はバックエンド内部の並び替え状態をエンコードした opaque 文字列です。クライアント側でパース・変形しないでください。
- `pageNumber` は使用しません。body に含めると 400 レスポンスが返されます。

```
POST /v3/{appkey}/logs/cursor

Content-Type: application/json
```

#### リクエストパラメーター
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式の User Access Key トークン | O |

#### リクエスト本文
| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Lucene クエリー | O |  |
| from | String | 開始時刻 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| to | String | 終了時刻 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | 並び替え基準 |  | フィールドごとの昇順（ASC）および降順（DESC）設定 |
| cursor | String | 前回のレスポンスの `nextCursor` 値 |  | 最初のページのリクエスト時は省略 |

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
| totalItems | Body | Number | ログ件数 |
| pageNumber | Body | Number | ページ番号（cursor モードでは常に `0` 固定、意味なし） |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログ一覧 |
| nextCursor | Body | String | 次のページ取得用 opaque cursor（最後のページには含まれない） |

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
Lucene クエリーを使用して、指定した時間範囲のログをページ指定なしですべて取得します。Scroll Continue API と組み合わせて使用することで、複数回にわたって取得できます。
```
POST /v3/{appkey}/logs/scroll

Content-Type: application/json
```

#### リクエストパラメーター
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式の User Access Key トークン | O |

#### リクエスト本文
| 名前 | 形式 | 説明 | 必須 | 備考 |
| --- | --- | --- | --- | --- |
| query | String | Lucene クエリー | O |  |
| from | String | 開始時刻 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| to | String | 終了時刻 | O | ISO8601 形式の日付（YYYY-MM-DDThh:mm:ss.sTZD） |
| pageSize | Number | ページサイズ |  | デフォルト値 10、最大値 100 |
| sort | Object | 並び替え基準 |  | フィールドごとの昇順（ASC）および降順（DESC）設定 |

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
| totalItems | Body | Number | ログ件数 |
| pageSize | Body | Number | ページサイズ |
| data | Body | List | ログ一覧 |

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
Scroll Start API または直前に呼び出した Scroll Continue API から取得した Scroll Key を指定して、ログの取得を継続します。<br>
Scroll Key は 1 分間有効です。
```
POST /v3/{appkey}/logs/scroll/{scrollKey}

Content-Type: application/json
```

#### リクエストパラメーター
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |
| scrollKey | String | Scroll Key | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式の User Access Key トークン | O |

#### リクエスト本文
Scroll Continue API はリクエスト本文を必要としません。

#### レスポンス
| 名前 | 種類 | 形式 | 説明 |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | ログ件数 |
| data | Body | List | ログ一覧 |

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
使用可能なトークン数を取得します。
```
GET /v3/{appkey}/logs/available-token
```

#### リクエストパラメーター
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| appkey | String | プロジェクトアプリキー | O |

#### リクエストヘッダー
| 名前 | 形式 | 説明 | 必須 |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | `Bearer {Access Token}` 形式の User Access Key トークン | O |

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