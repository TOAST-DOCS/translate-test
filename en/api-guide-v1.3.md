<!-- machine_translated: true -->

<!-- pre-align:aligned sig=1830bd25c1cb -->

<a id="management-certificate-manager-api-v13-guide"></a>
## Management > Certificate Manager > API v1.3 Guide { #management-certificate-manager-api-v13-guide }

Certificate Manager provides APIs to retrieve the certificate list and download certificate files. Clients can register certificates and certificate files in the console and then use the data through APIs.

<a id="certificatemanager-api-common-information"></a>
### CertificateManager API Common Information { #certificatemanager-api-common-information }
<a id="certificatemanager-api-common-information-api-endpoint"></a>
#### API Endpoint
```text
https://certmanager.api.nhncloudservice.com
```
<a id="certificatemanager-api-common-information-authentication-and-authorization"></a>
#### Authentication and Authorization
CertificateManager uses a User Access Key token for authentication/authorization when making API calls.
A User Access Key token is a temporary, Bearer-type access token issued from a User Access Key.
For more information on issuing and using User Access Key tokens, please refer to the [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

The CertificateManager API uses role-based access control (RBAC).<br>
To use the API, you must have the **CertificateManager ADMIN role** or the **CertificateManager VIEWER role**.

<a id="certificatemanager-api-common-information-provided-apis"></a>
#### Provided APIs
| Method | URI                                                                     | Description |
| ------ |-------------------------------------------------------------------------| --- |
| GET | /certmanager/v1.3/appkeys/{appKey}/certificates                         | Retrieves the certificate list. |
| GET | /certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files | Downloads the registered certificate file by certificate name. |
| GET | /certmanager/v1.3/appkeys/{appKey}/certificates/{certificateId}/certificate-files | Downloads the registered certificate file by certificate ID. |

##### Path Variables for API Requests

| Value | Type | Description |
| --- | --- | --- |
| appKey | String | App key of the NHN Cloud project that stores the data to use |
| certificateName | String | Name of the data (certificate) to be used |
| certificateId | Number | ID of the data (certificate) to be used |

##### Common Header for API Response Data

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

| Value | Type | Description |
| --- | --- | --- |
| resultCode | Number | Result code of the API call |
| resultMessage | String | Result message of the API call |
| isSuccessful | Boolean | Whether the API call was successful |

<a id="retrieve-a-certificate-list"></a>
### Retrieve a Certificate List { #retrieve-a-certificate-list }

Use this API to retrieve the certificate list registered in Certificate Manager.

<a id="retrieve-a-certificate-list-request"></a>
#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| Value | Type | Description | Allowed Values |
| --- | --- | --- | --- |
| pageSize | Number | Page size | 10 (default) |
| pageNum | Number | Page number | 1 (default) |
| all | Boolean | Whether to retrieve all | true, false (default) |
| status | String | Certificate status | ALL, EXPIRED, UNEXPIRED (default) |

※ The values for all and status are case-insensitive.

<a id="retrieve-a-certificate-list-response"></a>
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

| Value | Type | Description |
| --- | --- | --- |
| totalCount | Number | Total number of certificates |
| totalPage | Number | Total number of pages |
| currentPage | Number | Current page |
| pageSize | Number | Page size |
| certificateId | Number | Certificate ID |
| certificateName | String | Certificate name |
| authority | String | Certificate authority |
| signatureAlgorithm | String | Signature algorithm |
| fileCreationDate | String | Certificate file creation date |
| expirationDate | String | Certificate file expiration date |

<a id="download-a-certificate-file-certificate-name"></a>
### Download a Certificate File (Certificate Name) { #download-a-certificate-file-certificate-name }

Use this API to download a certificate file registered in Certificate Manager by certificate name.

<a id="download-a-certificate-file-certificate-name-request"></a>
#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files
```

<a id="download-a-certificate-file-certificate-name-success-response"></a>
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

<a id="download-a-certificate-file-certificate-name-failure-response"></a>
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

<a id="download-a-certificate-file-certificate-name-using-the-command-line-interface-cli"></a>
#### Using the Command Line Interface (CLI)

You can send a request to the certificate file download API by using the curl command.

```bash
#Write to file
curl 'https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files' \
    -H "X-NHN-AUTHORIZATION: Bearer {issued token}" > cert.pem

#Specify file name
curl -o cert.pem 'https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files' \
    -H "X-NHN-AUTHORIZATION: Bearer {issued token}"

#Keep uploaded file name
curl -OJ 'https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateName}/files' \
    -H "X-NHN-AUTHORIZATION: Bearer {issued token}"
```
* For other curl command usage, see the guide below.
  * curl command guide: [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

<a id="download-a-certificate-file-certificate-id"></a>
### Download a Certificate File (Certificate ID) { #download-a-certificate-file-certificate-id }

Use this API to download a certificate file registered in Certificate Manager by certificate ID.
The certificate ID is the certificateId value in the Retrieve a Certificate List API response.

<a id="download-a-certificate-file-certificate-id-request"></a>
#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.3/appkeys/{appKey}/certificates/{certificateId}/certificate-files
```

<a id="download-a-certificate-file-certificate-id-success-response"></a>
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

<a id="download-a-certificate-file-certificate-id-failure-response"></a>
#### Failure Response
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

※ The failure response is returned with HTTP status code 404 (Not Found).

<a id="response-code"></a>
### Response Code { #response-code }

| isSuccessful | resultCode | resultMessage | Description |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | Success |
| false | 52000 | Certificate name does not exist. | The requested certificate name does not exist. |
| false | 52001 | Certificate file does not exist. | The requested certificate file does not exist. |
| false | 52002 | There are more than one certificate file. | Two or more files are registered to the requested certificate. |
| false | 52003 | The certificate file is not a pem file. | The requested certificate file is not in PEM format. |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | The certificate name in the requested file does not match the registered certificate name. |
| false | 52005 | Certificate file has expired | The requested certificate file has expired. |
| false | 52006 | The certificate has an invalid certificate authority name. | The certificate authority information in the requested certificate file is not valid. |
| false | 52007 | Requested certificate file should be one. | Only one certificate file can be uploaded at a time. |
| false | 52008 | Maximum permitted size is {} bytes. But, requested {} bytes. | The maximum upload file size is 512 KB. |
| false | 52009 | Certificate id does not exist. | The requested certificate ID does not exist. |