<!-- pre-align:aligned sig=c6e7b8f5a7f1 -->

<a id="ai-service-ocr-document-ai-api-guide"></a>
## AI Service > OCR > Document AI > APIガイド { #ai-service-ocr-document-ai-api-guide }

<a id="document-ai-analysis-api"></a>
### Document AI分析API { #document-ai-analysis-api }

<a id="document-ai-analysis-api-request"></a>
#### リクエスト

[URI]

| メソッド | URI                                                               |
|------|-------------------------------------------------------------------|
| POST | https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/document-ai |

[リクエストヘッダ]

| 名前          | 値                 | 説明            |
|---------------|---------------------|-----------------|
| Authorization | {secretKey}         | コンソールで発行された秘密鍵 |
| Content-Type  | multipart/form-data | コンテンツタイプ        |

[リクエスト本文]

```shell
curl -X POST 'https://api-ocr.nhncloudservice.com/v1.0/appkeys/{appKey}/document-ai' \
-H 'Authorization: ${secretKey}' \
-F 'image=@sample.png' \
-F 'prompt="簡潔に要約してくれ"' \
-F 'documentTypeCode="GENERAL"'
```

[フィールド]

| 名前  | タイプ | 必須かどうか | デフォルト値 | 有効範囲 | 説明  |
|-------|--------|---------|--------|--------|--------|
| image | file | O |     |   | イメージファイル|
| documentTypeCode | text | X |  GENERAL | GENERAL, BUSINESS_REGISTRATION, BUSINESS_CARD  | 文書タイプ<br> 一般: GENERAL <br> 事業者登録証: BUSINESS_REGISTRATION <br> 名刺: BUSINESS_CARD |
| prompt | text | O |    |   | 質問内容<br>最大1000文字 |

<a id="document-ai-analysis-api-response"></a>
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
        "llmResponse": "この文書は、意味のないテキストである'ローレンipsum'を使用して、文字はあるが読みにくい、可読性が落ちる文章を作成したようです。"
    }
}
```

[ヘッダ]

| 名前          | タイプ    | 説明                             |
|---------------|---------|----------------------------------|
| isSuccessful  | Boolean | 分析API成否                   |
| resultCode    | Integer | 結果コード                          |
| resultMessage | String  | 結果メッセージ(成功時はsuccess、失敗時はエラー内容) |

[フィールド]

| 名前                                    | タイプ   | 説明                                        |
|-----------------------------------------|--------|---------------------------------------------|
| llmResponse                                | String | LLM分析回答                          |
