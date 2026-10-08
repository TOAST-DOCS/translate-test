<!-- pre-align:aligned sig=2e88c3fa0965 -->

<a id="ai-service-ocr-general-ocr-api-v11-guide"></a>
## AI Service > OCR > General OCR > API v1.1 ガイド { #ai-service-ocr-general-ocr-api-v11-guide }

<a id="general-ocr-api-common-information"></a>
## General OCR API 共通情報 { #general-ocr-api-common-information }

<a id="api-endpoints"></a>
### APIエンドポイント { #api-endpoints }

| リージョン              | エンドポイント                      |
| ----------------------- | ----------------------------------- |
| 韓国(パンギョ)リージョン | https://api-ocr.nhncloudservice.com |

<a id="authentication-and-authorization"></a>
### 認証及び権限 { #authentication-and-authorization }

General OCRは、API呼び出し時の認証/認可のためにUser Access Keyトークンを使用します。User Access Keyトークンは、User Access Keyに基づいて発行されるBearerタイプの一時的なアクセストークンです。
User Access Keyトークンの発行及び使用に関する詳細は、[User Access Keyトークン](/nhncloud/ja/public-api/user-access-key-token)を参照してください。

<a id="common-response-information"></a>
### レスポンス共通情報 { #common-response-information }

すべてのAPIリクエストに対してHTTP 200 OKレスポンスを返します。APIリクエストの成否はResponse Bodyのheader項目を参照して判断できます。

<details>
  <summary><strong>成功レスポンス</strong></summary>

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
  <summary><strong>失敗レスポンス</strong></summary>

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

| 名前          | タイプ  | 説明                                              |
| ------------- | ------- | ------------------------------------------------- |
| resultCode    | int     | レスポンスコード<br>成功時0、失敗時エラーコード返却 |
| resultMessage | String  | レスポンスメッセージ                               |
| isSuccessful  | boolean | 成否                                              |

<a id="error-codes"></a>
### エラーコード { #error-codes }

<a id="error-codes-common"></a>
#### 共通

| エラーコード | エラーメッセージ                                                                           | 説明                                |
| ------------ | ------------------------------------------------------------------------------------------ | ----------------------------------- |
| -1           | Unknown error.                                                                             | 不明なエラー                        |
| 4000001      | Invalid parameter.                                                                         | 無効なパラメータ                    |
| 4000002      | Invalid file.                                                                              | 無効なファイル                      |
| 4000003      | Invalid file type.                                                                         | 無効なファイルタイプ                |
| 4000004      | Uploaded file is empty.                                                                    | アップロードされたファイルが空      |
| 4000005      | Required headers is missing.                                                               | 必須ヘッダ不足                      |
| 4000006      | Api call limit exceeded, If you need to adjust the limit, please contact customer service. | API呼び出し上限超過                 |
| 4010006      | Invalid token.                                                                             | 無効なトークン                      |
| 4010007      | Unauthorized.                                                                              | 権限なし                            |
| 4131000      | Request size is larger than permissible limit.                                             | リクエストサイズが許容上限超過                     |

<a id="general-ocr-api"></a>
### General OCR API { #general-ocr-api }

<a id="general-ocr-api-request"></a>
#### リクエスト

[URI]

| メソッド | URI                            |
| -------- | ------------------------------ |
| POST     | /v1.1/appkeys/{appKey}/general |

<a id="general-ocr-api-request-with-image-file"></a>
#### 画像ファイルを利用したリクエスト

[リクエストヘッダ]

| 名前                | 値                  | 説明                    |
| ------------------- | ------------------- | ----------------------- |
| X-NHN-Authorization | Bearer {User Access Key Token}      | User Access Keyトークン |
| Content-Type        | multipart/form-data | コンテンツタイプ        |

[リクエスト本文]

- 画像ファイルのバイナリデータを入れます。

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/general' \
-F 'image=@sample.png' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: multipart/form-data'
```

[フィールド]

| 名前  | タイプ              | 説明       |
| ----- | ------------------- | ---------- |
| image | multipart/form-data | 画像ファイル |

<a id="general-ocr-api-request-with-image-url"></a>
#### 画像URLを利用したリクエスト

[リクエストヘッダ]

| 名前                | 値               | 説明                    |
| ------------------- | ---------------- | ----------------------- |
| X-NHN-Authorization | Bearer {User Access Key Token}   | User Access Keyトークン |
| Content-Type        | application/json | コンテンツタイプ        |

[リクエスト本文]

- 画像のURLを入れます。

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/general' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: application/json' \
--data '{ "imageUrl": "https://example.com/example.jpg" }'
```

[フィールド]

| 名前     | タイプ | 説明    |
| -------- | ------ | ------- |
| imageUrl | String | 画像URL |

- イメージURLにポートを直接指定する場合は80、443、10000～12000ポートのみ使用できます。

<a id="general-ocr-api-response"></a>
#### レスポンス

[レスポンス本文]

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

[ヘッダ]

| 名前          | タイプ  | 説明                                              |
| ------------- | ------- | ------------------------------------------------- |
| isSuccessful  | Boolean | 分析API成否                                       |
| resultCode    | Integer | 結果コード                                        |
| resultMessage | String  | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

[フィールド]

| 名前                                    | タイプ | 説明                                              |
| --------------------------------------- | ------ | ------------------------------------------------- |
| fileType                                | String | ファイル拡張子(jpg、png)                          |
| listOfInferTexts                        | List   | 認識結果リスト                                    |
| listOfInferTexts[0].inferTexts[0].value | String | 認識内容                                          |
| listOfInferTexts[0].inferTexts[0].conf  | Double | 認識結果の信頼度                                  |
| listOfBoundingBoxes                     | List   | 認識領域(Bounding box)座標リスト                  |
| listOfBoundingBoxes[0].boundingBoxes[0] | Object | 認識領域の座標{ x1, y1, x2, y2, x3, y3, x4, y4 } |

- boxes[0]
  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)

<a id="general-ocr-segmentation-recognition-api"></a>
### General OCR分割認識API { #general-ocr-segmentation-recognition-api }

<a id="general-ocr-segmentation-recognition-api-request"></a>
#### リクエスト

[URI]

| メソッド | URI                                     |
| -------- | --------------------------------------- |
| POST     | /v1.1/appkeys/{appKey}/general/cropping |

<a id="general-ocr-segmentation-recognition-api-request-with-image-file"></a>
#### 画像ファイルを利用したリクエスト

[リクエストヘッダ]

| 名前                | 値                  | 説明                    |
| ------------------- | ------------------- | ----------------------- |
| X-NHN-Authorization | Bearer {User Access Key Token}      | User Access Keyトークン |
| Content-Type        | multipart/form-data | コンテンツタイプ        |

[リクエスト本文]

- 画像ファイルのバイナリデータを入れます。

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/general/cropping' \
-F 'image=@sample.png' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: multipart/form-data'
```

[フィールド]

| 名前  | タイプ              | 説明       |
| ----- | ------------------- | ---------- |
| image | multipart/form-data | 画像ファイル |

<a id="general-ocr-segmentation-recognition-api-request-with-image-url"></a>
#### 画像URLを利用したリクエスト

[リクエストヘッダ]

| 名前                | 値               | 説明                    |
| ------------------- | ---------------- | ----------------------- |
| X-NHN-Authorization | Bearer {User Access Key Token}   | User Access Keyトークン |
| Content-Type        | application/json | コンテンツタイプ        |

[リクエスト本文]

- 画像のURLを入れます。

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.1/appkeys/{appKey}/general/cropping' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: application/json' \
--data '{ "imageUrl": "https://example.com/example.jpg" }'
```

[フィールド]

| 名前     | タイプ | 説明    |
| -------- | ------ | ------- |
| imageUrl | String | 画像URL |

- イメージURLにポートを直接指定する場合は80、443、10000～12000ポートのみ使用できます。

<a id="general-ocr-segmentation-recognition-api-response"></a>
#### レスポンス

[レスポンス本文]

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

[ヘッダ]

| 名前          | タイプ  | 説明                                              |
| ------------- | ------- | ------------------------------------------------- |
| isSuccessful  | Boolean | 分析API成否                                       |
| resultCode    | Integer | 結果コード                                        |
| resultMessage | String  | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

[フィールド]

| 名前                                    | タイプ  | 説明                                                          |
| --------------------------------------- | ------- | ------------------------------------------------------------- |
| fileType                                | String  | ファイル拡張子(jpg、png)                                      |
| listOfInferTexts                        | List    | 認識結果リスト                                                |
| listOfInferTexts[0].inferTexts[0].value | String  | 認識内容                                                      |
| listOfInferTexts[0].inferTexts[0].conf  | Double  | 認識結果の信頼度                                              |
| listOfBoundingBoxes                     | List    | 認識領域(Bounding box)座標リスト                              |
| listOfBoundingBoxes[0].boundingBoxes[0] | Object  | 認識領域の座標{ x1, y1, x2, y2, x3, y3, x4, y4 }             |
| slicesImages                            | Integer | 入力画像のアスペクト比に応じて内部的に分割された画像の数      |

- boxes[0]
  ![Bounding box](http://static.toastoven.net/prod_ocr/bbox.png)
