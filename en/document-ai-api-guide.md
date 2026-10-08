<!-- pre-align:aligned sig=c6e7b8f5a7f1 -->

<a id="ai-service-ocr-document-ai-api-guide"></a>
## AI Service > OCR > Document AI > API Guide { #ai-service-ocr-document-ai-api-guide }

<a id="document-ai-analysis-api"></a>
### Document AI Analysis API { #document-ai-analysis-api }

<a id="document-ai-analysis-api-request"></a>
#### Request

* You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top right of the console.

[URI]

| Method  | URI                                                               |
|------|-------------------------------------------------------------------|
| POST | https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/document-ai |

[Request Header]

| Name            | Value                   | Description              |
|---------------|---------------------|-----------------|
| Authorization | {secretKey}         | Security key issued from the console |
| Content-Type  | multipart/form-data | Content type          |

[Request Body]

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/document-ai' \
-H 'Authorization: ${secretKey}' \
-F 'image=@sample.png' \
-F 'prompt="Give me a quick summary"' \
-F 'documentTypeCode="GENERAL"'
```

[Field]

| Name    | Type   | Required | Default value | Valid range | Description    |
|-------|--------|---------|--------|--------|--------|
| image | file | O |     |   | Template image file|
| documentTypeCode | text | X |  GENERAL | GENERAL, BUSINESS_REGISTRATION, BUSINESS_CARD  | Document type<br> General: GENERAL <br> Business registration: BUSINESS_REGISTRATION <br> Business card: BUSINESS_CARD |
| prompt | text | O |    |   | Question content<br>Up to 1,000 characters  |

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
        "llmResponse": "This document appears to have been written using 'loren ipsum', a meaningless text, to create a sentence that has letters but is difficult and illegible to read."
    }
}
```

[Header]

| Name            | Type      | Description                               |
|---------------|---------|----------------------------------|
| isSuccessful  | Boolean | Analysis API success or not                     |
| resultCode    | Integer | Result code                            |
| resultMessage | String  | Result message (success on success, error content on failure) |

[Field]

| Name                                      | Type     | Description                                          |
|-----------------------------------------|--------|---------------------------------------------|
| llmResponse                                | String | LLM Analysis Answer                           |
