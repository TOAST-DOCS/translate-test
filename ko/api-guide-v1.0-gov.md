## API v1.0 가이드
**Management > Certificate Manager > API v1.0 가이드**

Certificate Manager에서는 인증서 목록 조회, 다운로드를 위한 API를 제공합니다. 클라이언트는 콘솔에서 인증서와 인증서 파일을 등록한 후 API를 통해 데이터를 사용할 수 있습니다.

## Certificate Manager API 공통 정보

### API 엔드포인트

| 리전 | 엔드포인트 |
|---|---|
| Global | https://certmanager.api.gov-nhncloudservice.com |

### 인증 및 권한

Certificate Manager API v1.0을 사용하려면 Appkey가 필요합니다.

Appkey는 NHN Cloud의 각 서비스별로 발급되는 고유 인증 키입니다. Appkey 확인 및 사용에 대한 자세한 내용은 [Appkey](/nhncloud/ko/public-api/appkey)를 참고하세요.

### 제공하는 API 종류
| 메서드 | URI | 설명 |
| ------ | --- | --- |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates | 인증서 목록을 조회합니다. |
| GET | /certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files | 등록된 인증서 파일을 다운로드합니다. |

#### API 요청의 경로 변수

| 값 | 타입 | 설명 |
| --- | --- | --- |
| appKey | String | 사용할 데이터를 저장하고 있는 NHN Cloud 프로젝트의 앱키 |
| certificateName | String | 사용할 데이터(인증서)의 이름 |

#### API 응답의 데이터 공통 헤더

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": {

    }
}
```

| 값 | 타입 | 설명 |
| --- | --- | --- |
| resultCode | Number | API 호출 결과 코드값 |
| resultMessage | String | API 호출 결과 메시지 |
| isSuccessful | Boolean | API 호출 성공 여부 |

## 인증서 API

### 인증서 목록 조회

Certificate Manager에 등록한 인증서 목록을 조회할 때 사용합니다.

#### 요청

```
GET https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| 값 | 타입 | 설명 | 입력 가능 |
| --- | --- | --- | --- |
| pageSize | Number | 페이지 크기 | 10(default) |
| pageNum | Number | 페이지 번호 | 1(default) |
| all | Boolean | 전체 조회 여부 | true, false(default) |
| status | String | 인증서 상태 | ALL, EXPIRED, UNEXPIRED(default) |

※ all, status의 값은 대소문자 구분 없이 사용할 수 있습니다.

#### 응답

[Response Header]

```
Content-Type:application/json
```

[Response Body]

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": {
        "totalCount": 1,
        "totalPage": 1,
        "currentPage": 1,
        "pageSize": 10,
        "data": [
            {
                "certificateName": "test.nhn.com",
                "authority": "NHN",
                "signatureAlgorithm": "SHA256withRSA",
                "fileCreationDate": "2020-03-02",
                "expirationDate": "2021-03-25"
            }
        ]
    }
}
```

| 값 | 타입 | 설명|
| --- | --- |---|
| totalCount | Number | 전체 인증서 수 |
| totalPage | Number | 전체 페이지 수 |
| currentPage | Number | 현재 페이지 |
| pageSize | Number | 페이지 크기 |
| certificateName | String | 인증서 이름 |
| authority | String | 인증 기관 |
| signatureAlgorithm | String | 서명 방식 |
| fileCreationDate | String | 인증서 파일 생성일 |
| expirationDate | String | 인증서 파일 만료일 |

### 인증서 파일 다운로드

Certificate Manager에 등록한 인증서 파일을 다운로드할 때 사용합니다.

#### 요청

```
GET https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files
```

#### 성공 응답

[Response Header]

```
Content-Disposition:attachment; filename="{파일명}"
Content-Type:application/octet-stream
```

[Response Body]

```
-----BEGIN CERTIFICATE-----
...
-----END CERTIFICATE-----
...
-----BEGIN RSA PRIVATE KEY-----
...
-----END RSA PRIVATE KEY-----
```

#### 실패 응답
[Response Header]
```
Content-Type:application/json
```
[Response Body]

```
{
    "header": {
        "resultCode": 52000,
        "resultMessage": "Certificate name does not exist.",
        "isSuccessful": false
    },
    "body": {}
}
```

#### Command Line Interface(CLI) 사용 시

인증서 파일 다운로드 API는 `curl` 명령어를 사용해 요청할 수 있습니다.

```bash
#파일에 쓰기
curl 'https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#파일명 지정
curl -o cert.pem 'https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'

#업로드한 파일명 유지
curl -OJ 'https://certmanager.api.gov-nhncloudservice.com/certmanager/v1.0/appkeys/{appKey}/certificates/{certificateName}/files'
```
* 기타 curl 명령어 사용법은 아래 가이드를 참고하십시오.
  * curl command guide : [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

## 응답 코드

| isSuccessful | resultCode | resultMessage | 설명 |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | 성공 |
| false | 52000 | Certificate name does not exist. | 요청한 인증서 이름이 존재하지 않습니다. |
| false | 52001 | Certificate file does not exist. | 요청한 인증서 파일이 존재하지 않습니다. |
| false | 52002 | There are more than one certificate file. | 요청한 인증서에 등록된 파일이 두 개 이상입니다. |
| false | 52003 | The certificate file is not a pem file. | 요청한 인증서 파일이 pem 파일이 아닙니다. |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | 요청한 인증서 이름과 인증서 파일에 등록된 이름이 다릅니다. |
| false | 52005 | Certificate file has expired | 요청한 인증서 파일이 만료된 파일입니다. |
| false | 52006 | The certificate has an invalid certificate authority name. | 요청한 인증서 파일의 인증 기관 정보가 유효하지 않습니다. |
| false | 52007 | Requested certificate file should be one. | 동시에 하나의 인증서 파일만 업로드 가능합니다. |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | 업로드 가능한 최대 파일 크기는 512KB입니다. |
