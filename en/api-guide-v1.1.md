<!-- machine_translated: true -->

<!-- pre-align:aligned sig=52fa21e7a0e7 -->

<a id="ai-service-speech-to-text-api-guide"></a>
## AI Service > Speech to Text > API Guide { #ai-service-speech-to-text-api-guide }

<a id="speech-recognition-api"></a>
### Speech Recognition API { #speech-recognition-api }

<a id="speech-recognition-api-request"></a>
#### Request

The Speech to Text API uses a User Access Key token for authentication/authorization. A User Access Key token is a temporary, Bearer-type access token issued from a User Access Key. For more information on issuing and using User Access Key tokens, please refer to the [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

[URI]

| Method | URI                                                              |
|--------|------------------------------------------------------------------|
| POST | https://api-speech.nhncloudservice.com/v1.1/appkeys/{appKey}/stt |

[Request Header]

| Name                  | Value                           | Description            |
|-----------------------|---------------------------------|------------------------|
| X-NHN-Authorization | Bearer {User Access Key Token} | User Access Key token |

[Request Body]

- Enter the binary data of the audio file.

```
curl -X POST 'https://api-speech.nhncloudservice.com/v1.1/appkeys/{appKey}/stt' \
-F 'audio=@sample.mp3' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}'
```

[Fields]

| Name  | Type                  | Description                                              |
|-------|-----------------------|----------------------------------------------------------|
| audio | multipart/form–data | Audio file (WAV, WebM, MP3, OGG, FLAC, AAC, AC3) |

<a id="speech-recognition-api-response"></a>
#### Response

[Response Body]
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
        "text": "Hello.",
        "confidence": 0.94
    }
}
```

[Header]

| Name          | Type    | Description                                                           |
|---------------|---------|-----------------------------------------------------------------------|
| isSuccessful  | Boolean | Whether the analysis API succeeded                                    |
| resultCode    | Integer | Result code                                                           |
| resultMessage | String  | Result message (SUCCESS on success, error details on failure) |

[Fields]

| Name        | Type   | Description                                  |
|-------------|--------|----------------------------------------------|
| inputLength | Double | Length of the recognized audio file (in seconds) |
| fileType    | String | Type of the recognized audio file            |
| text        | String | Text conversion result of the recognized speech |
| confidence  | Double | Confidence of the recognition result         |