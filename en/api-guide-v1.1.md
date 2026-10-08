<!-- pre-align:aligned sig=2c9270a88b89 -->

<a id="management-certificate-manager-api-v11-guide"></a>
## Management > Certificate Manager > API v1.1 Guide { #management-certificate-manager-api-v11-guide }

Certificate Manager provides APIs for viewing and downloading a list of certificates. Clients can register certificates and certificate files in the console and then use the data through APIs.

<a id="common-certificate-manager-api-information"></a>
### Common Certificate Manager API Information { #common-certificate-manager-api-information }
<a id="common-certificate-manager-api-information-api-endpoint"></a>
#### API EndPoint
```text
https://certmanager.api.nhncloudservice.com
```

<a id="common-certificate-manager-api-information-authentication-and-authorization"></a>
#### Authentication and Authorization
Certificate Manager uses User Access Key authentication for authentication and authorization when calling APIs.
User Access Key is an authentication key issued based on an NHN Cloud account or IAM account, and is used together with a Secret Access Key as an authentication method for API requests.
For more information on using User Access Key, refer to [User Access Key Authentication](/nhncloud/en/public-api/user-access-key).

Certificate Manager API uses role-based access control (RBAC).<br>
Users must have the **Certificate Manager ADMIN Role** or **Certificate Manager VIEWER Role** to use the API.

<a id="common-certificate-manager-api-information-supported-api-types"></a>
#### Supported API Types
| Method | URI                                                                     | Description |
| ------ |-------------------------------------------------------------------------| --- |
| GET | /certmanager/v1.1/appkeys/{appKey}/certificates                         | Retrieves a list of certificates. |
| GET | /certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files | Downloads a registered certificate file. |

##### Path Variables of API Request

| Value | Type | Description |
| --- | --- | --- |
| appKey | Token ID | Appkey of the NHN Cloud project where the data in need is stored |
| certificateName | Token ID | Name of the data (certificate) you want to use |

##### [Common Data Header of API Response]

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "success",
        "isSuccessful": true
    },
    "body": {
        ...
    }
}
```

| Value | Type | Description |
| --- | --- | --- |
| resultCode | Number | Result code value of API call |
| resultMessage | Token ID | Result message of API call |
| isSuccessful | Boolean | Whether API call is successful or not |

<a id="list-certificates"></a>
### List Certificates { #list-certificates }

Used to query the list of certificates registered with Certificate Manager.

<a id="list-certificates-request"></a>
#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| Value | Type | Description | Available input |
| --- | --- | --- | --- |
| pageSize | Number | Page size | 10(default) |
| pageNum | Number | Page number | 1(default) |
| all | Boolean | Retrieve all or not | true, false(default) |
| String | Token ID | Certificate status | ALL, EXPIRED, UNEXPIRED(default) |

※ The values for all and status are case insensitive.

<a id="list-certificates-response"></a>
#### Response

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

| Value | Type | Description |
| --- | --- | --- |
| totalCount | Number | Total number of certificates |
| totalPage | Number | Total number of pages |
| currentPage | Number | Current page |
| pageSize | Number | Page size |
| certificateName | Token ID | Certificate name |
| authority | Token ID | Certificate Authority |
| signatureAlgorithm | Token ID | Signature method |
| fileCreationDate | Token ID | Certificate file creation date |
| expirationDate | Token ID | Certificate file expiration date |

<a id="download-certificate-file"></a>
### Download Certificate File { #download-certificate-file }

Downloads certificates registered in Certificate Manager.

<a id="download-certificate-file-request"></a>
#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files
```

<a id="download-certificate-file-success-response"></a>
#### Success Response

[Response Header]

```
Content-Disposition:attachment; filename="{filename}"
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
#### Failure Response
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
#### For Command Line Interface (CLI)

Download Certificate File API can be requested by using the `curl` command.

```bash
#Write to File
curl -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
    -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}' \
    'https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#Specify File Name
curl -o cert.pem \
    -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
    -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}' \
    'https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files'

#Maintain Uploaded File Name
curl -OJ \
    -H 'X-TC-AUTHENTICATION-ID: {User Access Key ID}' \
    -H 'X-TC-AUTHENTICATION-SECRET: {Secret Access Key}' \
    'https://certmanager.api.nhncloudservice.com/certmanager/v1.1/appkeys/{appKey}/certificates/{certificateName}/files'
```
* See the link below on how to use curl command
  * curl command guide: [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

<a id="response-codes"></a>
### Response Codes { #response-codes }

| isSuccessful | resultCode | resultMessage | Description |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | Successful |
| false | 52000 | Certificate name does not exist. | Requested certificate name does not exist. |
| false | 52001 | Certificate file does not exist. | Requested certificate file does not exist. |
| false | 52002 | There are more than one certificate file. | More than two files are registered for requested certificate. |
| false | 52003 | The certificate file is not a pem file. | Requested certificate file is not pem file. |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | Requested certificate name is different from registered name on certificate file. |
| false | 52005 | Certificate file has expired | Requested certificate file is expired. |
| false | 52006 | The certificate has an invalid certificate authority name. | The certificate authority information in the requested certificate file is invalid. |
| false | 52007 | Requested certificate file should be one. | Only one certificate file can be uploaded at the same time. |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | The maximum file size that can be uploaded is 512KB. |
