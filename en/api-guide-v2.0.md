<!-- machine_translated: true -->

<a id="ai-service-speech-to-text-api-guide"></a>
## AI Service > Speech to Text > API Guide { #ai-service-speech-to-text-api-guide }

Speech to Text API v2.0 provides richer speech recognition results.
Speech to Text API v2.0 significantly improves the response structure of previous versions, providing more precise information needed for various post-processing tasks and user experience enhancements.

<a id="api-common-information"></a>
## API Common Information { #api-common-information }

<a id="preliminary-preparation"></a>
### Preliminary Preparation { #preliminary-preparation }

To use the Speech to Text API, you need an Appkey or a Project Integrated Appkey.<br/>
An Appkey is a unique authentication key issued for each service in NHN Cloud, and a Project Integrated Appkey is a common authentication key that can be used across multiple services within a single NHN Cloud project.<br/>
For more information on checking and using Appkeys, see [Appkey](/nhncloud/en/public-api/appkey). For more information on creating and using a Project Integrated Appkey, see [Project Integrated Appkey](/nhncloud/en/public-api/project-integrated-appkey).

<a id="request-common-information"></a>
### Request Common Information { #request-common-information }

- To use the API, {secretKey} authentication is required.
- All API requests must include {secretKey} in the **Authorization** header.

[Request Header]

| Name          | Value       | Description                     |
|---------------|-------------|---------------------------------|
| Authorization | {secretKey} | Secret key issued from the console |

<a id="response-common-information"></a>
### Response Common Information { #response-common-information }

- The API responds with **200 OK** to all API requests. For more information on the response results, see Response Body Header.

[Success Response Body]

```
{
    "header": {
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "Success"
    }
}
```

[Failure Response Body]
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

| Name          | Type    | Description                                                          |
|---------------|---------|----------------------------------------------------------------------|
| isSuccessful  | Boolean | Whether the analysis API succeeded                                   |
| resultCode    | Integer | Result code                                                          |
| resultMessage | String  | Result message (SUCCESS on success, error details on failure) |

<a id="voice-recognition-api"></a>
## Voice Recognition API { #voice-recognition-api }

<a id="voice-recognition"></a>
### Voice Recognition { #voice-recognition }
- Extracts speech data from an audio file in text format.

[URI]

| Method | URI                                                              |
|--------|------------------------------------------------------------------|
| POST   | https://api-speech.nhncloudservice.com/v2.0/appkeys/{appKey}/stt |

[Request Body]

- Include the binary data of the voice file.
- Based on the values entered in the user word list (biasingList), words recognized as "차단계" are replaced with "차단기", and words recognized as "안전 운행" are replaced with "안전운행".

```
curl -X POST 'https://api-speech.nhncloudservice.com/v2.0/appkeys/{appKey}/stt' \
-F 'audio=@sample.mp3' \
-F 'biasingList="차단기_차단계"' \
-F 'biasingList="안전운행_안전 운행"' \ 
-H 'Authorization: ${secretKey}'
```

[Fields]

| Name        | Type                | Required | Description                                                                                                                                                                                                                      |
|-------------|---------------------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| audio       | multipart/form–data | Required | Voice file (WAV, WebM, MP3, OGG, FLAC, AAC, AC3)                                                                                                                                                                                |
| biasingList | String[]            | Optional | A parameter that helps prioritize recognition or replacement of specific words or phrases. Use this to correct expected misrecognition results or to reinforce specific keywords. Each item is formatted as **"correct_value_model_recognized_value"**. |

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
        "inputLength": 220.0,
        "fileType": "mp3float",
        "text": [
            "This is an example response text",
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

| Name                  | Type     | Description                                              |
|-----------------------|----------|----------------------------------------------------------|
| inputLength           | Double   | Length of the recognized voice file (in seconds)         |
| fileType              | String   | File type of the recognized voice file                   |
| text                  | String[] | Text conversion result of the recognized speech          |
| timeslot              | List     | Section information where the text at the same index was recognized |
| timeslot[0].startTime | Long     | Section start time (milliseconds)                        |
| timeslot[0].endTime   | Long     | Section end time (milliseconds)                          |
| confidence            | Double[] | Confidence of the text recognition result at the same index |


<a id="voice-recognition-api-asynchronous"></a>
## Voice Recognition API (Asynchronous) { #voice-recognition-api-asynchronous }

<a id="voice-recognition-asynchronous"></a>
### Voice Recognition (Asynchronous) { #voice-recognition-asynchronous }
- Extracts speech data from an audio file in text format (asynchronous).

[URI]

| Method | URI                                                                    |
|--------|------------------------------------------------------------------------|
| POST   | https://api-speech.nhncloudservice.com/v2.0/appkeys/{appKey}/stt/async |

[Request Body]

- Submit a speech recognition request by providing a downloadable URL for the audio file.
- Replace {appKey} and {secretKey} with the values obtained from the console.
- Based on the values entered in the user word list (biasingList), words recognized as "차단계" are replaced with "차단기", and words recognized as "안전 운행" are replaced with "안전운행".

```
curl -X POST 'https://api-speech.nhncloudservice.com/v2.0/appkeys/{appKey}/stt/async' \
-H 'Authorization: {secretKey}' \
-H 'Content-Type: application/json' \
--data '{"audioUrl": "https://url/to/audioFile", "biasingList": ["차단기_차단계", "안전운행_안전 운행"]}'
```

[Fields]

| Name        | Type     | Required | Description                                                                                                                                                                                                                      |
|-------------|----------|----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| audioUrl    | String   | Required | Downloadable voice file URL (WAV, WebM, MP3, OGG, FLAC, AAC, AC3) with a maximum size of 150 MB                                                                                                                                  |
| biasingList | String[] | Optional | A parameter that helps prioritize recognition or replacement of specific words or phrases. Use this to correct expected misrecognition results or to reinforce specific keywords. Each item is formatted as **"correct_value_model_recognized_value"**. |

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

| Name   | Type   | Description                                                   |
|--------|--------|---------------------------------------------------------------|
| taskId | String | Task UUID that can be used to request status checks and retries |


<a id="check-status"></a>
### Check Status { #check-status }
- Retrieves the current status of the requested task.

[URI]

| Method | URI                                                                                    |
|--------|----------------------------------------------------------------------------------------|
| GET    | https://api-speech.nhncloudservice.com/v2.0/appkeys/{appKey}/stt/async/{taskId}/status |

[Fields]

| Name   | Type   | Required | Description                                              |
|--------|--------|----------|----------------------------------------------------------|
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
        "inputLength": 220.0,
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

| Name       | Type   | Description                                                        |
|------------|--------|--------------------------------------------------------------------|
| taskId     | String | Task UUID for which the status was requested                       |
| taskStatus | String | Current status of the task (PENDING, IN_PROGRESS, COMPLETED, FAILED) |
| result     | Result | Result value when the task status is COMPLETED                     |

[Result]

| Name                  | Type     | Description                                              |
|-----------------------|----------|----------------------------------------------------------|
| inputLength           | Double   | Length of the recognized voice file (in seconds)         |
| fileType              | String   | File type of the recognized voice file                   |
| text                  | String[] | Text conversion result of the recognized speech          |
| timeslot              | List     | Section information where the text at the same index was recognized |
| timeslot[0].startTime | Long     | Section start time (milliseconds)                        |
| timeslot[0].endTime   | Long     | Section end time (milliseconds)                          |
| confidence            | Double[] | Confidence of the text recognition result at the same index |

<a id="retry"></a>
### Retry { #retry }
- Requests a retry for a failed task.

[URI]

| Method | URI                                                                                   |
|--------|---------------------------------------------------------------------------------------|
| GET    | https://api-speech.nhncloudservice.com/v2.0/appkeys/{appKey}/stt/async/{taskId}/retry |

[Fields]

| Name   | Type   | Required | Description                                              |
|--------|--------|----------|----------------------------------------------------------|
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
