<!-- pre-align:aligned sig=c609b65a9475 -->

<a id="ai-service-ocr-document-ocr-api-v11-guide"></a>
## AI Service > OCR > Document OCR > API v1.1 Guide { #ai-service-ocr-document-ocr-api-v11-guide }

<a id="document-ocr-api-common-information"></a>
## Document OCR API Common Information { #document-ocr-api-common-information }

<a id="api-endpoints"></a>
### API Endpoints { #api-endpoints }

| Region                | Endpoint                            |
| --------------------- | ----------------------------------- |
| Korea (Pangyo) Region | https://api-ocr.nhncloudservice.com |

<a id="authentication-and-authorization"></a>
### Authentication and Authorization { #authentication-and-authorization }

Document OCR uses User Access Key tokens for authentication and authorization when making API calls. The User Access Key token is a temporary, Bearer-type access token issued from a User Access Key.
For more information on issuing and using User Access Key tokens, see the [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

<a id="common-response-information"></a>
### Common Response Information { #common-response-information }

All API requests return HTTP 200 OK. The success or failure of an API request can be determined by referring to the header in the Response Body.

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
        ...
    }
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

| Name          | Type    | Description                                          |
| ------------- | ------- | ---------------------------------------------------- |
| resultCode    | int     | Response code<br>0 on success, error code on failure |
| resultMessage | String  | Response message                                     |
| isSuccessful  | boolean | Success or not                                       |

<a id="error-codes"></a>
### Error Codes { #error-codes }

<a id="error-codes-common"></a>
#### Common

| Error Code | Error Message                                                                              | Description                                |
| ---------- | ------------------------------------------------------------------------------------------ | ------------------------------------------ |
| -1         | Unknown error.                                                                             | Unknown error                              |
| 4000001    | Invalid parameter.                                                                         | Invalid parameter                          |
| 4000002    | Invalid file.                                                                              | Invalid file                               |
| 4000003    | Invalid file type.                                                                         | Invalid file type                          |
| 4000004    | Uploaded file is empty.                                                                    | Uploaded file is empty                     |
| 4000005    | Required headers are missing.                                                              | Required headers missing                   |
| 4000006    | Api call limit exceeded. If you need to adjust the limit, please contact customer service. | API call limit exceeded                    |
| 4010006    | Invalid token.                                                                             | Invalid token                              |
| 4010007    | Permission denied.                                                                         | Permission denied                          |
| 4131000    | Request size is larger than permissible limit.                                             | Request size exceeds the permissible limit |

<a id="business-registration-certificate-analysis-api"></a>
### Business Registration Certificate Analysis API { #business-registration-certificate-analysis-api }

<a id="business-registration-certificate-analysis-api-request"></a>
#### Request

[URI]

| Method | URI                             |
| ------ | ------------------------------- |
| POST   | /v1.1/appkeys/{appKey}/business |

[Request Header]

| Name                | Value          | Description              |
|---------------------|----------------|--------------------------|
| X-NHN-Authorization | Bearer {User Access Key Token} | Issued Access Token      |

[Path Variable]

| Name   | Value    | Description                         |
| ------ | -------- | ----------------------------------- |
| appKey | {appKey} | Integrated Appkey or Service Appkey |

[Request Body]

* Put the binary data of the image file.

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/business' \
-F 'image=@sample.png' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}'
```

[Field]

| Name  | Type                | Description |
|-------|---------------------|-------------|
| image | multipart/form–data | Image file  |

<a id="business-registration-certificate-analysis-api-response"></a>
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
        "fileType": "png",
        "unitType": "pixel",
        "keyValues": [
            {
                "key":"구분",
                "value":" 간이과세자",
                "conf":0.93
            },
            {
                "key":"등록번호",
                "value":"123-45-67890",
                "conf":1
            },
            ...
        ],
        "boxes": [
            {
                "x1": 340,
                "y1": 3231,
                "x2": 523,
                "y2": 3231,
                "x3": 523,
                "y3": 3297,
                "x4": 340,
                "y4": 3297
            },
            ...
        ],
        "resolution": "normal"
    }
}
```

[Header]

| Name          | Type    | Description                                                   |
| ------------- | ------- | ------------------------------------------------------------- |
| isSuccessful  | Boolean | Analysis API success or not                                   |
| resultCode    | Integer | Result code                                                   |
| resultMessage | String  | Result message (success on success, error details on failure) |

[Field]

| Name               | Type   | Description                                                                                                                            |
| ------------------ | ------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| fileType           | String | File extension (.pdf, .jpg, .png)                                                                                                      |
| keyValues          | List   | List of recognition results                                                                                                            |
| keyValues[0].key   | String | Recognized item name                                                                                                                   |
| keyValues[0].value | String | Recognized content                                                                                                                     |
| keyValues[0].conf  | Double | Confidence of the recognition result                                                                                                   |
| resolution         | String | normal: the resolution is the recommended resolution (HD 1280*720px) or above, low: the resolution is below the recommended resolution |
| unitType           | String | Coordinate unit for boxes (pixel by default, point for PDF)                                                                            |
| boxes              | List   | List of recognized area (bounding box) coordinates                                                                                     |
| boxes[0]           | Object | Coordinates of recognized area { x1, y1, x2, y2, x3, y3, x4, y4 }                                                                      |

* boxes[0]
  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)

<a id="retrieve-business-registration-stoppageclosure-api"></a>
### Retrieve Business Registration Stoppage/Closure API { #retrieve-business-registration-stoppageclosure-api }

<a id="retrieve-business-registration-stoppageclosure-api-request"></a>
#### Request

[URI]

| Method | URI                                    |
| ------ | -------------------------------------- |
| POST   | /v1.1/appkeys/{appKey}/business/status |

[Request Header]

| Name                | Value          | Description              |
|---------------------|----------------|--------------------------|
| X-NHN-Authorization | Bearer {User Access Key Token} | Issued Access Token      |

[Path Variable]

| Name   | Value    | Description                         |
| ------ | -------- | ----------------------------------- |
| appKey | {appKey} | Integrated Appkey or Service Appkey |

[Field]

| Name           | Type   | Description                                          |
| -------------- | ------ | ---------------------------------------------------- |
| businessNumber | String | Business registration certificate number (10 digits) |

[Request Body]

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/business/status' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
--data-raw '{
  "businessNumber": "1234567890"
}'
```

<a id="retrieve-business-registration-stoppageclosure-api-response"></a>
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
    "statusCode": "00",
    "statusMessage": ""
  }
}
```

[Header]

| Name          | Type    | Description                                                     |
| ------------- | ------- | --------------------------------------------------------------- |
| isSuccessful  | Boolean | Whether the Retrieve stoppage/closure API was successful or not |
| resultCode    | Integer | Result code                                                     |
| resultMessage | String  | Result message (Success when successful, error when failed)     |

[Field]

| Name          | Type   | Description                                                          |
|---------------|--------|----------------------------------------------------------------------|
| statusCode    | String | Business registration certificate status code (Hometax result code) |
| statusMessage | String | Business registration certificate status message                    |

* **List of Business Registration Certificate Statuses by "statusCode"**

| Code value | Description                                                                                                                      |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 00         | Businesses not in business                                                                                                       |
| 01         | VAT general taxpayers                                                                                                            |
| 02         | VAT simplified taxpayer                                                                                                          |
| 03         | Exempt from VAT                                                                                                                  |
| 04         | Non-profit corporation or organization with a unique number that is not engaged in a profitable business. National organizations |
| 05         | Inactive                                                                                                                         |
| 06         | Closed                                                                                                                           |
| 09         | Others                                                                                                                           |

<a id="credit-card-analysis-api"></a>
### Credit Card Analysis API { #credit-card-analysis-api }

<a id="credit-card-analysis-api-request"></a>
#### Request

[URI]

| Method | URI                                |
| ------ | ---------------------------------- |
| POST   | /v1.1/appkeys/{appKey}/credit-card |

[Request Header]

| Name          | Value       | Description                          |
|---------------|-------------|--------------------------------------|
| X-NHN-Authorization | Bearer {User Access Key Token} | User Access Key token |

[Path Variable]

| Name   | Value    | Description                         |
| ------ | -------- | ----------------------------------- |
| appKey | {appKey} | Integrated Appkey or Service Appkey |

[Request Body]

- Put the binary data of the image file.

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/credit-card' \
-F 'image=@sample.png' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}'
```

[Field]

| Name  | Type                | Description |
|-------|---------------------|-------------|
| image | multipart/form–data | Image file  |

<a id="credit-card-analysis-api-response"></a>
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
    "fileType": "png",
    "resolution": "low",
    "cardNums": [
      {
        "value": "1111",
        "conf": 0.87
      },
      {
        "value": "2222",
        "conf": 0.99
      },
      {
        "value": "3333",
        "conf": 0.97
      },
      {
        "value": "4444",
        "conf": 0.89
      }
    ],
    "totalCardNum": "111222233334444",
    "cardNumBoxes": [
      {
        "x1": 62,
        "y1": 256,
        "x2": 192,
        "y2": 256,
        "x3": 192,
        "y3": 301,
        "x4": 62,
        "y4": 301
      },
      ...
    ],
    "validThru": {
      "value": "04/19",
      "conf": 0.53
    },
    "validThruBox": {
      "x1": 316,
      "y1": 315,
      "x2": 426,
      "y2": 315,
      "x3": 426,
      "y3": 347,
      "x4": 316,
      "y4": 347
    }
  }
}
```

[Header]

| Name          | Type    | Description                                                   |
| ------------- | ------- | ------------------------------------------------------------- |
| isSuccessful  | Boolean | Analysis API success or not                                   |
| resultCode    | Integer | Result code                                                   |
| resultMessage | String  | Result message (success on success, error details on failure) |

[Field]

| Name              | Type   | Description                                                                                                                        |
| ----------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| fileType          | String | File extension (.jpg, .png)                                                                                                        |
| resolution        | String | normal: the resolution is the recommended resolution (760*480px) or above, low: the resolution is below the recommended resolution |
| cardNums          | List   | List of card number recognition results                                                                                            |
| cardNums[0].value | String | Recognition result                                                                                                                 |
| cardNums[0].conf  | Double | Confidence of the recognition result                                                                                               |
| totalCardNum      | List   | Full card number recognition result                                                                                                |
| cardNumBoxes      | List   | List of coordinates of the card number recognition area (bounding box)                                                             |
| cardNumBoxes[0]   | Object | Coordinates of recognized area { x1, y1, x2, y2, x3, y3, x4, y4 }                                                                  |
| validThru.value   | String | Expiration date recognition content                                                                                                |
| validThru.conf    | Double | Confidence of expiration date recognition result                                                                                   |
| validThruBox      | Object | Coordinates of the expiration date recognition area { x1, y1, x2, y2, x3, y3, x4, y4 }                                             |

- boxes[0]
  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)