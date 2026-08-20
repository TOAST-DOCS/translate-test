<!-- machine_translated: true -->

<!-- pre-align:aligned sig=c189227c350c -->

<a id="ai-service-speech-to-text-api-guide"></a>
## AI Service > Speech to Text > API Guide { #ai-service-speech-to-text-api-guide }

Speech to Text API v2.1 provides richer speech recognition results.
Speech to Text API v2.1 significantly improves the response structure of previous versions, providing more detailed information needed for various post-processing tasks and user experience improvements.

<a id="api-common-information"></a>
## API Common Information { #api-common-information }

<a id="preliminary-preparation"></a>
### Preliminary Preparation { #preliminary-preparation }

The Speech to Text API uses a User Access Key token for authentication and authorization. A User Access Key token is a temporary access token of the Bearer type that is issued based on a User Access Key. For more information on issuing and using User Access Key tokens, please refer to the [User Access Key Token](/nhncloud/en/public-api/user-access-key-token).

[Request Header]

| Name | Value | Description |
|---------------------|--------------------------------|---------------------|
| X-NHN-Authorization | Bearer {User Access Key Token} | User Access Key token |

<a id="response-common-information"></a>
### Response Common Information { #response-common-information }

- The API responds with **200 OK** to all API requests. For more information on the response results, see Response Body Header.

[Successful Response Body]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    }
}
```

[Failed Response Body]
```
{
    "header": {
        "isSuccessful": false,
        "resultCode": 404,
        "resultMessage": "Please check your API Url, HTTP Method."
    }
}
```

[Header]

| Name | Type | Description |
|---------------|---------|----------------------------------|
| isSuccessful  | Boolean | Whether the analysis API call was successful |
| resultCode    | Integer | Result code |
| resultMessage | String  | Result message (SUCCESS on success, error details on failure) |

<a id="voice-recognition-api"></a>
## Voice Recognition API { #voice-recognition-api }

<a id="voice-recognition"></a>
### Voice Recognition { #voice-recognition }
- Extracts speech data from an audio file and converts it to text.

[URI]

| Method | URI |
|------|------------------------------------------------------------------|
| POST | https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt |

[Request Body]

- Enter the binary data of the audio file.
- Based on the values entered in the user word list (biasingList), words recognized as "차단계" are replaced with "차단기", and words recognized as "안전 운행" are replaced with "안전운행".

```
curl -X POST 'https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt' \
-F 'audio=@sample.mp3' \
-F 'biasingList="차단기_차단계"' \
-F 'biasingList="안전운행_안전 운행"' \ 
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}'
```

[Fields]

| Name | Type | Required | Description |
|-------------|---------------------|-------|--------------------------------------------------------------------------------------------------------------------|
| audio       | multipart/form–data | Required | Audio file (WAV, WebM, MP3, OGG, FLAC, AAC, AC3) |
| biasingList | String[]            | Optional | A parameter that helps prioritize recognition or replace specific words or phrases. Use this when you want to correct expected misrecognition results or reinforce specific keywords. Each entry is structured in the format **"correct_answer_model_recognition_value"**. |

<a id="voice-recognition-response"></a>
#### Response

[Response Body]
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
            "This is an example response text.",
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


[Fields]

| Name | Type | Description |
|-----------------------|----------|------------------------|
| inputLength           | Double   | Length of the recognized audio file (in seconds) |
| fileType              | String   | Type of the recognized audio file |
| text                  | String[] | Text conversion result of the recognized speech |
| timeslot              | List     | Section information for the text recognized at the same index |
| timeslot[0].startTime | Long     | Section start time (milliseconds) |
| timeslot[0].endTime   | Long     | Section end time (milliseconds) |
| confidence            | Double[] | Confidence of the text recognition result at the same index |


<a id="voice-recognition-api-asynchronous"></a>
## Voice Recognition API (Asynchronous) { #voice-recognition-api-asynchronous }

<a id="voice-recognition-asynchronous"></a>
### Voice Recognition (Asynchronous) { #voice-recognition-asynchronous }
- Extracts speech data from an audio file and converts it to text (asynchronous).

[URI]

| Method | URI |
|------|------------------------------------------------------------------------|
| POST | https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt/async |

[Request Body]

- Requests speech recognition by providing a downloadable URL for the audio file.
- Replace {appKey} with the value obtained from the console, and replace {User Access Key Token} with the issued User Access Key token.
- Based on the values entered in the user word list (biasingList), words recognized as "차단계" are replaced with "차단기", and words recognized as "안전 운행" are replaced with "안전운행".

```
curl -X POST 'https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt/async' \
-H 'X-NHN-Authorization: Bearer ${User Access Key Token}' \
-H 'Content-Type: application/json' \
--data '{"audioUrl": "https://url/to/audioFile", "biasingList": ["차단기_차단계", "안전운행_안전 운행"]}'
```

[Fields]

| Name | Type | Required | Description |
|-------------|----------|-------|--------------------------------------------------------------------------------------------------------------|
| audioUrl    | String   | Required | Downloadable audio file URL of up to 150 MB (WAV, WebM, MP3, OGG, FLAC, AAC, AC3) |
| biasingList | String[] | Optional | A parameter that helps prioritize recognition or replace specific words or phrases. Use this when you want to correct expected misrecognition results or reinforce specific keywords. Each entry is structured in the format **"correct_answer_model_recognition_value"**. |

<a id="voice-recognition-asynchronous-response"></a>
#### Response

[Response Body]

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

[Fields]

| Name | Type | Description |
|--------|--------|------------------------------|
| taskId | String | Task UUID that can be used to request result retrieval or retry |


<a id="check-status"></a>
### Check Status { #check-status }
- Retrieves the current status of the requested task.

[URI]

| Method | URI |
|-----|----------------------------------------------------------------------------------------|
| GET | https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt/async/{taskId}/status |

[Fields]

| Name | Type | Required | Description |
|--------|--------|-------|-------------------------------|
| taskId | String | Required | Task UUID received after calling the asynchronous voice recognition API |

<a id="check-status-response"></a>
#### Response

[Response Body]

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
            "This is an example response text.",
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

[Fields]

| Name | Type | Description |
|------------|--------|----------------------------------------------------|
| taskId     | String | Task UUID for which the status was requested |
| taskStatus | String | Current status of the task (PENDING, IN_PROGRESS, COMPLETED, FAILED) |
| result     | Result | Result value when the task status is COMPLETED |

[Result]

| Name | Type | Description |
|-----------------------|----------|------------------------|
| inputLength           | Double   | Length of the recognized audio file (in seconds) |
| fileType              | String   | Type of the recognized audio file |
| text                  | String[] | Text conversion result of the recognized speech |
| timeslot              | List     | Section information for the text recognized at the same index |
| timeslot[0].startTime | Long     | Section start time (milliseconds) |
| timeslot[0].endTime   | Long     | Section end time (milliseconds) |
| confidence            | Double[] | Confidence of the text recognition result at the same index |

<a id="retry"></a>
### Retry { #retry }
- Requests a retry for a failed task.

[URI]

| Method | URI |
|-----|---------------------------------------------------------------------------------------|
| GET | https://api-speech.nhncloudservice.com/v2.1/appkeys/{appKey}/stt/async/{taskId}/retry |

[Fields]

| Name | Type | Required | Description |
|--------|--------|-------|-------------------------------|
| taskId | String | Required | Task UUID received after calling the asynchronous voice recognition API |

<a id="retry-response"></a>
#### Response

[Response Body]

```
{
	"header": {
		// omitted
	},
	"result": {
		"taskId": "c337256d-b17e-42ce-9f63-a792a05ae0ef"
	}
}
```
