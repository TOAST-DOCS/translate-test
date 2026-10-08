<!-- pre-align:aligned sig=0aa4a7e7a7e7 -->

<a id="ai-service-ocr-document-ocr-console-user-guide"></a>
## AI Service > OCR > Document OCR > Console User Guide { #ai-service-ocr-document-ocr-console-user-guide }

You can get the analysis results by uploading image files of business registration certificates, credit cards, and IDs to the console.


<a id="business-registration-certificate-analysis"></a>
## Business Registration Certificate Analysis { #business-registration-certificate-analysis }


<a id="upload-an-image-for-analysis"></a>
### Upload an Image for Analysis { #upload-an-image-for-analysis }

Upload an image of the business registration certificate to analyze.

- Images can be uploaded in the following two methods:
    1. Click the **Upload Image** button
    2. Drag and drop the image

<a id="analysis"></a>
### Analysis { #analysis }

After uploading the image, click the **Analyze** button and the analysis results will appear on the right side of the screen.

![Business Registration](http://static.toastoven.net/prod_ocr/business_ocr_console_en.png)

* [Text (Key Value)] Displays the analyzed contents of the business registration certificate in the form of Key/Value.
* [JSON] Displays the analysis results in JSON format.
    * [success] Analysis success/failure
    * [fileType] File extension (.pdf, .jpg, .png)
    * [keyValues] Analysis results
        * [key] Value corresponding to the key in the business registration certificate (classification, shop name, address, etc.)
        * [value] Value corresponding to a specific key
        * [conf] Confidence of an analysis result
    * [resolution] normal: the resolution is the recommended resolution (HD 1280*720px) or above, low: the resolution is below the recommended resolution
    * [unitType] Coordinate unit for boxes (pixel by default, point for PDF)
    * [boxes] Coordinate values of the recognized area on the image ({x1, y1, x2, y2, x3, y3, x4, y4} format for each box)
![bbox](http://static.toastoven.net/prod_ocr/bbox.png)
    * [JSON Sample]

```json
{
  "fileType": "jpg",
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
```

* Provides the feature to copy or download analysis results (Excel, JSON).

<a id="modify"></a>
### Modify { #modify }
	
You can modify the content of the business registration certificate after analysis. Click **Modify** to modify the content.

<a id="retrieve-stoppageclosure"></a>
### Retrieve Stoppage/Closure { #retrieve-stoppageclosure }

After analyzing the business registration certificate, you can search whether the business is stopped or closed by the contents of the analysis result. Click **Search for Stoppage/Clousre** to display the search results on the right side of the button.

<a id="credit-card-analysis"></a>
## Credit Card Analysis { #credit-card-analysis }


<a id="credit-card-analysis-upload-an-image-for-analysis"></a>
### Upload an Image for Analysis { #credit-card-analysis-upload-an-image-for-analysis }

Upload an image of the credit card to analyze.

- Images can be uploaded in the following two methods:
    1. Click the **Upload Image** button
    2. Drag and drop the image

<a id="credit-card-analysis-analysis"></a>
### Analysis { #credit-card-analysis-analysis }

After uploading the image, click the **Analyze** button and the analysis results will appear on the right side of the screen.

![Credit Card](http://static.toastoven.net/prod_ocr/credit_card_ocr_console_en.png)

* [Text (Key Value)] Displays the analyzed contents of the credit card in the form of Key/Value.
* [JSON] Displays the analysis results in JSON format.
    * [fileType] File extension (.jpg, .png)
    * [resolution] normal: the resolution is the recommended resolution (760*480px) or above, low: the resolution is below the recommended resolution
    * [cardNums] List of card number analysis results
        * [value] Card number recognition result
        * [conf] Confidence of card number recognition result
    * [totalCardNum] Full card number recognition result
    * [validThru] Expiration date recognition content
        * [value] Expiration date recognition result
        * [conf] Confidence of expiration date recognition result
    * [cardNumBoxes] Coordinate values of the card number recognition area on the image ({x1, y1, x2, y2, x3, y3, x4, y4} format for each box)
    * [validThruBox] Coordinate values of the expiration date recognition area on the image
![bbox](http://static.toastoven.net/prod_ocr/bbox.png)
    * [JSON Sample]

```json
{
  "fileType": "jpg",
  "resolution": "low",
  "cardNums": [
    {
      "value": "1111",
      "conf": 0.67
    },
    {
      "value": "2222",
      "conf": 0.66
    },
    {
      "value": "3333",
      "conf": 0.67
    },
    {
      "value": "4444",
      "conf": 0.34
    }
  ],
  "totalCardNum": "4330288628448618",
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
```
  
* Provides the feature to copy or download analysis results (JSON).

<a id="analyze-id-card"></a>
## Analyze ID Card { #analyze-id-card }


<a id="analyze-id-card-upload-an-image-for-analysis"></a>
### Upload an Image for Analysis { #analyze-id-card-upload-an-image-for-analysis }

Upload an image of an ID card to analyze.

- Images can be uploaded in the following two methods:
    1. Click the **Upload Image** button
    2. Drag and drop the image

<a id="analyze-id-card-analysis"></a>
### Analysis { #analyze-id-card-analysis }

After uploading the image, click the **Analyze** button and the analysis results will appear on the right side of the screen.

![ID Card](http://static.toastoven.net/prod_ocr/id_card_ocr_console_en.png)


* [Text (Key Value)] Displays the analyzed contents of the credit card in the form of Key/Value.
* [JSON] Displays the analysis results in JSON format.
    * [fileType] File extension (.jpg, .png)
    * [resolution] normal: the resolution is the recommended resolution (760\*480px) or above, low: the resolution is below the recommended resolution
    * [idType] resident for resident registration certificate, driver for driver's license, passport for passport
    * [keyValues] Analysis results
        * [key] Value corresponding to the key in the ID card (name, resident registration number, etc.)
        * [value] Value corresponding to a specific key
        * [conf] Confidence of an analysis result
    * [boxes] Coordinate values of the recognized area on the image ({x1, y1, x2, y2, x3, y3, x4, y4} format for each box)
      ![bbox](http://static.toastoven.net/prod_ocr/bbox.png)
    * [JSON Sample]
    
```json
{
  "fileType": "png",
  "resolution": "low",
  "idType": "driver",
  "keyValues": [
    {
      "key": "driverLicenseNumber",
      "value": "12-34-567890-01",
      "conf": 0.91
    },
    {
      "key": "licenseType",
      "value": "1종대형/1종보통/1종소형/특수(대형견인,/소형견인,/구난)/2종보통,/2종/소형/원동기",
      "conf": 0.51
    },
    {
      "key": "name",
      "value": "홍길순",
      "conf": 0.94
    },
    ...
  ],
  "boxes": [
    {
      "x1": 23,
      "y1": 15,
      "x2": 65,
      "y2": 15,
      "x3": 65,
      "y3": 28,
      "x4": 23,
      "y4": 28
    },
    {
      "x1": 69,
      "y1": 15,
      "x2": 112,
      "y2": 15,
      "x3": 112,
      "y3": 28,
      "x4": 69,
      "y4": 28
    },
    ...
  ]
}
```
  
* Provides the feature to copy or download analysis results (JSON).

<a id="analyze-id-card-modify"></a>
### Modify { #analyze-id-card-modify }

You can modify the content of the ID card after analysis. Click**Modify**to modify the content. 

<a id="verify-authenticity"></a>
### Verify Authenticity { #verify-authenticity }

You can verify the authenticity of the ID card (resident registration certificate, driver's license) after analysis. Click **Verify authenticity** and the result appears at the right of the button.