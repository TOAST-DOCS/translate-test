<!-- pre-align:aligned sig=8eec8a51e376 -->

<a id="ai-service-ocr-general-ocr-api-guide"></a>
## AI Service > OCR > General OCR > API Guide { #ai-service-ocr-general-ocr-api-guide }


<a id="general-ocr-api"></a>
### General OCR API { #general-ocr-api }

<a id="general-ocr-api-request"></a>
#### Request

* You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI                                                               |
| ------ | ----------------------------------------------------------------- |
| POST   | https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/general |

<a id="general-ocr-api-request-with-image-files"></a>
#### Request with image files

[Request Header]

| Name          | Value               | Description                          |
| ------------- | ------------------- | ------------------------------------ |
| Authorization | {secretKey}         | Security key issued from the console |
| Content-Type  | multipart/form-data | Content type                         |

[Request Body]

* Put binary data of the image file.

```
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/general' \
-F 'image=@sample.png' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: multipart/form-data'
```

[Field]

| Name  | Type                | Description |
| ----- | ------------------- | ----------- |
| image | multipart/form-data | Image file  |

<a id="general-ocr-api-request-with-image-urls"></a>
#### Request with image URLs

[Request Header] 

| Name          | Value            | Description                          |
| ------------- | ---------------- | ------------------------------------ |
| Authorization | {secretKey}      | Security key issued from the console |
| Content-Type  | application/json | Content type                         |

[Request Body]

* Insert the image URL.

```
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/general' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data '{ "imageUrl": "https://example.com/example.jpg" }'
```

[Field]

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| imageUrl | String | Image URL   |

* If you specify the port directly in the image URL, only ports 80, 443, 10000-12000 can be used.

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
                        "value":"stella",
                        "conf":0.99
                    },
                    {
                        "value":"artois",
                        "conf":0.98
                    }
                ],
                "inferTexts": [
                    {
                        "value":"belgium",
                        "conf":0.99
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
| resultMessage | String  | Result message (success on success, error content on failure) |

[Field]

| Name                                    | Type   | Description                                                       |
| --------------------------------------- | ------ | ----------------------------------------------------------------- |
| fileType                                | String | File extension (jpg, png)                                         |
| listOfInferTexts                        | List   | List of recognition results                                       |
| listOfInferTexts[0].inferTexts[0].value | String | Recognized content                                                |
| listOfInferTexts[0].inferTexts[0].conf  | Double | Confidence score of the recognition result                        |
| listOfBoundingBoxes                     | List   | List of bounding box coordinates                                  |
| listOfBoundingBoxes[0].boundingBoxes[0] | Object | Coordinates of recognized area { x1, y1, x2, y2, x3, y3, x4, y4 } |

* boxes[0]
  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)

<a id="general-ocr-segmentation-recognition-api"></a>
### General OCR segmentation recognition API { #general-ocr-segmentation-recognition-api }

<a id="general-ocr-segmentation-recognition-api-request"></a>
#### Request

- You can check the {appKey} and {secretKey} in the **URL & Appkey** menu at the top of the console.

[URI]

| Method | URI                                                                        |
| ------ | -------------------------------------------------------------------------- |
| POST   | https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/general/cropping |

<a id="general-ocr-segmentation-recognition-api-request-with-image-files"></a>
#### Request with image files

[Request Header] 

| Name          | Value               | Description                          |
| ------------- | ------------------- | ------------------------------------ |
| Authorization | {secretKey}         | Security key issued from the console |
| Content-Type  | multipart/form-data | Content type                         |

[Request Body]

- Input the binary data of the image file.

```
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/general/cropping' \
-F 'image=@sample.png' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: multipart/form-data'
```

[Field]

| Name  | Type                | Description |
| ----- | ------------------- | ----------- |
| image | multipart/form-data | Image file  |

<a id="general-ocr-segmentation-recognition-api-request-with-image-urls"></a>
#### Request with image URLs
[Request Header] 

| Name          | Value            | Description                          |
| ------------- | ---------------- | ------------------------------------ |
| Authorization | {secretKey}      | Security key issued from the console |
| Content-Type  | application/json | Content type                         |

[Request Body]

- Insert the image URL.

```
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/general/cropping' \
-H 'Authorization: ${secretKey}' \
-H 'Content-Type: application/json' \
--data '{ "imageUrl": "https://example.com/example.jpg" }'
```

[Field]

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| imageUrl | String | Image URL   |

* If you specify the port directly in the image URL, only ports 80, 443, 10000-12000 can be used.

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
                        "value":"stella",
                        "conf":0.99
                    },
                    {
                        "value":"artois",
                        "conf":0.98
                    }
                ],
                "inferTexts": [
                    {
                        "value":"belgium",
                        "conf":0.99
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
| resultMessage | String  | Result message (success on success, error content on failure) |

[Field]

| Name                                    | Type    | Description                                                         |
| --------------------------------------- | ------- | ------------------------------------------------------------------- |
| fileType                                | String  | File extension (jpg, png)                                           |
| listOfInferTexts                        | List    | List of recognition results                                         |
| listOfInferTexts[0].inferTexts[0].value | String  | Recognized content                                                  |
| listOfInferTexts[0].inferTexts[0].conf  | Double  | Confidence score of the recognition result                          |
| listOfBoundingBoxes                     | List    | List of bounding box coordinates                                    |
| listOfBoundingBoxes[0].boundingBoxes[0] | Object  | Coordinates of recognized area { x1, y1, x2, y2, x3, y3, x4, y4 }   |
| slicesImages                            | Integer | Number of images internally split based on the image's aspect ratio |

* boxes[0]
  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)