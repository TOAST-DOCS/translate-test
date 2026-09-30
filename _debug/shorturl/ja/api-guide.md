<!-- pre-align:aligned sig=7351159b01ed -->

<a id="application-service-shorturl-api-guide"></a>
## Application Service > ShortURL > APIガイド { #application-service-shorturl-api-guide }

<a id="basic-information"></a>
### 基本情報 { #basic-information }
```http
API Endpoint: https://api-shorturl.nhncloudservice.com
```

<a id="shortened-url"></a>
## 短縮URL { #shortened-url }

<a id="create"></a>
### 1. 作成 { #create }
- 短縮URLを作成します。

[URL]
```http
POST /open-api/v1.0/appkeys/{appkey}/urls
Content-Type: application/json
```

<a id="create-request"></a>
#### リクエスト

[Path Variables]
| 名前 | タイプ | 必須かどうか | 説明 |
|---|---|---|---|
| appKey | String | O | サービスAppkey(**サービス管理**タブで確認可能) |

[Request Body]
| 名前 |	タイプ | 必須かどうか | 説明 |
|---|---|---|---|
| url | String | O | 元のURL |
| domain | String | X | 短縮URLに使用するドメイン(ない場合はnh.nuで作成) |
| backHalf | String | X | 短縮URL ID(https://nh.nu/exampleではexampleを指す。ない場合はランダムに作成) |
| description | String | X | 短縮URLの説明 |
| campaigns | List<String> | X | 所属するキャンペーンIDリスト |
| startDateTime | String | X | shortUrl使用開始日時 |
| endDateTime | String | X | shortUrl使用終了日時 |

* **startDateTime**および**endDateTime**を追加する時、**DateTimeFormatter.ISO_OFFSET_DATE_TIME**フォーマットを使用してください。
* **startDateTime**を別途指定しない場合は、現在時点に設定され、**endDateTime**を別途指定しない場合は**startDateTime**の3か月後に設定されます。
```json
{
   "url": "https://nhn.com",
   "domain": "nh.nu",
   "campaigns": [0,1],
   "backHalf": "example",
   "description": "test",
   "startDateTime" : "2022-11-10T02:58Z",
   "endDateTime": "2100-02-10T02:58Z"
}
```

<a id="create-response"></a>
#### レスポンス
```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "body": {
        "shortUrl": "http://nh.nu/example",
        "originUrl": "https://nhn.com",
        "status": "ACTIVE",
        "backHalfType": "CUSTOM",
        "description": "test",
        "startDateTime" : "2022-11-10T02:58Z",
        "endDateTime": "2100-02-10T02:58Z"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| header.isSuccessful | Boolean | 成否 |
| header.resultCode | Integer | 結果コード |
| header.resultMessage | String | 失敗メッセージ |
| body.shortUrl | String | 短縮されたURL |
| body.originUrl | String | 元のURL |
| body.status | String | 短縮URLの状態 |
| body.backHalfType | String | 短縮URLの作成方式 |
| body.description | String | 短縮URLの説明 |
| body.startDateTime | String | 短縮URLの使用開始日時 |
| body.endDateTime | String | 短縮URLの使用終了日時 |

* 作成された短縮URLを介して原本URLにアクセスする場合、原本URLをASCII(7)文字列に変更してLocationヘッダに追加します。
* この時、+ 文字はエンコードされずそのまま使われます。
  * たとえば、`https://nhn.com?query=안+녕`は`https://nhn.com?query=%EC%95%88+%EB%85%95`に変換され`+`文字を`%2B`にエンコードしません。

<a id="search"></a>
### 2. 検索 { #search }
- 短縮URLを検索します。

[URL]
```http
POST /open-api/v1.0/appkeys/{appkey}/domains/{domain}/urls/{backHalf}
Content-Type: application/json
```

<a id="search-request"></a>
#### リクエスト

[Path Variables]
| 名前 |	タイプ | 必須かどうか | 説明 |
|---|---|---|---|
| appKey | String | O | サービスAppkey(**サービス管理**タブで確認可能) |
| domain | String | O | ドメイン名 |
| backHalf | String | O | 短縮URL path ID |


<a id="search-response"></a>
#### レスポンス
```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "body": {
        "shortUrl": "http://nh.nu/a",
        "originUrl": "https://nhn.com",
        "status": "ACTIVE",
        "backHalfType": "AUTO",
        "description": "test",
        "startAt": "2021-03-26T03:35+0000",
        "endAt": "9999-12-31T00:00+0000"
    }
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| header.isSuccessful | Boolean | 成否 |
| header.resultCode | Integer | 結果コード |
| header.resultMessage | String | 失敗メッセージ |
| body.shortUrl | String | 短縮されたURL |
| body.originUrl | String | 元のURL |
| body.status | String | 短縮URLの状態 |
| body.backHalfType | String | 短縮URLの作成方式 |
| body.description | String | 短縮URLの説明 |
| body.startDateTime | String | 短縮URLの使用開始日時 |
| body.endDateTime | String | 短縮URLの使用終了日時 |



<a id="search-for-a-qr-code"></a>
### 3. QRコード検索 { #search-for-a-qr-code }
- 短縮URLを作成します。

[URL]
```http
POST /domains/{domain}/urls/{backHalf}/qrcode
Content-Type: image/png
```

<a id="search-for-a-qr-code-request"></a>
#### リクエスト

[Path Variables]
| 名前 | タイプ | 必須かどうか | 説明 |
|---|---|---|---|
| appKey | String | O | サービスAppkey(**サービス管理**タブで確認可能) |
| domain | String | O | ドメイン名 |
| backHalf | String | O | 短縮URL path ID |

<a id="search-for-a-qr-code-response"></a>
#### レスポンス
```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "body": "iVBORw0KGgoAAAANSUhEUgAAAIIAAACCAQAAAACieC1QAAAA+0lEQVR4Xu3UsZHEIAwFUO0QkO024BnaIKMlbwNnuwHTkjO3wYwasDMCBp18wbHrxFJ6t4rMCzTigwE61QIf+ZOSAGizNILRCFIuj0yRPzQyeqoeZ9AKVjB6ScN66nMtlGmD0y4uhfPB2eN7Ypdy1JSPpUbSsHTPTNXqBEL6CtCDU8kdMC4urm0XAqGJuA+N9jcfiZS7L73FqaUqkfRcu4HMTk4jPHDpvdvbzCKpgcd2fIgq2Xx342w9aeSnlcWqk+OOcThzS1UifJ95aWpoO5UI/6ezB3h5E2TCb0J5vKQqExoD7rnNLBHK6ZaRUSNHPnExcVXJW33kX8g3k5xLHpTtgoMAAAAASUVORK5CYII="
}
```

| 名前 | タイプ | 説明 |
|---|---|---|
| header.isSuccessful | Boolean | 成否 |
| header.resultCode | Integer | 失敗コード(0は正常) |
| header.resultMessage | String | 失敗メッセージ |
| body | String | Base64でエンコードされたPNGイメージ |
