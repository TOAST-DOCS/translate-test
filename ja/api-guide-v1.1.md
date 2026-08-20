<!-- machine_translated: true -->

<!-- pre-align:aligned sig=52fa21e7a0e7 -->

<a id="ai-service-speech-to-text-api-guide"></a>
## AI Service > Speech to Text > API ガイド { #ai-service-speech-to-text-api-guide }

<a id="speech-recognition-api"></a>
### 音声認識 API { #speech-recognition-api }

<a id="speech-recognition-api-request"></a>
#### リクエスト

Speech to Text API は、認証/認可に User Access Key トークンを使用します。User Access Key トークンは、User Access Key をもとに発行される Bearer タイプの一時的なアクセストークンです。User Access Key トークンの発行および使用の詳細については、[User Access Key トークン](/nhncloud/ja/public-api/user-access-key-token)を参照してください。

[URI]

| メソッド | URI                                                              |
|------|------------------------------------------------------------------|
| POST | https://api-speech.nhncloudservice.com/v1.1/appkeys/{appKey}/stt |

[リクエストヘッダー]

| 名前                  | 値                              | 説明                  |
|---------------------|--------------------------------|---------------------|
| X-NHN-Authorization | Bearer {User Access Key Token} | User Access Key トークン |

[リクエスト本文]

- 音声ファイルのバイナリデータを設定します。

```
curl -X POST 'https://api-speech.nhncloudservice.com/v1.1/appkeys/{appKey}/stt' \
-F 'audio=@sample.mp3' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}'
```

[フィールド]

| 名前    | タイプ                  | 説明                                         |
|-------|---------------------|--------------------------------------------|
| audio | multipart/form–data | 音声ファイル（WAV、WebM、MP3、OGG、FLAC、AAC、AC3） |

<a id="speech-recognition-api-response"></a>
#### レスポンス

[レスポンス本文]
```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "result": {
        "inputLength": 1.85,
        "fileType": "mp3",
        "text": "こんにちは。",
        "confidence": 0.94
    }
}
```

[ヘッダー]

| 名前            | タイプ      | 説明                               |
|---------------|---------|----------------------------------|
| isSuccessful  | Boolean | 分析 API の成否                     |
| resultCode    | Integer | 結果コード                            |
| resultMessage | String  | 結果メッセージ（成功時は SUCCESS、失敗時はエラー内容） |

[フィールド]

| 名前          | タイプ     | 説明                  |
|-------------|--------|---------------------|
| inputLength | Double | 認識された音声ファイルの長さ（単位: 秒） |
| fileType    | String | 認識された音声ファイルタイプ        |
| text        | String | 認識された音声のテキスト変換結果   |
| confidence  | Double | 認識結果の信頼度           |