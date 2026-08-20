<!-- machine_translated: true -->

<a id="foundry.api.guide"></a>

## Machine Learning > NHN Cloud Foundry > API Guide { #foundry.api.guide }

This document describes APIs provided by NHN Cloud Foundry.

| API | Description |
| --- | --- |
| Ingest API | Ingests data into an already created data source. Provides snapshot file upload. |
| Query Recommendation API | Requests recommendation results from a created recommendation system app. |
| Recommendation Event API | Collects user response events to recommendation results. |
<a id="auth.common"></a>

## Authentication and Common Items { #auth.common }

<a id="auth.common.preparation"></a>

### Prerequisites { #auth.common.preparation }

**Appkey** and an **authentication token** are required to use the API.

- The Appkey can be found in the **URL & Appkey** menu at the top of the **Machine Learning > NHN Cloud Foundry** page in the NHN Cloud Console.
- The API uses the **gateway-public** endpoint.
- For information on how to issue an authentication token (Bearer token in the `X-NHN-Authorization` header), please refer to the [User Access Key Token](https://docs.nhncloud.com/ko/nhncloud/ko/public-api/user-access-key-token/) guide.

<a id="auth.common.request"></a>

### Common Request Information { #auth.common.request }

Required headers:

```plaintext
X-NC-APP-KEY: {appKey}
X-NHN-Authorization: Bearer {ACCESS_TOKEN}
Content-Type: application/json
```

Base URL:

```plaintext
https://{gateway-public-host}/api/v1.0
```

<a id="auth.common.response"></a>

### Common Response Information { #auth.common.response }

All API responses consist of a `header` and a `body`.

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {}
}
```

| Field | Type | Description |
| --- | --- | --- |
| header.isSuccessful | Boolean | Request success |
| header.resultCode | Integer | Result code. 0 on success, error code on failure |
| header.resultMessage | String | Result message. Returns SUCCESS on success, or error details on failure |
| body | Object/Array | Response data (varies by API) |
<a id="ingest.api"></a>

## Ingest API { #ingest.api }

The Ingest API loads data into a data source that you have already created in the console.
It provides a snapshot upload method that replaces all data in the data source with the data from an uploaded file.

!!! danger "Caution"
    The API for creating a new data source is not provided. To use the Ingest API, you must first create a data source in the console, and only FILE type data sources can be used.

<a id="ingest.snapshot"></a>

### Upload Snapshot (Upload File) { #ingest.snapshot }

Replaces **all** data in the data source with the content of the uploaded file. The upload process consists of three steps.

!!! danger "Caution"
    Uploading a snapshot replaces all data already loaded in the data source. Existing data cannot be recovered.

Upload Restriction:

- Maximum upload size: **10 GB**
- `100 MB` or less → **Single upload (SINGLE)**
- Over `100 MB` → **Multipart upload (MULTIPART)**
- Use the `formPost` field values returned in the response **as-is** in your request.

<a id="ingest.snapshot.init"></a>

#### 1. Initialize Upload (init) { #ingest.snapshot.init }

| Method | URI |
| --- | --- |
| POST | /api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/init |
Issues a temporary signed URL for directly uploading large files to storage. Returns either a single URL (SINGLE) or a multipart URL (MULTIPART) depending on the file size.

curl example:

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/init" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "fileName": "data.csv",
    "fileSize": 52428800,
    "contentType": "text/csv"
  }'
```

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| fileName | String | O | File Name. Allowed characters: letters, numbers, periods (.), underscores (_), hyphens (-) |
| fileSize | Long | O | File size (bytes). Min. 1, Max. 10 GB |
| contentType | String | X | Content-Type (default: application/octet-stream) |
Response(SINGLE):

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "uploadType": "SINGLE",
    "uploadUrl": "{upload-url}",
    "uploadId": null,
    "partSize": null,
    "parts": null,
    "expiresAt": "2025-01-20T11:00:00Z",
    "formPost": {
      "objectPrefix": "{appKey}/{dataSourceId}/snapshot/{jobId}/",
      "signature": "{SIGNATURE}",
      "expires": 1737370800,
      "maxFileSize": 10737418240,
      "maxFileCount": 1
    }
  }
}
```

Response (MULTIPART):

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "uploadType": "MULTIPART",
    "uploadUrl": null,
    "uploadId": "{appKey}/{dataSourceId}/snapshot/{jobId}/data.csv_segments/",
    "partSize": 104857600,
    "parts": [
      {
        "partNumber": 1,
        "uploadUrl": "{part-upload-url}?signature={SIG}&expires={TS}&max_file_size=104857600&max_file_count=1",
        "headUrl": "{part-head-url}?temp_url_sig={SIG}&temp_url_expires={TS}"
      }
    ],
    "expiresAt": "2025-01-20T11:00:00Z",
    "formPost": {
      "objectPrefix": "{appKey}/{dataSourceId}/snapshot/{jobId}/",
      "signature": "{SIGNATURE}",
      "expires": 1737370800,
      "maxFileSize": 104857600,
      "maxFileCount": 1
    }
  }
}
```

!!! tip "Note"
    The MULTIPART response also includes `formPost`. However, since multipart upload sends parts using the query parameters (`signature`/`expires`/`max_file_size`/`max_file_count`) of `parts[].uploadUrl`, `formPost` is provided for reference only and is not used for the actual part upload.

| Field | Description |
| --- | --- |
| body.jobId | Job ID. Used in subsequent complete / status query requests |
| body.uploadType | Upload type. SINGLE (100 MB or less) or MULTIPART (more than 100 MB) |
| body.uploadUrl | Upload URL (when uploading a single file) |
| body.uploadId | Multipart upload ID (when using multipart upload) |
| body.partSize | Part size (bytes, for multipart upload) |
| body.parts[].partNumber | Part number (starting from 1) |
| body.parts[].uploadUrl | Part upload URL |
| body.parts[].headUrl | URL for ETag retrieval (HEAD request after upload is complete) |
| body.expiresAt | URL expiration time |
| body.formPost.objectPrefix | Object prefix (path prepended to the file name) |
| body.formPost.signature | HMAC-SHA1 Signature |
| body.formPost.expires | Expiration time (UNIX timestamp) |
| body.formPost.maxFileSize | Maximum file size (bytes) |
| body.formPost.maxFileCount | Maximum number of files |
<a id="ingest.snapshot.upload.single"></a>

#### 2-A. Upload a File (100 MB or less) { #ingest.snapshot.upload.single }

Send a multipart/form-data POST request to the `uploadUrl` from the init response.
This request is sent directly to Object Storage, so no additional authentication is required (the `signature` serves as authentication).

curl example:

```bash
curl -X POST "{uploadUrl}" \
  -F "redirect=" \
  -F "max_file_size={formPost.maxFileSize}" \
  -F "max_file_count={formPost.maxFileCount}" \
  -F "expires={formPost.expires}" \
  -F "signature={formPost.signature}" \
  -F "file=@./data.csv;filename=data.csv"
```

!!! danger "Caution"
    The `file` field must be added at the **end** of the form data. On success, you will receive an HTTP `201 Created` response.

<a id="ingest.snapshot.upload.multipart"></a>

#### 2-B. Upload Large Files (More than 100MB, MULTIPART) { #ingest.snapshot.upload.multipart }

Receive the `parts[]` array from the response and upload each part.
Process each part in the following order: **(1) Upload → (2) Retrieve ETag via HEAD → (3) Collect into `partETags[]` in ascending order by `partNumber`**.

1. Split the file into chunks of `partSize` (default 100 MB).
2. For each part, parse the query parameters (`signature`, `expires`, `max_file_size`, `max_file_count`) from `parts[i].uploadUrl` and send them as multipart/form-data (field name `file`, fixed file name `part`).
3. After a successful upload, send a `HEAD` request to `parts[i].headUrl` and collect the `ETag` value from the response header.
4. When all parts are complete, build the `partETags` array in ascending order of `partNumber` and include it in the upload complete request.

Upload Part curl example:

```bash
# 1) Upload
curl -X POST "{parts[i].uploadUrl}" \
  -F "redirect=" \
  -F "max_file_size={max_file_size-from-query}" \
  -F "max_file_count={max_file_count-from-query}" \
  -F "expires={expires-from-query}" \
  -F "signature={signature-from-query}" \
  -F "file=@./part_i.bin;filename=part"

# 2) Retrieve ETag
curl -I "{parts[i].headUrl}" | grep -i '^etag:'
```

<a id="ingest.snapshot.complete"></a>

#### 3. Complete upload { #ingest.snapshot.complete }

| Method | URI |
| --- | --- |
| POST | /api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/complete |
curl example (single upload):

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/complete" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "fileName": "data.csv"
  }'
```

curl example (multipart upload):

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/complete" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "fileName": "data.csv",
    "uploadId": "{multipart-upload-id}",
    "partETags": ["etag-part1", "etag-part2", "etag-part3"]
  }'
```

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| jobId | String | O | Job ID (jobId from the INIT response) |
| fileName | String | O | File Name |
| uploadId | String | X | Multipart upload ID (required only for multipart uploads) |
| partETags | Array | X | List of ETags per part (required only for multipart upload, in partNumber order) |
Response:

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "jobId": "550e8400-e29b-41d4-a716-446655440000"
  }
}
```

| Field | Description |
| --- | --- |
| body.jobId | Job ID. Used for [Query Task Status](#ingest.snapshot.job.status) |
<a id="ingest.snapshot.cancel"></a>

#### Cancel Upload { #ingest.snapshot.cancel }

| Method | URI |
| --- | --- |
| DELETE | /api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/{jobId} |
curl example (single upload):

```bash
curl -X DELETE "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/{jobId}" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}"
```

curl example (Multipart Upload) - pass `uploadId` together as a query parameter:

```bash
curl -X DELETE "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/snapshots/{jobId}?uploadId={uploadId}" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}"
```

<a id="ingest.snapshot.job.status"></a>

#### Query Task Status { #ingest.snapshot.job.status }

| Method | URI |
| --- | --- |
| GET | /api/v1.0/data-sources/{dataSourceId}/ingest/jobs/{jobId} |
curl example:

```bash
curl "https://{gateway-public-host}/api/v1.0/data-sources/{dataSourceId}/ingest/jobs/{jobId}" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}"
```

Response:

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "jobId": "550e8400-e29b-41d4-a716-446655440000",
    "dataSourceId": "ds-001",
    "jobType": "SNAPSHOT",
    "status": "COMPLETED",
    "obsFilePath": "s3a://{bucket}/{path}/file.csv",
    "statistics": {
      "totalRecords": 10000,
      "failedRecords": 5,
      "successfulRecords": 9995,
      "successRate": 0.9995
    },
    "errorMessage": null,
    "createdDatetime": "2025-01-20T10:00:00Z",
    "startedDatetime": "2025-01-20T10:01:00Z",
    "completedDatetime": "2025-01-20T10:05:00Z",
    "modifiedDatetime": "2025-01-20T10:05:00Z"
  }
}
```

| Field | Description |
| --- | --- |
| body.jobId | Task ID |
| body.dataSourceId | Target Data Source ID |
| body.jobType | Task type. SNAPSHOT (snapshot load) or EVENT (change event) |
| body.status | Task status. Refer to the status values below |
| body.obsFilePath | OBS file path |
| body.statistics.totalRecords | Total number of records |
| body.statistics.failedRecords | Number of failed records |
| body.statistics.successfulRecords | Number of successful records |
| body.statistics.successRate | Success rate (0.0–1.0) |
| body.errorMessage | Error message (on failure) |
| body.createdDatetime | Task creation time |
| body.startedDatetime | Task start time |
| body.completedDatetime | Task completion time |
| body.modifiedDatetime | Last Updated At |
Task status (`status`) has the following values.

| Value | Description |
| --- | --- |
| UPLOADING | Uploading the file. |
| STAGED | Ready to process. |
| RUNNING | Loading data. |
| COMPLETED | The task has been completed normally. |
| FAILED | The task failed. |
<a id="recommendation.api"></a>

## Query Recommendation API { #recommendation.api }

Requests recommendation results from a created recommendation system app. If the user history is sufficient, inference is performed using a model-based approach (Normal Flow); if insufficient, an attribute-based approach (Cold Start) is used.

<a id="recommendation.api.recommend"></a>

### Recommend Request { #recommendation.api.recommend }

| Method | URI |
| --- | --- |
| POST | /api/v1.0/recommendation-apps/{appId}/recommend |
curl example:

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/recommendation-apps/{appId}/recommend" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "userId": "user_12345",
    "context": {
      "currentItemKey": "CONT0001",
      "recentlyViewed": ["CONT0010", "CONT0023"],
      "pageType": "course_detail",
      "sessionId": "session_abc123"
    },
    "options": {
      "maxRecommendations": 10
    }
  }'
```

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| userId | String | O | User ID of the recommendation target |
| context | Object | X | Request context information |
| context.currentItemKey | String | X | The key of the item that you are currently viewing |
| context.recentlyViewed | Array | X | List of recently viewed item keys |
| context.pageType | String | X | Current page type. home, course_detail, course_list, search_result, my_page |
| context.sessionId | String | X | Session ID |
| userAttributes | Object | X | User attribute information. Used for Cold Start inference. |
| userAttributes.jobCategory | String | X | Job/occupation category |
| userAttributes.interestArea | Array | X | List of areas of interest |
| userAttributes.experienceYears | Integer | X | Years of experience |
| options.maxRecommendations | Integer | X | Maximum number of recommendations (1 to 100, default: 10) |
| options.excludeItemKeys | Array | X | List of item keys to exclude from recommendations |
!!! tip "Note"
    The `userAttributes` schema may undergo changes to its collection method or field types depending on future implementation directions for Preference Elicitation.

Response:

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "body": {
    "userId": "user_12345",
    "recommendations": [
      { "itemKey": "CONT0023", "score": 0.95, "position": 1 },
      { "itemKey": "CONT0045", "score": 0.89, "position": 2 }
    ],
    "metadata": {
      "modelVersion": "v1.2.0",
      "requestId": "req_xyz789",
      "inferenceType": "normal",
      "abTestGroup": "treatment"
    }
  }
}
```

| Field | Description |
| --- | --- |
| body.userId | User ID of the requester |
| body.recommendations[].itemKey | Recommended item key |
| body.recommendations[].score | Recommendation score (0.0 to 1.0) |
| body.recommendations[].position | Recommendation rank |
| body.metadata.modelVersion | Model version used |
| body.metadata.requestId | Request tracking ID. Use this value when sending recommendation event API requests. |
| body.metadata.inferenceType | Inference type. normal (history-based) or cold_start (property-based) |
| body.metadata.abTestGroup | A/B test group. treatment, control, none |
<a id="recommendation.event.api"></a>

## Recommendation Event API { #recommendation.event.api }

Collects events representing user interactions (such as clicks) with recommendation results. You can analyze the recommendation success rate using the loaded event data.

<a id="recommendation.event.api.send"></a>

### Send Recommendation Events { #recommendation.event.api.send }

| Method | URI |
| --- | --- |
| POST | /api/v1.0/recommendation-apps/{appId}/events |
curl example:

```bash
curl -X POST "https://{gateway-public-host}/api/v1.0/recommendation-apps/{appId}/events" \
  -H "X-NC-APP-KEY: {appKey}" \
  -H "X-NHN-Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: application/json" \
  -d '{
    "eventType": "CLICK",
    "requestId": "req_xyz789",
    "itemKey": "CONT0023",
    "userId": "user_12345",
    "context": {
      "sessionId": "sess_abc",
      "placement": "home_main"
    }
  }'
```

`requestId`, `itemKey`, and `userId` are the values received from the recommendation query API response and must be passed as-is.

| Field | Required | Description |
| --- | --- | --- |
| eventType | O | Event type. You can define this freely (for example, CLICK, PURCHASE, IMPRESSION). Only English letters, numbers, and underscores are allowed (^[A-Za-z0-9_]+$), up to 64 characters. Case-insensitive; stored in uppercase. REQUEST and RESPONSE are reserved words and cannot be used. |
| requestId | O | The `body.metadata.requestId` value from the recommendation API response (opaque string, up to 128 characters) |
| itemKey | O | itemKey of the recommended item that the user interacted with |
| userId | X | Value of body.userId from the recommendation API response |
| context | X | Additional event information (free-form key-value. Example: display position, placement) |
| userAttributes | X | User attribute information (free-form key-value) |
| options | X | Additional options (free-form key-value pairs) |
The success response (200) returns only the `header`.

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  }
}
```

!!! tip "Note"
    - A success response (200) means the collection pipeline has received the event; it does not guarantee that the data has been loaded into the analytics table.
    - After an event API request, it may take up to 10 minutes for the data to be loaded into the dataset.
    - If you retry after a timeout, the same event may be loaded into the dataset more than once. Consider deduplication when performing analysis.