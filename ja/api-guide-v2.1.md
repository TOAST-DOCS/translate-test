<!-- machine_translated: true -->

<!-- pre-align:aligned sig=c189227c350c -->

<a id="ai-service-speech-to-text-api-guide"></a>
## AI Service > Speech to Text > API ガイド { #ai-service-speech-to-text-api-guide }

Speech to Text API v2.1 は、より豊富な音声認識結果を提供します。
Speech to Text API v2.1 は、旧バージョンのレスポンス構造を大幅に改善し、さまざまな後処理やユーザーエクスペリエンス向上に必要な情報をより精緻に提供します。

<a id="api-common-information"></a>
## API 共通情報 { #api-common-information }

<a id="preliminary-preparation"></a>
### 事前準備 { #preliminary-preparation }

Speech to Text API は、認証/認可に User Access Key トークンを使用します。User Access Key トークンは、User Access Key をもとに発行される Bearer タイプの一時的なアクセストークンです。User Access Key トークンの発行と使用に関する詳細については、[User Access Key トークン](/nhncloud/ja/public-api/user-access-key-token)を参照してください。

[リクエストヘッダー]

| 名前                  | 値                              | 説明                  |
|---------------------|--------------------------------|---------------------|
| X-NHN-Authorization | Bearer {User Access Key Token} | User Access Key トークン |

<a id="response-common-information"></a>
### レスポンス共通情報 { #response-common-information }

- すべての API リクエストに対して **200 OK** でレスポンスします。詳細なレスポンス結果はレスポンス本文のヘッダーを参照してください。

[成功レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    }
}
```

[失敗レスポンス本文]
```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 404,
        "resultMessage": "Please check your API Url, HTTP Method."
    }
}
```

[ヘッダー]

| 名前            | タイプ      | 説明                               |
|---------------|---------|----------------------------------|
| isSuccessful  | Boolean | 分析 API の成否                     |
| resultCode    | Integer | 結果コード                            |
| resultMessage | String  | 結果メッセージ（成功時は SUCCESS、失敗時はエラー内容） |

<a id="voice-recognition-api"></a>
## 音声認識 API { #voice-recognition-api }

<a id="voice-recognition"></a>
### 音声認識 { #voice-recognition }
- オーディオファイルの音声データをテキスト形式に変換します。

[URI]

| メソッド  | URI                                                              |
|------|------------------------------------------------------------------|
| POST | https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt |

[リクエスト本文]

- 音声ファイルのバイナリデータを指定します。
- ユーザー単語リスト（biasingList）に入力された値に基づき、「차단계」と認識された単語は「차단기」に、「안전 운행」と認識された単語は「안전운행」に置換された結果が提供されます。

```
curl -X POST 'https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt' \
-F 'audio=@sample.mp3' \
-F 'biasingList="차단기_차단계"' \
-F 'biasingList="안전운행_안전 운행"' \ 
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}'
```

[フィールド]

| 名前          | タイプ                  | 必須 | 説明                                                                                                                 |
|-------------|---------------------|-------|--------------------------------------------------------------------------------------------------------------------|
| audio       | multipart/form–data | 必須    | 音声ファイル（WAV、WebM、MP3、OGG、FLAC、AAC、AC3）                                                                         |
| biasingList | String[]            | 任意   | 特定の単語やフレーズを優先的に認識または置換するためのパラメータ。想定される誤認識結果を修正したり、特定のキーワードを強化したりする場合に使用します。各項目は **「正解_モデル認識値」** の形式で構成されます。 |

<a id="voice-recognition-response"></a>
#### 応答

[レスポンス本文]
```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    },
    "result": {
        "inputLength": 220.1,
        "fileType": "mp3float",
        "text": [
            "応答テキストの例です",
        ],
        "timeslot": [
            {
                "startTime": "390",
                "endTime": "12090"
            },
        ],
		"confidence": [
			0
		]
    }
}
```


[フィールド]

| 名前                    | タイプ       | 説明                     |
|-----------------------|----------|------------------------|
| inputLength           | Double   | 認識された音声ファイルの長さ（単位：秒）    |
| fileType              | String   | 認識された音声ファイルタイプ           |
| text                  | String[] | 認識された音声のテキスト変換結果      |
| timeslot              | List     | 同一インデックスのテキストが認識された区間情報 |
| timeslot[0].startTime | Long     | 区間開始時間（millisecond）  |
| timeslot[0].endTime   | Long     | 区間の終了時間（millisecond） |
| confidence            | Double[] | 同一インデックスのテキスト認識結果の信頼度  |


<a id="voice-recognition-api-asynchronous"></a>
## 音声認識 API（非同期） { #voice-recognition-api-asynchronous }

<a id="voice-recognition-asynchronous"></a>
### 音声認識（非同期） { #voice-recognition-asynchronous }
- オーディオファイルの音声データをテキスト形式に変換します。（非同期）

[URI]

| メソッド  | URI                                                                    |
|------|------------------------------------------------------------------------|
| POST | https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt/async |

[リクエスト本文]

- オーディオファイルをダウンロード可能な URL で提供し、音声認識をリクエストします。
- `{appKey}` はコンソールで確認した値に置き換え、`{User Access Key Token}` は発行済みの User Access Key トークンに置き換えます。
- ユーザー単語リスト（biasingList）に入力された値に基づき、「차단계」と認識された単語は「차단기」に、「안전 운행」と認識された単語は「안전운행」に置換された結果が提供されます。

```
curl -X POST 'https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt/async' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: application/json' \
--data '{"audioUrl": "https://url/to/audioFile", "biasingList": ["차단기_차단계", "안전운행_안전 운행"]}'
```

[フィールド]

| 名前          | タイプ       | 必須 | 説明                                                                                                           |
|-------------|----------|-------|--------------------------------------------------------------------------------------------------------------|
| audioUrl    | String   | 必須    | 最大 150MB のダウンロード可能な音声ファイル URL（WAV、WebM、MP3、OGG、FLAC、AAC、AC3）                                         |
| biasingList | String[] | 任意   | 特定の単語やフレーズを優先的に認識または置換するためのパラメータ。想定される誤認識結果を修正したり、特定のキーワードを強化したりする場合に使用します。各項目は **「正解_モデル認識値」** の形式で構成されます。 |

<a id="voice-recognition-asynchronous-response"></a>
#### 応答

[レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "taskId": "6acb2d15-2180-4e79-b92f-45b1e887e920"
}
```

[フィールド]

| 名前     | タイプ     | 説明                           |
|--------|--------|------------------------------|
| taskId | String | 結果照会および再試行をリクエストできる作業UUID |


<a id="check-status"></a>
### 状態確認 { #check-status }
- リクエストした作業の現在の状態を照会します。

[URI]

| メソッド | URI                                                                                    |
|-----|----------------------------------------------------------------------------------------|
| GET | https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt/async/{taskId}/status |

[フィールド]

| 名前     | タイプ     | 必須 | 説明                            |
|--------|--------|-------|-------------------------------|
| taskId | String | 必須    | 非同期音声認識 API 呼び出し後に取得した作業UUID |

<a id="check-status-response"></a>
#### 応答

[レスポンス本文]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "success"
    },
    "taskId": "d3dc604c-ebef-411a-959e-16f99770f2cf",
    "taskStatus": "COMPLETED",
    "result": {
        "inputLength": 220.1,
        "fileType": "mp3float",
        "text": [
            "レスポンステキストの例です",
        ],
        "timeslot": [
            {
                "startTime": "390",
                "endTime": "12090"
            }
        ],
		"confidence": [
			0
		]
    }
}
```

[フィールド]

| 名前         | タイプ     | 説明                                                 |
|------------|--------|----------------------------------------------------|
| taskId     | String | 状態照会をリクエストした作業UUID                                 |
| taskStatus | String | 作業の現在の状態（PENDING、IN_PROGRESS、COMPLETED、FAILED） |
| result     | Result | 作業の状態が COMPLETED の場合の結果値                          |

[Result]

| 名前                    | タイプ       | 説明                     |
|-----------------------|----------|------------------------|
| inputLength           | Double   | 認識された音声ファイルの長さ（単位：秒）    |
| fileType              | String   | 認識された音声ファイルタイプ           |
| text                  | String[] | 認識された音声のテキスト変換結果      |
| timeslot              | List     | 同一インデックスのテキストが認識された区間情報 |
| timeslot[0].startTime | Long     | 区間開始時間（millisecond）  |
| timeslot[0].endTime   | Long     | 区間の終了時間（millisecond） |
| confidence            | Double[] | 同一インデックスのテキスト認識結果の信頼度  |

<a id="retry"></a>
### 再試行 { #retry }
- 失敗した作業の再試行をリクエストします。

[URI]

| メソッド | URI                                                                                   |
|-----|---------------------------------------------------------------------------------------|
| GET | https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt/async/{taskId}/retry |

[フィールド]

| 名前     | タイプ     | 必須 | 説明                            |
|--------|--------|-------|-------------------------------|
| taskId | String | 必須    | 非同期音声認識 API 呼び出し後に取得した作業UUID |

<a id="retry-response"></a>
#### 応答

[レスポンス本文]

```
{
	"header": {
		// 省略
	},
	"result": {
		"taskId": "c337256d-b17e-42ce-9f63-a792a05ae0ef"
	}
}
```
