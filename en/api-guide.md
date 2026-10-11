## Game > Launching > API Guide

Enable Launching Service on console and configure required launching information for a mobile app, and data as follows can be queried. 

## Common API Information 

### Request

* To call APIs, an Appkey of the launching service is required.   를
* You can find AppKey from **URL & Appkey** on top of the console menu. 

### Response 

* Each response body includes a header as below. For more response results, see Error Codes. 

[Successful Response Body]

```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    }
}
```

[Failed Response Body]

```json
{
    "header": {
        "isSuccessful": false,
        "resultCode": 90003,
        "resultMessage": "Failed to verify appkey. 'EyJ6IEGKv1dpDVCHc'"
    }
}
```


## Query Launching Data 

Querying configured launching data on a console is as follows:  

[Method, URI]

```
GET https://api-lnc.cloud.toast.com/launching/v3.0/appkeys/{appKey}/configurations
```

[Path Variable]

| Name     | Type    | Value                   |
| ------ | ------ | -------------------- |
| Appkey | String | Appkey for Launching Service |

[Request Parameter]

| Name     | Type    | Required | Value | Note |
| ------ | ------ | --- |-------------------- | --- |
| SubKey | String | Optional | Subkey | Start with "launching." |

* Only partial launching data can be imported with a subKey. 
    * The subKey must start with "launching.".
* All GET parameters, other than Subkey, are considered as general parameters and can be applied as part of the logic conditions.  

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
