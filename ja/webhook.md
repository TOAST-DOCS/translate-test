## ウェブフック

SMS サービス内で特定のイベントが発生すると、ウェブフック設定で定義された URL に POST リクエストを生成します。<br>
生成された POST リクエストに関する API ドキュメントです。

## ウェブフック送信

[URL]

| Http method | URI               |
|-------------|-------------------|
| POST        | ウェブフック設定で定義したターゲット URL |

[Header]

| 値                         | タイプ      | 説明             |
|---------------------------|---------|----------------|
| X-Toast-Webhook-Signature | 	String | ウェブフック設定時に入力した署名 |

[Request body]

```json
{
  "hooksId": "202007271010101010sadasdavas",
  "webhookConfigId": "String",
  "productName": "SMS",
  "appKey": "akb3dukdmdjsdSvgk",
  "event": "UNSUBSCRIBE",
  "hooks": [
    {
      ...
    }
  ]
}
```

| 値               | タイプ        | 説明                                                                                                                                                                                |
|-----------------|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| hooksId         | String    | ウェブフック設定で定義された URL に POST リクエストを行うたびに一意に生成される ID                                                                                                                                       |
| webhookConfigId | String    | ウェブフック設定 ID                                                                                                                                                                          |
| productName     | String    | ウェブフックイベントが発生したサービス名                                                                                                                                                                  |
| appKey          | String    | ウェブフックイベントが発生したサービスアプリケーションキー                                                                                                                                                                |
| event           | String    | ウェブフックイベント名<br>* UNSUBSCRIBE: 広告メッセージ受信番号登録<br>* MESSAGE_RESULT_UPDATE: メッセージ送信結果コード更新<br>* CONVERSION_BLOCK: コンバージョン率による遮断国の発生<br>* INTERNATIONAL_DELIVERY_RECEIPT: 国際送信 DLR 更新 |
| hooks           | List<Map> | ウェブフックイベント発生時のデータ<br>* 詳細については「[イベントタイプ別 hooks 定義](./webhook/#hooks)」を参照してください。                                                                                                         |

#### cURL

```
curl -X POST \
    '{TargetUrl}' \
    -H 'Content-Type: application/json;charset=UTF-8' \
    -H 'X-Toast-Webhook-Signature: application/json;charset=UTF-8' \
    -d '{
        "hooksId": "202007271010101010sadasdavas",
        "webhookConfigId": "String",
        "productName": "Sms",
        "appKey": "akb3dukdmdjsdSvgk",
        "event": "UNSUBSCRIBE",
        "hooks": [
            {
                ...
            }
        ]
    }
'
```

## イベントタイプ別 hooks 定義
ウェブフック設定で定義された URL に POST リクエストを生成する際のイベントタイプ別フック(hook)データです。
### 広告メッセージ受信番号登録
| 値                       | タイプ     | 説明                                            |
|-------------------------|--------|-----------------------------------------------|
| hooks[].hookId          | String | サービスでイベント発生時に生成される一意の ID                     |
| hooks[].recipientNo     | String | 受信拒否された携帯電話番号                                 |
| hooks[].unsubscribeNo   | String | 受信拒否サービスに登録された 080 番号                         |
| hooks[].enterpriseName  | String | 受信拒否サービスに登録された会社名                            |
| hooks[].createdDateTime | String | 受信拒否リクエスト日時<br>* yyyy-MM-dd'T'HH:mm:ss.SSSXXX |

```json
"hooks": [
  {
    "hookId": "202007271010101010sadasdavas",
    "recipientNo": "01012341234",
    "unsubscribeNo": "08012341234",
    "enterpriseName": "NHN Cloud",
    "createdDateTime": "2020-09-09T11:25:10.000+09:00"    
  }
]
```

### メッセージ送信結果コード更新
| 値                            | タイプ      | 説明                                                                                                |
|------------------------------|---------|---------------------------------------------------------------------------------------------------|
| hooks[].hookId               | String  | サービスでイベント発生時に生成される一意の ID                                                                         |
| hooks[].senderType           | String  | 送信タイプ                                                                                             |
| hooks[].requestId            | String  | リクエスト ID                                                                                             |
| hooks[].recipientSeq         | Integer | 送信詳細 ID（詳細検索時必須）                                                                              |
| hooks[].requestDate          | String  | 発信日時<br>* yyyy-MM-dd'T'HH:mm:ss                                                                  |
| hooks[].receiveDate          | String  | 受信日時<br>* yyyy-MM-dd'T'HH:mm:ss                                                                  |
| hooks[].sendNo               | String  | 発信番号                                                                                             |
| hooks[].recipientNo          | String  | 受信番号                                                                                             |
| hooks[].messageStatus        | String  | メッセージステータス <br>(COMPLETED: 送信完了, FAILED: 送信失敗, CANCEL: キャンセル, DUPLICATED: 重複送信, FAILED_AD: 失敗（広告制限）) |
| hooks[].recipientGroupingKey | String  | 受信者グループキー                                                                                          |
| hooks[].senderGroupingKey    | String  | 発信者グループキー                                                                                          |
| hooks[].resultCode           | String  | 結果コード                                                                                             |
| hooks[].messageCount         | Integer | 送信されたメッセージ件数                                                                                        |
| hooks[]._links.self.href     | String  | メッセージ単一検索 API リンク                                                                                  | 

```json
"hooks": [
  {
    "hookId": "20240429205809GcSUXthVA00",
    "senderType": "NORMAL_SMS",
    "requestId": "20240429205802y0Tl7Gbz0e0",
    "recipientSeq": 1,
    "requestDate": "2024-04-29T20:58:02",
    "receiveDate": "2024-04-29T20:58:04",
    "sendNo": "15446859",
    "recipientNo": "01012341234",
    "messageStatus": "COMPLETED",
    "recipientGropuingKey": "RecipientGroupingKey",
    "senderGroupingKey": "SenderGroupingKey",
    "resultCode": "1000",
    "messageCount": 1,
    "_link": {
      "self": {
        "href": "https://sms.api.nhncloudservice.com/sms/v2.4/appKeys/{appKey}/sender/sms/20240429205802y0Tl7Gbz0e0?recipientSeq=1"
      }
    },
  }
]
```

### コンバージョン率ベース送信遮断国発生
| 値                       | タイプ     | 説明                                            |
|-------------------------|--------|-----------------------------------------------|
| hooks[].hookId          | String | サービスでイベント発生時に生成される一意の ID                     |
| hooks[].countryCode     | String | 国コード                                         |
| hooks[].blockedDateTime | String | 遮断国発生日時<br>* yyyy-MM-dd'T'HH:mm:ss.SSSXXX |

```json
"hooks": [
  {
    "hookId": "20240429205809GcSUXthVA00",
    "countryCode": "1",
    "blockedDateTime": "2024-05-28T09:00:00.000+09:00"
  }
]
```

### 国際送信 DLR 更新
| 値                    | タイプ      | 説明                                                                            |
|----------------------|---------|-------------------------------------------------------------------------------|
| hooks[].hookId       | String  | サービスでイベント発生時に生成される一意の ID                                                     |
| hooks[].requestId    | String  | リクエスト ID                                                                         |
| hooks[].recipientSeq | Integer | 送信詳細 ID（詳細検索時必須）                                                          |
| hooks[].dlrStatus    | String  | DLR ステータス<br>(ACCEPTED, DELIVERED, BUFFERED, EXPIRED, FAILED, REJECTED, UNKNOWN) |
| hooks[].networkCode  | String  | DLR ネットワークコード                                                                   |
| hooks[].errorCode    | String  | DLR エラーコード                                                                     |

```json
"hooks": [
  {
    "hookId": "202409251600118GSDDYTwzX0",
    "requestId": "20240925160005UvxdDrJ4g20",
    "recipientSeq": 1,
    "dlrStatus": "ACCEPTED",
    "networkCode": "US-VIRTUAL-BANDWIDTH",
    "errorCode": "0"
  }
]
```