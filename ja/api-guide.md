## Game > Launching > APIガイド

ConsoleでLaunchingサービスを有効にした後、モバイルアプリに必要なLaunching情報を設定すると、次のようなデータを照会できます。

## API共通情報

### リクエスト

* APIを呼び出すには、LaunchingサービスのAppKeyが必要です。
* AppKeyは、Consoleメニュー上部にある**URL & AppKey**で確認できます。

### レスポンス

* すべてのレスポンス本文には、次のようなheaderを含めます。詳細なレスポンス結果は、エラーコードを参照してください。

[成功レスポンス本文]
```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    }
}
```

[失敗レスポンス本文]
```json
{
    "header": {
        "isSuccessful": false,
        "resultCode": 90003,
        "resultMessage": "Failed to verify appkey. 'EyJ6IEGKv1dpDVCHc'"
    }
}
```


## Launchingデータ照会

Consoleを使用して設定したLaunching情報を照会する方法です。

[Method, URI]

```
GET https://api-lnc.cloud.toast.com/launching/v3.0/appkeys/{appKey}/configurations
```

[Path Variable]

| Name     | Type    | Value                   |
| ------ | ------ | -------------------- |
| appkey | String | LaunchingサービスAppKey |

[Request Parameter]

| Name     | Type    | Required | Value | Note |
| ------ | ------ | --- |-------------------- | --- |
| subKey | String | Optional | サブキー | "launching."で開始 |

* subKeyを通してLaunching情報から一部のデータのみを取得できます。
    * subKeyは"launching."で始まる必要があります。
* subKey以外のすべてのGETパラメータは一般変数として扱い、ロジック条件に使用できます。

---

[Request Sample - 00]

```
GET https://api-lnc.cloud.toast.com/launching/v3.0/appkeys/EyJ6IEGKv1pDVCHc/configurations
```

[Request Sample - 00 : Response]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    },
    "launching": {
        "server": {
            "cds": "",
            "ip": ""
        },
        "client": {
            "privacyUrl": "",
            "termsUrl": "",
            "eventUrl": "",
            "bannerUrl": "",
            "downloadUrl": "",
            "noticeUrl": "",
            "currentVersion": ""
        },
        "state": "",
        "maintenance": {
            "message": {
                "ko": "",
                "jp": "",
                "en": ""
            }
        }
    }
}
```

[Request Sample - 01]

```
GET https://api-lnc.cloud.toast.com/launching/v3.0/appkeys/EyJ6IEGKv1pDVCHc/configurations?subKey=launching.server
```

[Request Sample - 01 : Response]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    },
    "launching": {
        "cds": "",
        "ip": ""
    }
}
```
