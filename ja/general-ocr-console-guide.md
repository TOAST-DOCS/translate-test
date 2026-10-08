<!-- pre-align:aligned sig=1e79fcef4bcf -->

<a id="ai-service-ocr-general-ocr-console-user-guide"></a>
## AI Service > OCR > General OCR > コンソール使用ガイド { #ai-service-ocr-general-ocr-console-user-guide }

コンソールに画像ファイルをアップロードして画像に含まれるテキストの分析結果を得ることができます。

<a id="image-analysis"></a>
## 画像分析 { #image-analysis }

<a id="upload-an-image-for-analysis"></a>
### 分析のための画像アップロード { #upload-an-image-for-analysis }

分析する画像をアップロードします。

- 画像は次の2つの方法でアップロードできます。
    1. **画像アップロード**ボタンをクリック
    2. 画像のドラッグ＆ドロップ


<a id="analysis"></a>
### 分析 { #analysis }

写真をアップロードした後、**分析**ボタンをクリックすると、分析結果が画面右側に表示されます。

![General OCR Image](http://static.toastoven.net/prod_ocr/GeneralOCR_console_new_ja.png)

* [テキスト]分析された画像の内容を表示します。
* [JSON]分析した結果をJSON形式で表示します。

    * [fileType]ファイル拡張子(jpg、png)
    * [listOfInferTexts]分析結果
        * [value]認識したテキストの内容
        * [conf]分析結果の信頼度
    * [resolution]推奨解像度(HD 1280*720px)以上ならnormal、推奨解像度未満はlow
    * [listOfBoundingBoxes]認識領域に対する画像上の座標値(boxごとに{x1, y1, x2, y2, x3, y3, x4, y4}形式)

      ![bbox](http://static.toastoven.net/prod_ocr/bbox.png)

* 分析結果のコピーおよびダウンロード(Text、JSON)機能を提供します。 

* [JSON Sample]
```json
{
  "fileType": "png",
  "listOfInferTexts": [
    {
      "inferTexts": [
        {
          "value": "関連単語",
          "conf": 0.72
        }
      ]
    },
    {
      "inferTexts": [
        {
          "value": "血",
          "conf": 0.92
        },
        {
          "value": "blood",
          "conf": 0.59
        },
        {
          "value": "ブラッド",
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
