## Game > Launching > API 가이드

Console에서 Launching 서비스를 활성화한 후, 모바일 앱에 필요한 Launching 정보를 설정하면 다음과 같은 데이터를 조회할 수 있습니다.

## API 공통 정보

### 요청

* API를 호출하려면 Launching 서비스의 AppKey가 필요합니다.
* AppKey는 Console 메뉴 상단의 **URL & AppKey**에서 확인할 수 있습니다.

### 응답

* 모든 응답 본문에는 다음과 같은 header를 포함합니다. 자세한 응답 결과는 오류 코드를 참고합니다.

[성공 응답 본문]
```json
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    }
}
```

[실패 응답 본문]
```json
{
    "header": {
        "isSuccessful": false,
        "resultCode": 90003,
        "resultMessage": "Failed to verify appkey. 'EyJ6IEGKv1dpDVCHc'"
    }
}
```


## Launching 데이터 조회

Console을 사용하여 설정한 Launching 정보를 조회할 수 있는 방법입니다.

[Method, URI]

```
GET https://api-lnc.cloud.toast.com/launching/v3.0/appkeys/{appKey}/configurations
```

[Path Variable]

| Name     | Type    | Value                   |
| ------ | ------ | -------------------- |
| appkey | String | Launching 서비스 AppKey |

[Request Parameter]

| Name     | Type    | Required | Value | Note |
| ------ | ------ | --- |-------------------- | --- |
| subKey | String | Optional | 서브 키 | "launching."으로 시작 |

* subKey를 통해 Launching 정보에서 일부 데이터만 가져올 수 있습니다.
    * subKey는 "launching."으로 시작해야 합니다.
* subKey 외의 모든 GET 파라미터는 일반 변수로 취급하여 로직 조건에 사용할 수 있습니다.

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
