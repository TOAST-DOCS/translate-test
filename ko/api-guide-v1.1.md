<!-- pre-align:aligned sig=2c9270a88b89 -->

<a id="management-certificate-manager-api-v11-guide"></a>
## Management > Certificate Manager > API v1.1 가이드 { #management-certificate-manager-api-v11-guide }

Certificate Manager에서는 인증서 목록 조회와 다운로드 API를 제공합니다. 클라이언트는 콘솔에서 인증서와 인증서 파일을 등록한 후 API로 데이터를 사용할 수 있습니다.

<a id="common-certificate-manager-api-information"></a>
### Certificate Manager API 공통 정보 { #common-certificate-manager-api-information }
<a id="common-certificate-manager-api-information-api-endpoint"></a>
#### API 엔드포인트
```text
https://certmanager.api.nhncloudservice.com
```

<a id="common-certificate-manager-api-information-authentication-and-authorization"></a>
#### 인증 및 권한
Certificate Manager는 API 호출 시 인증/인가를 위해 User Access Key 인증을 사용합니다.
User Access Key는 NHN Cloud 계정 또는 IAM 계정을 기반으로 발급되는 인증 키로, Secret Access Key와 함께 사용하여 API 요청에 대한 인증 수단입니다.
User Access Key 사용에 대한 자세한 내용은 [User Access Key 인증](/nhncloud/ko/public-api/user-access-key)을 참고하세요.

Certificate Manager API는 역할 기반 접근 제어(RBAC)를 사용합니다.<br>
사용자는 API 사용을 위해 **Certificate Manager ADMIN 역할** 또는 **Certificate Manager VIEWER 역할**을 소유해야 합니다.

<a id="common-certificate-manager-api-information-supported-api-types"></a>
#### 제공하는 API 종류
| 메서드 | URI                                                                     | 설명 |
| ------ |-------------------------------------------------------------------------| --- |
| GET | /certmanager/v1.1/appkeys/{appKey}/certificates                         | 인증서 목록을 조회합니다. |
| GET | /certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files | 등록된 인증서 파일을 다운로드합니다. |

##### API 요청의 경로 변수

| 값 | 타입 | 설명 |
| --- | --- | --- |
| appKey | String | 사용할 데이터를 저장하고 있는 NHN Cloud 프로젝트의 앱키 |
| certificateName | String | 사용할 데이터(인증서)의 이름 |

##### API 응답의 데이터 공통 헤더

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
| resultCode | Number | API 호출 결과 코드 값 |
| resultMessage | String | API 호출 결과 메시지 |
| isSuccessful | Boolean | API 호출 성공 여부 |

<a id="list-certificates"></a>
### 인증서 목록 조회 { #list-certificates }

Certificate Manager에 등록한 인증서 목록을 조회할 때 사용합니다.

<a id="list-certificates-request"></a>
#### 요청

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| 값 | 타입 | 설명 | 입력 가능 |
| --- | --- | --- | --- |
| pageSize | Number | 페이지 크기 | 10(default) |
| pageNum | Number | 페이지 번호 | 1(default) |
| all | Boolean | 전체 조회 여부 | true, false(default) |
| status | String | 인증서 상태 | ALL, EXPIRED, UNEXPIRED(default) |

※ all, status의 값은 대소문자 구분 없이 사용할 수 있습니다.

<a id="list-certificates-response"></a>
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

| 값 | 타입 | 설명 |
| --- | --- | --- |
| totalCount | Number | 전체 인증서 수 |
| totalPage | Number | 전체 페이지 수 |
| currentPage | Number | 현재 페이지 |
| pageSize | Number | 페이지 크기 |
| certificateName | String | 인증서 이름 |
| authority | String | 인증 기관 |
| signatureAlgorithm | String | 서명 방식 |
| fileCreationDate | String | 인증서 파일 생성일 |
| expirationDate | String | 인증서 파일 만료일 |

<a id="download-certificate-file"></a>
### 인증서 파일 다운로드 { #download-certificate-file }

Certificate Manager에 등록한 인증서 파일을 다운로드할 때 사용합니다.

<a id="download-certificate-file-request"></a>
#### 요청

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files
```

<a id="download-certificate-file-success-response"></a>
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

<a id="download-certificate-file-failure-response"></a>
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

<a id="download-certificate-file-for-command-line-interface-cli"></a>
#### Command Line Interface(CLI) 사용 시

인증서 파일 다운로드 API는 `curl` 명령어를 사용해 요청할 수 있습니다.

```bash
#파일에 쓰기
curl -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
    -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}' \
    'https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#파일명 지정
curl -o cert.pem \
    -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
    -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}' \
    'https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files'

#업로드한 파일명 유지
curl -OJ \
    -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
    -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}' \
    'https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files'
```
* 기타 curl 명령어 사용법은 아래 가이드를 참고하세요.
  * curl command guide: [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

<a id="response-codes"></a>
### 응답 코드 { #response-codes }

| isSuccessful | resultCode | resultMessage | 설명 |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | 성공 |
| false | 52000 | Certificate name does not exist. | 요청한 인증서 이름이 없습니다. |
| false | 52001 | Certificate file does not exist. | 요청한 인증서 파일이 없습니다. |
| false | 52002 | There are more than one certificate file. | 요청한 인증서에 등록된 파일이 두 개 이상입니다. |
| false | 52003 | The certificate file is not a pem file. | 요청한 인증서 파일이 pem 파일이 아닙니다. |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | 요청한 인증서 이름과 인증서 파일에 등록된 이름이 다릅니다. |
| false | 52005 | Certificate file has expired | 요청한 인증서 파일이 만료되었습니다. |
| false | 52006 | The certificate has an invalid certificate authority name. | 요청한 인증서 파일의 인증 기관 정보가 유효하지 않습니다. |
| false | 52007 | Requested certificate file should be one. | 동시에 하나의 인증서 파일만 업로드 가능합니다. |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | 업로드 가능한 최대 파일 크기는 512KB입니다. |
