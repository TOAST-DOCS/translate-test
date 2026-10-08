<!-- pre-align:aligned sig=1e79fcef4bcf -->

<a id="ai-service-ocr-general-ocr-console-user-guide"></a>
## AI Service > OCR > General OCR > 콘솔 사용 가이드 { #ai-service-ocr-general-ocr-console-user-guide }

콘솔에 이미지 파일을 올려 이미지에 포함된 텍스트 분석 결과를 얻을 수 있습니다.

<a id="image-analysis"></a>
## 이미지 분석 { #image-analysis }

<a id="upload-an-image-for-analysis"></a>
### 분석을 위한 이미지 업로드 { #upload-an-image-for-analysis }

분석할 이미지를 업로드합니다.

- 이미지는 다음 2가지 방법으로 업로드할 수 있습니다.
    1. **이미지 업로드** 버튼 클릭
    2. 이미지 드래그 앤드 드롭


<a id="analysis"></a>
### 분석 { #analysis }

사진을 업로드한 후 **분석** 버튼을 클릭하면 분석 결과가 화면 오른쪽에 나타납니다.

![General OCR Image](http://static.toastoven.net/prod_ocr/GeneralOCR_console_new_ko.png)

* [텍스트] 분석된 이미지의 내용을 표시합니다.
* [JSON] 분석한 결과를 JSON 형태로 표시합니다.
    * [fileType] 파일 확장자(jpg, png)
    * [listOfInferTexts] 분석 결과
        * [value] 인식한 텍스트 내용
        * [conf] 분석 결과에 대한 신뢰도
    * [resolution] 권장 해상도(HD 1280*720px) 이상이면 normal, 권장 해상도 미만은 low
    * [listOfBoundingBoxes] 인식 영역에 대한 이미지 상의 좌표값(box 별 {x1, y1, x2, y2, x3, y3, x4, y4} 형태)

      ![bbox](http://static.toastoven.net/prod_ocr/bbox.png)

* 분석 결과 복사 및 다운로드(Text, JSON) 기능을 제공합니다. 

* [JSON Sample]
```json
{
  "fileType": "png",
  "listOfInferTexts": [
    {
      "inferTexts": [
        {
          "value": "관련단어",
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
          "value": "블러드",
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