<!-- pre-align:aligned sig=1e79fcef4bcf -->

<a id="ai-service-ocr-general-ocr-console-user-guide"></a>
## AI Service > OCR > General OCR > Console User Guide { #ai-service-ocr-general-ocr-console-user-guide }

You can get the results of text analysis included in the image by uploading the image file to the console.

<a id="image-analysis"></a>
## Image Analysis { #image-analysis }

<a id="upload-an-image-for-analysis"></a>
### Upload an Image for Analysis { #upload-an-image-for-analysis }

Upload an image to analyze.

- Images can be uploaded in the following two methods:
    1. Click the **Upload Image** button
    2. Drag and drop the image


<a id="analysis"></a>
### Analysis { #analysis }

After uploading the image, click the **Analyze** button and the analysis results will appear on the right side of the screen.

![General OCR Image](http://static.toastoven.net/prod_ocr/GeneralOCR_console_new_en.png)

* [Text] Displays the analyzed contents.
* [JSON] Displays the analysis results in JSON format.
    * [fileType] File extension (jpg, png)
    * [listOfInferTexts] Analysis result
        * [value] Recognized text content
        * [conf] Confidence score of an analysis result
    * [resolution] normal: the resolution is the recommended resolution (HD 1280\*720px) or above, low: the resolution is below the recommended resolution
    * [listOfBoundingBoxes] Coordinate values of the recognized area on the image ({x1, y1, x2, y2, x3, y3, x4, y4} format for each box)

      ![bbox](http://static.toastoven.net/prod_ocr/bbox.png)

* Provides a feature to copy and download (Text, JSON) analysis results. 

* [JSON Sample]
```json
{
  "fileType": "png",
  "listOfInferTexts": [
    {
      "inferTexts": [
        {
          "value": "Relevant word",
          "conf": 0.72
        }
      ]
    },
    {
      "inferTexts": [
        {
          "value": "피",
          "conf": 0.92
        },
        {
          "value": "blood",
          "conf": 0.59
        },
        {
          "value": "blood",
          "conf": 0.79
        }
      ]
    },
    ...
  ],
  "listOfBoundingBoxes": [
    {
      "boundingBoxes": [
        {
          "x1": 279,
          "y1": 122,
          "x2": 465,
          "y2": 110,
          "x3": 467,
          "y3": 162,
          "x4": 282,
          "y4": 173
        }
      ]
    },
    {
      "boundingBoxes": [
        {
          "x1": 151,
          "y1": 227,
          "x2": 197,
          "y2": 227,
          "x3": 197,
          "y3": 269,
          "x4": 151,
          "y4": 269
        },
        {
          "x1": 430,
          "y1": 219,
          "x2": 546,
          "y2": 216,
          "x3": 547,
          "y3": 255,
          "x4": 431,
          "y4": 258
        },
        {
          "x1": 860,
          "y1": 206,
          "x2": 969,
          "y2": 208,
          "x3": 968,
          "y3": 251,
          "x4": 859,
          "y4": 248
        }
      ]
    },
    ...
  ]
}
```