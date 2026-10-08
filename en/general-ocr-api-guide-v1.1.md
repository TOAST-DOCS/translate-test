<!-- pre-align:aligned sig=2e88c3fa0965 -->

<a id="ai-service-ocr-general-ocr-api-v11-guide"></a>
## AI Service > OCR > General OCR > API v1.1 Guide { #ai-service-ocr-general-ocr-api-v11-guide }

<a id="general-ocr-api-common-information"></a>
## General OCR API Common Information { #general-ocr-api-common-information }

<a id="api-endpoints"></a>
### API Endpoints { #api-endpoints }

| Region               | Endpoint                            |
| -------------------- | ----------------------------------- |
| Korea (Pangyo) Region | https://api-ocr.nhncloudservice.com |

<a id="authentication-and-authorization"></a>
### Authentication and Authorization { #authentication-and-authorization }

General OCR uses User Access Key tokens for authentication and authorization when making API calls. The User Access Key token is a temporary, Bearer-type access token issued from a User Access Key.
For more information on issuing and using User Access Key tokens, please see the [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

<a id="common-response-information"></a>
### Common Response Information { #common-response-information }

All API requests return HTTP 200 OK. The success or failure of an API request can be determined by referring to the header field in the response body.

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

| Name          | Type    | Description                                                  |
| ------------- | ------- | ------------------------------------------------------------ |
| resultCode    | int     | Response code<br>Returns 0 on success, error code on failure |
| resultMessage | String  | Response message                                             |
| isSuccessful  | boolean | Success or not                                               |

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
| 4000005    | Required headers are missing.                                                              | Required headers are missing               |
| 4000006    | Api call limit exceeded. If you need to adjust the limit, please contact customer service. | API call limit exceeded                    |
| 4010006    | Invalid token.                                                                             | Invalid token                              |
| 4010007    | Permission denied.                                                                         | Permission denied                          |
| 4131000    | Request size is larger than permissible limit.                                             | Request size exceeds the permissible limit |

<a id="general-ocr-api"></a>
### General OCR API { #general-ocr-api }

<a id="general-ocr-api-request"></a>
#### Request

[URI]

| Method | URI                            |
| ------ | ------------------------------ |
| POST   | /v1.1/appkeys/{appKey}/general |

<a id="general-ocr-api-request-with-image-file"></a>
#### Request with Image File

[Request Header]

| Name                | Value                          | Description           |
| ------------------- | ------------------------------ | --------------------- |
| X-NHN-Authorization | Bearer {User Access Key Token} | User Access Key token |
| Content-Type        | multipart/form-data            | Content type          |

[Request Body]

- Put the binary data of the image file.

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/general' \
-F 'image=@sample.png' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: multipart/form-data'
```

[Field]

| Name  | Type                | Description |
| ----- | ------------------- | ----------- |
| image | multipart/form-data | Image file  |

<a id="general-ocr-api-request-with-image-url"></a>
#### Request with Image URL

[Request Header]

| Name                | Value                          | Description           |
| ------------------- | ------------------------------ | --------------------- |
| X-NHN-Authorization | Bearer {User Access Key Token} | User Access Key token |
| Content-Type        | application/json               | Content type          |

[Request Body]

- Put the image URL.

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/general' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: application/json' \
--data '{ "imageUrl": "https://example.com/example.jpg" }'
```

[Field]

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| imageUrl | String | Image URL   |

- When directly specifying the port in the image URL, only ports 80, 443, and 10,000-12,000 are available.

<a id="general-ocr-api-response"></a>
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
    "listOfInferTexts": [
      {
        "inferTexts": [
          {
            "value": "stella",
            "conf": 0.99
          },
          {
            "value": "artois",
            "conf": 0.98
          }
        ],
        "inferTexts": [
          {
            "value": "belgium",
            "conf": 0.99
          }
        ]
      }
    ],
    "listOfBoundingBoxes": [
      {
        "boundingBoxes": [
          {
            "x1": 32,
            "y1": 23,
            "x2": 65,
            "y2": 23,
            "x3": 65,
            "y3": 35,
            "x4": 32,
            "y4": 35
          }
        ]
      }
    ]
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

| Name                                    | Type   | Description                                                       |
| --------------------------------------- | ------ | ----------------------------------------------------------------- |
| fileType                                | String | File extension (jpg, png)                                         |
| listOfInferTexts                        | List   | List of recognition results                                       |
| listOfInferTexts[0].inferTexts[0].value | String | Recognized content                                                |
| listOfInferTexts[0].inferTexts[0].conf  | Double | Confidence of the recognition result                              |
| listOfBoundingBoxes                     | List   | List of recognized area (bounding box) coordinates                |
| listOfBoundingBoxes[0].boundingBoxes[0] | Object | Coordinates of recognized area { x1, y1, x2, y2, x3, y3, x4, y4 } |

- boxes[0]
  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)

<a id="general-ocr-segmentation-recognition-api"></a>
### General OCR Segmentation Recognition API { #general-ocr-segmentation-recognition-api }

<a id="general-ocr-segmentation-recognition-api-request"></a>
#### Request

[URI]

| Method | URI                                     |
| ------ | --------------------------------------- |
| POST   | /v1.1/appkeys/{appKey}/general/cropping |

<a id="general-ocr-segmentation-recognition-api-request-with-image-file"></a>
#### Request with Image File

[Request Header]

| Name                | Value                          | Description           |
| ------------------- | ------------------------------ | --------------------- |
| X-NHN-Authorization | Bearer {User Access Key Token} | User Access Key token |
| Content-Type        | multipart/form-data            | Content type          |

[Request Body]

- Put the binary data of the image file.

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/general/cropping' \
-F 'image=@sample.png' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: multipart/form-data'
```

[Field]

| Name  | Type                | Description |
| ----- | ------------------- | ----------- |
| image | multipart/form-data | Image file  |

<a id="general-ocr-segmentation-recognition-api-request-with-image-url"></a>
#### Request with Image URL

[Request Header]

| Name                | Value                          | Description           |
| ------------------- | ------------------------------ | --------------------- |
| X-NHN-Authorization | Bearer {User Access Key Token} | User Access Key token |
| Content-Type        | application/json               | Content type          |

[Request Body]

- Put the image URL.

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/general/cropping' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: application/json' \
--data '{ "imageUrl": "https://example.com/example.jpg" }'
```

[Field]

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| imageUrl | String | Image URL   |

- When directly specifying the port in the image URL, only ports 80, 443, and 10,000-12,000 are available.

<a id="general-ocr-segmentation-recognition-api-response"></a>
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
    "listOfInferTexts": [
      {
        "inferTexts": [
          {
            "value": "stella",
            "conf": 0.99
          },
          {
            "value": "artois",
            "conf": 0.98
          }
        ],
        "inferTexts": [
          {
            "value": "belgium",
            "conf": 0.99
          }
        ]
      }
    ],
    "listOfBoundingBoxes": [
      {
        "boundingBoxes": [
          {
            "x1": 32,
            "y1": 23,
            "x2": 65,
            "y2": 23,
            "x3": 65,
            "y3": 35,
            "x4": 32,
            "y4": 35
          }
        ]
      }
    ],
    "slicesImages": 2
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

| Name                                    | Type    | Description                                                                        |
| --------------------------------------- | ------- | ---------------------------------------------------------------------------------- |
| fileType                                | String  | File extension (jpg, png)                                                          |
| listOfInferTexts                        | List    | List of recognition results                                                        |
| listOfInferTexts[0].inferTexts[0].value | String  | Recognized content                                                                 |
| listOfInferTexts[0].inferTexts[0].conf  | Double  | Confidence of the recognition result                                               |
| listOfBoundingBoxes                     | List    | List of recognized area (bounding box) coordinates                                 |
| listOfBoundingBoxes[0].boundingBoxes[0] | Object  | Coordinates of recognized area { x1, y1, x2, y2, x3, y3, x4, y4 }                  |
| slicesImages                            | Integer | Number of images internally segmented based on the aspect ratio of the input image |

- boxes[0]
  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)
