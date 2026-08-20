<!-- machine_translated: true -->

<!-- pre-align:aligned sig=52fa21e7a0e7 -->

<a id="ai-service-speech-to-text-api-guide"></a>
## AI Service > Speech to Text > APIガイド { #ai-service-speech-to-text-api-guide }

<a id="speech-recognition-api"></a>
### 音声認識API { #speech-recognition-api }

<a id="speech-recognition-api-request"></a>
#### リクエスト

STT API を使用するには、Appkey またはプロジェクト統合 Appkey が必要です。<br/>
Appkey は NHN Cloud の各サービスごとに発行される固有の認証キーであり、プロジェクト統合 Appkey は NHN Cloud で一つのプロジェクト内の複数のサービスに共通して使用できる認証キーです。<br/>
Appkey の確認および使用に関する詳細については、[Appkey](/nhncloud/ja/public-api/appkey) を参照してください。プロジェクト統合 Appkey の作成および使用に関する詳細については、[プロジェクト統合 Appkey](/nhncloud/ja/public-api/project-integrated-appkey) を参照してください。

[URI]

| メソッド | URI                                                              |
|------|------------------------------------------------------------------|
| POST | https://api-speech.nhncloudservice.com/v1.0/appkeys/{appKey}/stt |

[リクエストヘッダ]

| 名前            | 値           | 説明             |
|---------------|-------------|----------------|
| Authorization | {secretKey} | コンソールで発行されたセキュリティキー |

[リクエスト本文]

- 音声ファイルのバイナリデータを入れます。

```
curl -X POST 'https://api-speech.nhncloudservice.com/v1.0/appkeys/{appKey}/stt' \
-F 'audio=@sample.mp3' \
-H 'Authorization: ${secretKey}'
```

[フィールド]

| 名前    | タイプ                  | 説明                                         |
|-------|---------------------|--------------------------------------------|
| audio | multipart/form–data | 音声ファイル(WAV、WebM、MP3、OGG、FLAC、AAC、AC3) |

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

[ヘッダ]

| 名前            | タイプ      | 説明                               |
|---------------|---------|----------------------------------|
| isSuccessful  | Boolean | 分析 API の成功可否                     |
| resultCode    | Integer | 結果コード                            |
| resultMessage | String  | 結果メッセージ（成功時は SUCCESS、失敗時はエラー内容） |

[フィールド]

| 名前          | タイプ     | 説明                  |
|-------------|--------|---------------------|
| inputLength | Double | 認識した音声ファイルの長さ(単位：秒) |
| fileType    | String | 認識された音声ファイルタイプ        |
| text        | String | 認識された音声のテキスト変換結果 |
| confidence  | Double | 認識結果の信頼度           |
