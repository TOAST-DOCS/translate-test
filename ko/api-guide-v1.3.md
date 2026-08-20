<!-- pre-align:aligned sig=1830bd25c1cb -->

<a id="management-certificate-manager-api-v13-guide"></a>
## Management > Certificate Manager > API v1.3 가이드 { #management-certificate-manager-api-v13-guide }

Certificate Manager에서는 인증서 목록 조회, 다운로드를 위한 API를 제공합니다. 클라이언트는 콘솔에서 인증서와 인증서 파일을 등록한 후 API를 통해 데이터를 사용할 수 있습니다.

<a id="certificatemanager-api-common-information"></a>
### CertificateManager API 공통 정보 { #certificatemanager-api-common-information }
<a id="certificatemanager-api-common-information-api-endpoint"></a>
#### API 엔드포인트
```text
https://certmanager.api.nhncloudservice.com
```
<a id="certificatemanager-api-common-information-authentication-and-authorization"></a>
#### 인증 및 권한
CertificateManager는 API 호출 시 인증/인가를 위해 User Access Key 토큰을 사용합니다.
User Access Key 토큰은 User Access Key를 기반으로 발급되는 Bearer 타입의 일시적 액세스 토큰입니다.
User Access Key 토큰 발급 및 사용에 대한 자세한 내용은 [User Access Key 토큰](/nhncloud/ko/public-api/user-access-key-token)을 참고하세요.

CertificateManager API는 역할 기반 접근 제어(RBAC)를 사용하고 있습니다.<br>
사용자는 API 사용을 위해 **CertificateManager ADMIN 역할** 또는 **CertificateManager VIEWER 역할** 소유해야합니다.

<a id="certificatemanager-api-common-information-provided-apis"></a>
#### 제공하는 API 종류
| 메서드 | URI                                                                     | 설명 |
| ------ |-------------------------------------------------------------------------| --- |
| GET | /certmanager/v1.3/appkeys/{appKey}/certificates                         | 인증서 목록을 조회합니다. |
| GET | /certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files | 등록된 인증서 파일을 인증서 이름으로 다운로드합니다. |
| GET | /certmanager/v1.3/appkeys/{appKey}/certificates/{certificateId}/certificate-files | 등록된 인증서 파일을 인증서 ID로 다운로드합니다. |

##### API 요청의 경로 변수

| 값 | 타입 | 설명 |
| --- | --- | --- |
| appKey | String | 사용할 데이터를 저장하고 있는 NHN Cloud 프로젝트의 앱키 |
| certificateName | String | 사용할 데이터(인증서) 이름 |
| certificateId | Number | 사용할 데이터(인증서) ID |

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
| resultCode | Number | API 호출 결과 코드값 |
| resultMessage | String | API 호출 결과 메시지 |
| isSuccessful | Boolean | API 호출 성공 여부 |

<a id="retrieve-a-certificate-list"></a>
### 인증서 목록 조회 { #retrieve-a-certificate-list }

Certificate Manager에 등록한 인증서 목록을 조회할 때 사용합니다.

<a id="retrieve-a-certificate-list-request"></a>
#### 요청

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| 값 | 타입 | 설명 | 입력 가능 |
| --- | --- | --- | --- |
| pageSize | Number | 페이지 크기 | 10(기본값) |
| pageNum | Number | 페이지 번호 | 1(기본값) |
| all | Boolean | 전체 조회 여부 | true, false(기본값) |
| status | String | 인증서 상태 | ALL, EXPIRED, UNEXPIRED(기본값) |

※ all, status의 값은 대소문자 구분 없이 사용할 수 있습니다.

<a id="retrieve-a-certificate-list-response"></a>
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
                "certificateId": 1,
                "certificateName": "nhncloudservice.com",
                "authority": "NHN",
                "domains": [
                  "nhncloudservice.com",
                  "*.nhncloudservice.com"
                ],
                "signatureAlgorithm": "SHA256withRSA",
                "fileCreationDate": "2025-03-02",
                "expirationDate": "2026-03-25"
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
| certificateId | Number | 인증서 ID |
| certificateName | String | 인증서 이름 |
| authority | String | 인증 기관 |
| signatureAlgorithm | String | 서명 방식 |
| fileCreationDate | String | 인증서 파일 생성일 |
| expirationDate | String | 인증서 파일 만료일 |

<a id="download-a-certificate-file-certificate-name"></a>
### 인증서 파일 다운로드(인증서 이름) { #download-a-certificate-file-certificate-name }

Certificate Manager에 등록한 인증서 파일을 인증서 이름으로 다운로드할 때 사용합니다.

<a id="download-a-certificate-file-certificate-name-request"></a>
#### 요청

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files
```

<a id="download-a-certificate-file-certificate-name-success-response"></a>
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

<a id="download-a-certificate-file-certificate-name-failure-response"></a>
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

<a id="download-a-certificate-file-certificate-name-using-the-command-line-interface-cli"></a>
#### Command Line Interface(CLI) 사용 시

인증서 파일 다운로드 API는 curl 명령어를 사용해 요청할 수 있습니다.

```bash
#파일에 쓰기
curl 'https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files' \
    -H "X-NHN-AUTHORIZATION: Bearer {발급 받은 토큰}" > cert.pem

#파일명 지정
curl -o cert.pem 'https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files' \
    -H "X-NHN-AUTHORIZATION: Bearer {발급 받은 토큰}"

#업로드한 파일명 유지
curl -OJ 'https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files' \
    -H "X-NHN-AUTHORIZATION: Bearer {발급 받은 토큰}"
```
* 기타 curl 명령어 사용법은 아래 가이드를 참고하세요.
  * curl command guide: [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

<a id="download-a-certificate-file-certificate-id"></a>
### 인증서 파일 다운로드(인증서 ID) { #download-a-certificate-file-certificate-id }

Certificate Manager에 등록한 인증서 파일을 인증서 ID로 다운로드할 때 사용합니다.
인증서 ID는 인증서 목록 조회 API 응답의 certificateId 값입니다.

<a id="download-a-certificate-file-certificate-id-request"></a>
#### 요청

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateId}/certificate-files
```

<a id="download-a-certificate-file-certificate-id-success-response"></a>
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

<a id="download-a-certificate-file-certificate-id-failure-response"></a>
#### 실패 응답
[Response Header]
```
Content-Type:application/json
```
[Response Body]

```
{
    "header": {
        "resultCode": 52009,
        "resultMessage": "Certificate id does not exist.",
        "isSuccessful": false
    },
    "body": {}
}
```

※ 실패 응답은 HTTP 상태 코드 404(Not Found)와 함께 반환됩니다.

<a id="response-code"></a>
### 응답 코드 { #response-code }

| isSuccessful | resultCode | resultMessage | 설명 |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | 성공 |
| false | 52000 | Certificate name does not exist. | 요청한 인증서 이름이 존재하지 않습니다. |
| false | 52001 | Certificate file does not exist. | 요청한 인증서 파일이 존재하지 않습니다. |
| false | 52002 | There are more than one certificate file. | 요청한 인증서에 등록된 파일이 두 개 이상입니다. |
| false | 52003 | The certificate file is not a pem file. | 요청한 인증서 파일이 PEM 형식 파일이 아닙니다. |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | 요청한 인증서 이름과 인증서 파일에 등록된 이름이 다릅니다. |
| false | 52005 | Certificate file has expired | 요청한 인증서 파일이 만료된 파일입니다. |
| false | 52006 | The certificate has an invalid certificate authority name. | 요청한 인증서 파일의 인증 기관 정보가 유효하지 않습니다. |
| false | 52007 | Requested certificate file should be one. | 동시에 하나의 인증서 파일만 업로드 가능합니다. |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | 업로드 가능한 최대 파일 크기는 512KB입니다. |
| false | 52009 | Certificate id does not exist. | 요청한 인증서 ID가 존재하지 않습니다. |
