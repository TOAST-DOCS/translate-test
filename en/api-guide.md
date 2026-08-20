<!-- machine_translated: true -->

<!-- pre-align:aligned sig=52fa21e7a0e7 -->

<a id="ai-service-speech-to-text-api-guide"></a>
## AI Service > Speech to Text > API Guide { #ai-service-speech-to-text-api-guide }

<a id="speech-recognition-api"></a>
### Speech Recognition API { #speech-recognition-api }

<a id="speech-recognition-api-request"></a>
#### Request

To use the STT API, you need an Appkey or a Project Integrated Appkey.<br/>
An Appkey is a unique authentication key issued for each NHN Cloud service, and a Project Integrated Appkey is a common authentication key that can be used across multiple services within a single NHN Cloud project.<br/>
For more information on checking and using Appkeys, please refer to the [Appkey](/nhncloud/en/public-api/appkey). For more information on creating and using a Project Integrated Appkey, please refer to the [Project Integrated Appkey](/nhncloud/en/public-api/project-integrated-appkey).

[URI]

| Method  | URI                                                              |
|------|------------------------------------------------------------------|
| POST | https://api-speech.nhncloudservice.com/v1.0/appkeys/{appKey}/stt |

[Request Header]

| Name | Value | Description |
|---------------|-------------|----------------|
| Authorization | {secretKey} | Security key issued from the console |

[Request Body]

- Input the binary data of the voice file.

```
curl -X POST 'https://api-speech.nhncloudservice.com/v1.0/appkeys/{appKey}/stt' \
-F 'audio=@sample.mp3' \
-H 'Authorization: ${secretKey}'
```

[Field]

| Name | Type | Description |
|-------|---------------------|--------------------------------------------|
| audio | multipart/form–data | Voice file (WAV, WebM, MP3, OGG, FLAC, AAC, AC3) |

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

| Name            | Type      | Description                               |
|---------------|---------|----------------------------------|
| isSuccessful  | Boolean | Analysis API success or not                     |
| resultCode    | Integer | Result code                            |
| resultMessage | String  | Result message (SUCCESS on success, error content on failure) |

[Field]

| Name          | Type     | Description                  |
|-------------|--------|---------------------|
| inputLength | Double | Recognized voice file duration (unit: seconds) |
| fileType    | String | Recognized voice file type        |
| text        | String | Text conversion result of recognized speech   |
| confidence  | Double | Recognition result confidence           |