<!-- pre-align:aligned sig=d64a96abd1ac -->

<a id="ai-service-ocr-document-ai-api-v10-guide"></a>
## AI Service > OCR > Document AI > API v1.0 Guide { #ai-service-ocr-document-ai-api-v10-guide }

<a id="document-ai-api-common-information"></a>
## Document AI API Common Information { #document-ai-api-common-information }

<a id="api-endpoints"></a>
### API Endpoints { #api-endpoints }

| Region                | Endpoint                            |
| --------------------- | ----------------------------------- |
| Korea (Pangyo) Region | https://api-ocr.nhncloudservice.com |

<a id="authentication-and-authorization"></a>
### Authentication and Authorization { #authentication-and-authorization }

AppKey and SecretKey are required to use the Document AI API.
An Appkey is a unique authentication key issued for each NHN Cloud service that identifies the service and validates API requests. A SecretKey is a private key used to control access to the API.
For more information on checking and using Appkeys and SecretKeys, please refer to the [Appkey](/nhncloud/en/public-api/appkey).

Project Integrated Appkey can be used in place of the Appkey. Project Integrated Appkey is a common authentication key that can be shared across multiple services within a single NHN Cloud project.
For more information on creating and using Project Integrated Appkeys, see the [Project Integrated Appkey](/nhncloud/en/public-api/project-appkey).

<a id="common-response-information"></a>
### Common Response Information { #common-response-information }

All API requests return HTTP 200 OK. The success or failure of an API request can be determined by referring to the header field in the Response Body.

<details>
  <summary><strong>Success Response</strong></summary>

```
HTTP/1.1 200 OK
Content-Type: application/json

{
    "header": {
        "resultCode": 0,
        "resultMessage": "SUCCESS",
        "isSuccessful": true
    },
    "result": {
        "llmResponse": ...
    },
    ...
}
```

</details>

<details>
  <summary><strong>Failure Response</strong></summary>

```
{
    "header": {
        "isSuccessful": false,
        "resultCode": -1,
        "resultMessage": "Unknown error."
    }
}
```

</details>

| Name          | Type    | Description                                                  |
| ------------- | ------- | ------------------------------------------------------------ |
| resultCode    | int     | Response code<br>Returns 0 on success, error code on failure |
| resultMessage | String  | Response message                                             |
| isSuccessful  | boolean | Success or not                                               |

<a id="error-codes"></a>
### Error Codes { #error-codes }

<a id="error-codes-common"></a>
#### Common

| Error Code | Error Message                                                                              | Description                |
| ---------- | ------------------------------------------------------------------------------------------ | -------------------------- |
| -1         | Unknown error.                                                                             | Unknown error              |
| 4000001    | Invalid parameter.                                                                         | Invalid parameter          |
| 4000002    | Invalid file.                                                                              | Invalid file               |
| 4000003    | Invalid file type.                                                                         | Invalid file type          |
| 4000004    | Uploaded file is empty.                                                                    | Uploaded file is empty     |
| 4000005    | Required headers are missing.                                                              | Required headers missing   |
| 4000006    | Api call limit exceeded. If you need to adjust the limit, please contact customer service. | API call limit exceeded    |
| 4131000    | Request size is larger than permissible limit.                                             | Request size exceeds limit |

<a id="document-ai-analysis-api"></a>
### Document AI Analysis API { #document-ai-analysis-api }

[URI]

| Method | URI                                |
| ------ | ---------------------------------- |
| POST   | /v1.0/appkeys/{appKey}/document-ai |

[Request Header]

| Name          | Value               | Description                      |
| ------------- | ------------------- | -------------------------------- |
| Authorization | {secretKey}         | Security key issued from console |
| Content-Type  | multipart/form-data | Content type                     |

[Request Body]

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/document-ai' \
-H 'Authorization: ${secretKey}' \
-F 'image=@sample.png' \
-F 'prompt="Give me a quick summary"' \
-F 'documentTypeCode="GENERAL"'
```

[Field]

| Name             | Type | Required | Default | Valid Range                                   | Description                                                                                                            |
| ---------------- | ---- | -------- | ------- | --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| image            | file | O        |         |                                               | Image file                                                                                                             |
| documentTypeCode | text | X        | GENERAL | GENERAL, BUSINESS_REGISTRATION, BUSINESS_CARD | Document type<br> General: GENERAL <br> Business registration: BUSINESS_REGISTRATION <br> Business card: BUSINESS_CARD |
| prompt           | text | O        |         |                                               | Question content<br>Up to 1,000 characters                                                                             |

<a id="document-ai-analysis-api-response"></a>
#### Response

[Response Body]

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "result": {
    "llmResponse": "This document appears to have been written using 'lorem ipsum', a meaningless text, to create a sentence that has letters but is difficult and illegible to read."
  }
}
```

[Header]

| Name          | Type    | Description                                                   |
| ------------- | ------- | ------------------------------------------------------------- |
| isSuccessful  | Boolean | Analysis API success or not                                   |
| resultCode    | Integer | Result code                                                   |
| resultMessage | String  | Result message (success on success, error content on failure) |

[Field]

| Name        | Type   | Description        |
| ----------- | ------ | ------------------ |
| llmResponse | String | LLM analysis answer |
