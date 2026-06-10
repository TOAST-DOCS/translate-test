## Webhook

When specific events occur within the SMS service, a POST request is generated to the URL defined in the webhook settings.<br>
This is the API documentation for the generated POST request.

## Webhook Delivery

[URL]

| Http method | URI               |
|-------------|-------------------|
| POST        | Target URL defined in webhook settings |

[Header]

| Value                     | Type    | Description             |
|---------------------------|---------|----------------|
| X-Toast-Webhook-Signature | String | Signature entered during webhook configuration |

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

| Value           | Type      | Description                                                                                                                                                                                |
|-----------------|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| hooksId         | String    | Unique ID generated each time a POST request is made to the URL defined in webhook settings                                                                                                                                       |
| webhookConfigId | String    | Webhook configuration ID                                                                                                                                                                          |
| productName     | String    | Name of the service where the webhook event occurred                                                                                                                                                                  |
| appKey          | String    | App key of the service where the webhook event occurred                                                                                                                                                                |
| event           | String    | Webhook event name<br>* UNSUBSCRIBE: Promotional message recipient number registration<br>* MESSAGE_RESULT_UPDATE: Message delivery result code update<br>* CONVERSION_BLOCK: Blocked country occurrence due to conversion rate<br>* INTERNATIONAL_DELIVERY_RECEIPT: International delivery DLR update |
| hooks           | List<Map> | Data when webhook event occurs<br>* For detailed information, see [Event Type-Specific hooks Definition](./webhook/#hooks).                                                                                                         |

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

## Event Type-Specific hooks Definition
This is the hook data by event type when generating a POST request to the URL defined in webhook settings.
### Promotional Message Recipient Number Registration
| Value                   | Type   | Description                                            |
|-------------------------|--------|-----------------------------------------------|
| hooks[].hookId          | String | Unique ID generated when an event occurs in the service                     |
| hooks[].recipientNo     | String | Mobile phone number that opted out of receiving                                 |
| hooks[].unsubscribeNo   | String | 080 number registered with the opt-out service                         |
| hooks[].enterpriseName  | String | Company name registered with the opt-out service                            |
| hooks[].createdDateTime | String | Opt-out request date and time<br>* yyyy-MM-dd'T'HH:mm:ss.SSSXXX |

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

### Message Delivery Result Code Update
| Value                        | Type    | Description                                                                                                |
|------------------------------|---------|---------------------------------------------------------------------------------------------------|
| hooks[].hookId               | String  | Unique ID generated when an event occurs in the service                                                                         |
| hooks[].senderType           | String  | Delivery type                                                                                             |
| hooks[].requestId            | String  | Request ID                                                                                             |
| hooks[].recipientSeq         | Integer | Delivery detail ID (required for detailed search)                                                                              |
| hooks[].requestDate          | String  | Transmission date and time<br>* yyyy-MM-dd'T'HH:mm:ss                                                                  |
| hooks[].receiveDate          | String  | Reception date and time<br>* yyyy-MM-dd'T'HH:mm:ss                                                                  |
| hooks[].sendNo               | String  | Sender number                                                                                             |
| hooks[].recipientNo          | String  | Recipient number                                                                                             |
| hooks[].messageStatus        | String  | Message status <br>(COMPLETED: Delivery complete, FAILED: Delivery failed, CANCEL: Canceled, DUPLICATED: Duplicate delivery, FAILED_AD: Failed (advertising restriction)) |
| hooks[].recipientGroupingKey | String  | Recipient group key                                                                                          |
| hooks[].senderGroupingKey    | String  | Sender group key                                                                                          |
| hooks[].resultCode           | String  | Result code                                                                                             |
| hooks[].messageCount         | Integer | Number of delivered messages                                                                                        |
| hooks[]._links.self.href     | String  | Message single search API link                                                                                  | 

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

### Conversion Rate-Based Delivery Blocked Country Occurrence
| Value                   | Type   | Description                                            |
|-------------------------|--------|-----------------------------------------------|
| hooks[].hookId          | String | Unique ID generated when an event occurs in the service                     |
| hooks[].countryCode     | String | Country code                                         |
| hooks[].blockedDateTime | String | Blocked country occurrence date and time<br>* yyyy-MM-dd'T'HH:mm:ss.SSSXXX |

```json
"hooks": [
  {
    "hookId": "20240429205809GcSUXthVA00",
    "countryCode": "1",
    "blockedDateTime": "2024-05-28T09:00:00.000+09:00"
  }
]
```

### International Delivery DLR Update
| Value                | Type    | Description                                                                            |
|----------------------|---------|-------------------------------------------------------------------------------|
| hooks[].hookId       | String  | Unique ID generated when an event occurs in the service                                                     |
| hooks[].requestId    | String  | Request ID                                                                         |
| hooks[].recipientSeq | Integer | Delivery detail ID (required for detailed search)                                                          |
| hooks[].dlrStatus    | String  | DLR status<br>(ACCEPTED, DELIVERED, BUFFERED, EXPIRED, FAILED, REJECTED, UNKNOWN) |
| hooks[].networkCode  | String  | DLR network code                                                                   |
| hooks[].errorCode    | String  | DLR error code                                                                     |

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