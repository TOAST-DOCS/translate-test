<!-- pre-align:aligned sig=62797d4ab3bf -->

<a id="management-certificate-manager-api-v12-guide"></a>
## Management > Certificate Manager > API v1.2 Guide { #management-certificate-manager-api-v12-guide }

Certificate Manager provides an API for viewing and downloading certificate lists. Clients can register certificates and certificate files in the console and then access the data through the API.

<a id="basic-information"></a>
### Basic information { #basic-information }
<a id="basic-information-endpoint"></a>
#### EndPoint
```text
https://certmanager.api.nhncloudservice.com
```

<a id="basic-information-authentication-and-authorization"></a>
#### Authentication and Authorization

An Appkey is required to use the Certificate Manager API v1.2.

An Appkey is a unique authentication key issued for each individual NHN Cloud service. For more information on checking and using Appkeys, please refer to the [Appkey](/nhncloud/en/public-api/appkey).

<a id="basic-information-apis-provided"></a>
#### APIs Provided
| Method | URI                                                                     | Description |
| ------ |-------------------------------------------------------------------------| --- |
| GET | /certmanager/v1.2/appkeys/{appKey}/certificates                         | Retrieve the certificate list. |
| GET | /certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files | Download the registered certificate file. |

##### API Request Path Variable

| Value | Type | Description |
| --- | --- | --- |
| appKey | String | Appkey of the NHN Cloud project storing the data to be used |
| certificateName | String | Name of the data (certificate) to be used |

##### API Response Data Common Headers

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
| resultCode | Number | API call result code |
| resultMessage | String | API call result message |
| isSuccessful | Boolean | Whether the API call was successful |

<a id="retrieve-certificate-list"></a>
### Retrieve Certificate List { #retrieve-certificate-list }

Use the function to retrieve a list of certificates registered in the Certificate Manager.

<a id="retrieve-certificate-list-request"></a>
#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates?pageSize={pageSize}&pageNum={pageNum}&all={all}&status={status}
```

| Value | Type | Description | Input |
| --- | --- | --- | --- |
| pageSize | Number | Page size | 10 (default) |
| pageNum | Number | Page number | 1 (default) |
| all | Boolean | Full query | true, false (default) |
| status | String | Certificate status | ALL, EXPIRED, UNEXPIRED (default) |

※ The values ​​for "all" and "status" are case-insensitive.

<a id="retrieve-certificate-list-response"></a>
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
| certificateName | String | Certificate name |
| authority | String | Certificate authority |
| signatureAlgorithm | String | Signature method |
| fileCreationDate | String | Certificate file creation date |
| expirationDate | String | Certificate file expiration date |

<a id="download-certificate-file"></a>
### Download Certificate File { #download-certificate-file }

Use the feature to download the certificate file registered on the Certificate Manager.

<a id="download-certificate-file-request"></a>
#### Request

```
GET https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files
```

<a id="download-certificate-file-success-response"></a>
#### Success Response

[Response Header]

```
Content-Disposition:attachment; filename="{filenmae}"
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

<a id="download-certificate-file-when-using-command-line-interfacecli"></a>
#### When Using Command Line Interface(CLI)

The certificate file download API can be requested using the `curl` command.

```bash
#Write to a File
curl 'https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files' > cert.pem

#Specify a file name
curl -o cert.pem 'https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files'

#Keep the uploaded file name
curl -OJ 'https://certmanager.api.nhncloudservice.com/certmanager/v1.2/appkeys/{appKey}/certificates/{certificateName}/files'
```
* For how to use other curl commands, refer to the guide below:
  * curl command guide : [https://curl.haxx.se/docs/manpage.html](https://curl.haxx.se/docs/manpage.html)

<a id="response-code"></a>
### Response Code { #response-code }

| isSuccessful | resultCode | resultMessage | Description |
| ------------ | ---------- | ------------- | --- |
| true | 0 | SUCCESS | Success |
| false | 52000 | Certificate name does not exist. | The requested certificate name does not exist. |
| false | 52001 | Certificate file does not exist. | The requested certificate file does not exist. |
| false | 52002 | There are more than one certificate file. | There are more than one certificate file registered to the requested certificate. |
| false | 52003 | The certificate file is not a pem file. | The requested certificate file is not a pem file. |
| false | 52004 | The certificate name in the file is different from the requested certificate name. | The requested certificate name and the name registered in the certificate file are different. |
| false | 52005 | Certificate file has expired. | The requested certificate file has expired. |
| false | 52006 | The certificate has an invalid certificate authority name. | The certificate authority information in the requested certificate file is invalid. |
| false | 52007 | The requested certificate file should be one. | Only one certificate file can be uploaded at a time. |
| false | 52008 | The maximum permitted size is {} bytes. However, the requested {} bytes. | The maximum file size that can be uploaded is 512KB. |
