<!-- machine_translated: true -->

## Data & Analytics > Log & Crash Search > API Guide

### Appkey and SecretKey

AppKey and SecretKey are required to use the Log & Crash Search API.

AppKey and SecretKey are required to use the Log & Crash Search API.

An Appkey is a unique authentication key issued for each NHN Cloud service, used to identify the service and validate API requests. A SecretKey is a private key used to control access to the API. For more information on checking and using Appkeys, please refer to the [Appkey](/nhncloud/en/public-api/appkey).

## Collect Log API

HTTP 프로토콜을 사용해 Log & Crash 수집 서버에 로그를 전송할 수 있습니다.

> - When sending logs to the Log & Crash collector server via JSON/HTTP, you must use the following address:
>     - Log & Crash: api-logncrash.nhncloudservice.com
>     - Method of Delivery: POST
>     - URI: /v2/log
>     - Content-Type: "application/json"
> - Before sending logs, make sure that you have registered a project in Log & Crash.
> - "logTime" is used by the Log & Crash system. If you use this key, it will be ignored by Log & Crash.
> - Make sure that key names do not contain spaces. For example, "UserID" and "UserID " are recognized as different keys.
> - The maximum size of a single HTTP request is 52 MB.
> - The maximum size of a single log (JSON) is 8 MB (8,388,608 bytes).

Use the JSON format as below: 

```
{
	"projectName": "__Appkey__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "This log message come from HTTP client.",
	"logSource": "http",
	"logType": "nelo2-log",
	"host": "localhost"
}
```

[Default Parameters]

```
Parameters for Log Search

projectName: string, required
	[in] App key.

projectVersion: string, required
	[in] Version. User-configurable. Contains only "A~Z, a~z, 0~9, -._".

body: string, optional
	[in] Log message.

logVersion: string, required
	[in] Log format version. "v2".

logSource: string, optional
	[in] Log source. Used for filtering in Log Search. Defaults to "http" if not defined.

logType: string, optional
	[in] Log type. Used for filtering in Log Search. Defaults to "log" if not defined.

host: string, optional
	[in] Address of the device sending the log. If not defined, the collector server automatically fills this in using the peer address.
```

[Other Parameters]

```
sendTime: string, option
	[in] The time sent by the device. Enter as a Unix timestamp.

logLevel: string, option
	[in] For Syslog events.

UserBinaryData: string, option
	[in] Displays a [Download|View] link on the log search page. Send with a base64-encoded value.

UserTxtData: string, option
	[in] Displays a [Download|View] link on the log search page. Send with a base64-encoded value.

txt*: string, option
	[in] Field names starting with txt (txtMessage, txt_description, etc.) are saved as text fields. Full text search by some character strings of a field value is available on the log search page. The field size is limited to 1 MB.

long*: long, option
	[in] Field names starting with long (longElapsedTime, long_elapsed_time, etc.) are saved as long type fields. Range search is available for long type on the log search page.

double*: double, option
	[in] Field names starting with double (doubleAvgScore, double_avg_score, etc.) are saved as double type fields. Range search is available for double type on the log search page.
```

[Custom Fields]

```
Custom field names must start with "A–Z, a–z" and can use the characters "A–Z, a–z, 0–9, -, _".

Custom field names must not duplicate the names of the basic parameters or Crash parameters listed above.

Custom fields support only exact match searches (the entire field string must match).

The length of a custom field is limited to 1 KB. If you need to send data exceeding 1 KB, or search by a partial string of the field value, you must create the field with the `txt*` prefix.
```

[Return Value]
The collector server returns the following.

```
Content-Type: application/json

{
	"header":{
		"isSuccessful":true,
		"resultCode":0,
		"resultMessage":"Success"
	}
}

isSuccessful: boolean
	[out] True for success; false for failure 
resultCode: int
	[out] 0 for success; error code for failure 

resultMessage: string
	[out] "Success" for success; error message for failure 
```

[Bulk Delivery]
Sent in the JSON array format, for bulk delivery. 

```
[
    {
        "projectName": "__Appkey__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client. (1/2)",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost"
    },
    {
        "projectName": "__Appkey__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client. (2/2)",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost"
    }
]
```

* Note
    * On the web, logs are sorted and displayed based on receive time. For bulk transfers, all logs are considered to have been received at the same time, so the order in which the user sent them is not preserved.
        * To preserve the order of logs sent in bulk, add the `lncBulkIndex` field to each log with an Integer value. The server then displays the logs in descending order based on this value.

```
[
    {
        "projectName": "__AppKey__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "first message",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost",
        "lncBulkIndex":1
    },
    {
        "projectName": "__AppKey__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "second message",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost",
        "lncBulkIndex":2
    }
]
```
        * If sent as in the above example, the server displays the messages in the following order: second message → first message.

The collector server returns each result value in JSON array format according to the order in which they were sent.

```
Content-Type: application/json

{
    "header":{
        "isSuccessful":true,
        "resultCode":0,
        "resultMessage":"Success"
    },
    "body":{
        "data":{
            "total":5,
            "errors":2,
            "resultList":[
                {"isSuccessful":true, "resultMessage":"Success"},
                {"isSuccessful":true, "resultMessage":"Success"},
                {"isSuccessful":false, "resultMessage":"LogVersion Mismatch: v1, /v2/log"},
                {"isSuccessful":false, "resultMessage":"The project(invalidProject) is not registered"},
                {"isSuccessful":true, "resultMessage":"Success"}
            ]
        }
    }
}

total: int
    [out] Total number of logs sent

errors: int
    [out] Number of errors among the logs sent

resultList: array
    [out] Result values for each log sent
```

### Samples

[When log is normally sent with curl]

```
//Send logs using the POST method
$ curl -H "content-type:application/json" -XPOST 'https://api-logncrash.nhncloudservice.com/v2/log' -d '{
	"projectName": "__appkey__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http"
}'
```

[When it fails in log delivery]

```
//When the URL is incorrect (log -> loggg)
$ curl -v -H 'content-type:application/json' -XPOST "api-logncrash.nhncloudservice.com/v2/loggg" -d '{
	"projectName": "__appkey__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http"
}'


//When an invalid field key is used (_xxx)
$ curl -v -H 'content-type:application/json' -XPOST "api-logncrash.nhncloudservice.com/v2/log" -d '{
	"projectName": "__appkey__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http",
	"_xxx": "this is a invalid key"
	}'
Custom keys must contain "A–Z, a–z, 0–9, -_" and must start with a letter.
```

[When bulk-sending logs using curl]

```
//Send logs using the POST method
$ curl -H "content-type:application/json" -XPOST 'https://api-logncrash.nhncloudservice.com/v2/log' -d '[
    {
        "projectName": "__appkey__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client, and it is a simple bulk sample. (1/2)",
        "logSource": "http",
        "logType": "nelo2-log"
    },
    {
        "projectName": "__appkey__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client, and it is a simple bulk sample. (2/2)",
        "logSource": "http",
        "logType": "nelo2-log"
    }
]'
```

## Log Search API

> [Caution] This API is scheduled to be discontinued. We recommend that you use the [v3 Log Search API](#v3-로그-검색-api) below for new development.

Saved logs can be searched using Lucene queries.<br>
The log search API limits the amount of requests per hour according to user pattern. The resources available while searching are represented as tokens, and some of them are deducted whenever the search API is called. The API is available for use as long as the number of remaining tokens is a positive number.<br>
The number of tokens deducted when searching an item varies depending on the search duration, size, and the complexity of a query. Tokens are automatically replenished over time.<br>

![lncs-api-01-20230925](https://static.toastoven.net/prod_logncrash/lncs-api-01-20230925.png)

### Basic Information

```
API Endpoint: https://api-lncs-search.nhncloudservice.com
```
```
Only logs created in the past 90 days can be searched. The range of start time and end time cannot exceed 31 days.
```

### Search API

You can view logs within the specified time frame using the Lucene query. There is no limit on the search results (`totalItems`), but the range that can be viewed with paging is up to 100,000 logs (`pageNumber × pageSize ≤ 100,000`). To retrieve more logs, use the Search API (Cursor pagination) or the Scroll API.
```
POST /api/v2/search/{appkey}

Content-Type: application/json
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O | 

#### Request Header

| Name | Format | Description             | Required |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | Project SecretKey | O |

#### Request Body

| Name | Format | Description | Required | Note |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageNumber | Number | Page number |  | Default value 0 |
| pageSize | Number | Page size |  | Min 10, Max 100. |
| sort | Object | Sort by |  | Set ascending (ASC) and descending (DESC) by field |

<details>
<summary>Example</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2021-01-01T10:00:00+09:00",
  "to": "2021-01-01T11:00:00+09:00",
  "pageSize": 10,
  "pageNumber": 1,
  "sort": {
      "projectVersion": "asc"
  }
}
```
</details>

#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| totalItems | Body | Number | Number of logs |
| pageNumber | Body | Number | Page number |
| pageSize | Body | Number | Page size |
| data | Body | List | Log list |

<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 50,
        "pageNumber": 1,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>


### Search API (Cursor Pagination)

By specifying the URL query parameter `?cursor` at the same endpoint as the Search API and opting in, you can use cursor (search_after)-based pagination. Even when navigating to deep pages, you can sequentially retrieve the next page without being affected by the result window limit of `pageNumber × pageSize` (100,000 records for the default Search API).

```
POST /api/v2/search/{appkey}?cursor

Content-Type: application/json
```

> - Cursor pagination is activated when the URL query parameter `?cursor` or `?cursor=true` is specified. If not opted in, the existing Search API behavior is preserved.
> - When cursor is opted in, `pageNumber` cannot be sent at the same time (a 400 response is returned if both are specified). Leave `cursor` empty for the first page request, and for subsequent pages, pass the `nextCursor` value from the previous response directly to the `cursor` field of the next request.
> - The `cursor` value is an opaque string that encodes the server's internal sort state. Do not parse or modify it on the client side.
> - The page size limit per call (`pageSize` maximum value of 100) applies in the same way as the regular Search API.
> - When the last page is reached, the `nextCursor` field is not included in the response body.

#### Request Parameter

| Name | Location | Format | Description | Required |
| --- | --- | --- | --- | --- |
| appkey | Path | String | Project appkey | O |
| cursor | Query | - | Opt-in flag for cursor-based pagination. Activated when `?cursor` or `?cursor=true` is specified. | O |
#### Request Header

| Name | Format | Description | Required |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | Project SecretKey | O |
#### Request Body

| Name | Format | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO 8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | Date in ISO 8601 format (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort by |  | Set ascending (ASC) and descending (DESC) by field |
| cursor | String | Cursor for retrieving the next page |  | Omitted on the first page. For subsequent pages, pass the `nextCursor` value from the previous response as-is. Cannot be used together with `pageNumber` (400) |
<details>
<summary>Example</summary>

First page request (`cursor` not specified):

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2021-01-01T10:00:00+09:00",
  "to": "2021-01-01T11:00:00+09:00",
  "pageSize": 10,
  "sort": {
      "logTime": "desc"
  }
}
```

Next page request (pass the `nextCursor` from the previous response as-is):

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2021-01-01T10:00:00+09:00",
  "to": "2021-01-01T11:00:00+09:00",
  "pageSize": 10,
  "sort": {
      "logTime": "desc"
  },
  "cursor": "g2VleUlkLi4u"
}
```
</details>

#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| totalItems | Body | Number | Number of logs |
| pageSize | Body | Number | Page size |
| data | Body | List | Log list |
| nextCursor | Body | String | Cursor for retrieving the next page. Included only when there are more results; not included on the last page |
<details>
<summary>Example</summary>

When the next page exists (the response includes `nextCursor`):

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 50,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ],
        "nextCursor": "g2VleUlkLi4u"
    }
}
```

When this is the last page (the response does not include `nextCursor`):

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 50,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Scroll Start API

Searches all the logs within the specified time frame using the Lucene query without pages specified. It can be used with Scroll Continue API to search logs multiple times.
```
POST /api/v2/search/scroll/{appkey}

Content-Type: application/json
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O | 

#### Request Header

| Name | Format | Description             | Required |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | Project SecretKey | O |

#### Request Body

| Name | Format | Description | Required | Note |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | Page size |  | Min 10, Max 100. |
| sort | Object | Sort by |  | Set ascending (ASC) and descending (DESC) by field |

<details>
<summary>Example</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2021-01-01T10:00:00+09:00",
  "to": "2021-01-01T11:00:00+09:00",
  "pageSize": 10,
  "sort": {
      "projectVersion": "asc"
  }
}
```
</details>

#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | Number of logs |
| pageSize | Body | Number | Page size |
| data | Body | List | Log list |

<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "scrollKey": "51482f39-d499-394d-adca-462585a477e9",
        "totalItems": 60,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>


### Scroll Continue API

Continues searching logs by specifying the Scroll Key obtained from Scroll Start API or the previously called Scroll Continue API.<br>
Scroll Key is valid for 1 minute.
```
POST /api/v2/search/scroll/{appkey}/{scrollKey}

Content-Type: application/json
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |
| scrollKey | String | Scroll Key | O |

#### Request Header

| Name | Format | Description             | Required |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | Project SecretKey | O |

#### Request Body

Scroll Continue API does not require the request body.

#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | Number of logs |
| data | Body | List | Log list |

<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "scrollKey": "51482f39-d499-394d-adca-462585a477e9",
        "totalItems": 60,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Available Token API

Retrieves the number of available tokens.
```
GET /api/v2/search/available-tokens/{appkey}
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |

#### Request Header

| Name | Format | Description             | Required |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | Project SecretKey | O |

#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| availableToken | Body | Number | Available tokens |

<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "availableToken": 9875
    }
}
```
</details>
## Log Search API v3

Saved logs can be searched using Lucene queries, and this service provides Symbol file upload, retrieval, and deletion features for crash analysis.<br>
The log search API limits the amount of requests per hour according to user pattern. The resources available while searching are represented as tokens, and some of them are deducted whenever the search API is called. The API is available for use as long as the number of remaining tokens is a positive number.<br>
The number of tokens deducted when searching an item varies depending on the search duration, size, and the complexity of a query. Tokens are automatically replenished over time.<br>

### Authentication

API calls and authentication are supported using User Access Key tokens.<br>
For information on how to issue a token, see the link below.

[User Access Key Token](https://docs.nhncloud.com/en/nhncloud/ko/public-api/user-access-key-token/)

#### HTTP Header of API Request Examples

```
X-NHN-Authorization: Bearer {Access Token}
```

### Search API

You can view logs within the specified time frame using the Lucene query. There is no limit on the search results (`totalItems`), but the range that can be viewed with paging is up to 100,000 logs (`pageNumber × pageSize ≤ 100,000`). To view more logs than that, use the Cursor Search API or Scroll API.
```
POST /v3/{appkey}/logs/search

Content-Type: application/json
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |
#### Request Header

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |
#### Request Body

| Name | Format | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO 8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | Date in ISO 8601 format (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageNumber | Number | Page No. |  | Default: 0 |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort by |  | Set ascending (ASC) and descending (DESC) by field |
<details>
<summary>Example</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2026-03-24T00:00:00+09:00",
  "to": "2026-03-24T23:59:59.999+09:00",
  "pageSize": 10,
  "pageNumber": 0,
  "sort": {
      "logTime": "DESC"
  }
}
```
</details>

#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| totalItems | Body | Number | Number of logs |
| pageNumber | Body | Number | Page No. |
| pageSize | Body | Number | Page size |
| data | Body | List | Log list |
<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 20927,
        "pageNumber": 0,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Cursor Search API

Searches logs using cursor (opaque)-based pagination.<br>
Even when navigating to deep pages, you can retrieve results sequentially without being affected by the result window limit of `pageNumber × pageSize`.

- When requesting the first page, omit `cursor` from the request body.
- When requesting the next page, pass the `nextCursor` value from the previous response as-is to the `cursor` field in the request body.
- When the last page is reached, `nextCursor` is not included in the response body.
- The `cursor` value is an opaque string that encodes the internal sort state of the backend. Do not parse or modify it on the client side.
- `pageNumber` is not used, and including it in the request body returns a 400 response.

```
POST /v3/{appkey}/logs/cursor

Content-Type: application/json
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |
#### Request Header

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |
#### Request Body

| Name | Format | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO 8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | Date in ISO 8601 format (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort by |  | Set ascending (ASC) and descending (DESC) by field |
| cursor | String | `nextCursor` value from the previous response |  | Omit when requesting the first page |
<details>
<summary>Example</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2026-03-24T00:00:00+09:00",
  "to": "2026-03-24T23:59:59.999+09:00",
  "pageSize": 10,
  "sort": {
      "logTime": "DESC"
  },
  "cursor": "g6JpdGVtc4123WsBYWKhYWOhYWQ"
}
```
</details>

#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| totalItems | Body | Number | Number of logs |
| pageNumber | Body | Number | Page number (always fixed at `0` in cursor mode, meaningless) |
| pageSize | Body | Number | Page size |
| data | Body | List | Log list |
| nextCursor | Body | String | Opaque cursor for retrieving the next page (not included on the last page) |
<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "totalItems": 20907,
        "pageNumber": 0,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ],
        "nextCursor": "ghsAAAGePyNW0XZpRnFtZm42Q31231pRcHJ2UC9MMGpR"
    }
}
```
</details>

### Scroll Start API

Searches all the logs within the specified time frame using the Lucene query without pages specified. It can be used with Scroll Continue API to search logs multiple times.
```
POST /v3/{appkey}/logs/scroll

Content-Type: application/json
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |
#### Request Header

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |
#### Request Body

| Name | Format | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO 8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | Date in ISO 8601 format (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort by |  | Set ascending (ASC) and descending (DESC) by field |
<details>
<summary>Example</summary>

```json
{
  "query": "logType:\"NORMAL\"",
  "from": "2026-03-24T00:00:00+09:00",
  "to": "2026-03-24T23:59:59.999+09:00",
  "pageSize": 10,
  "sort": {
      "logTime": "DESC"
  }
}
```
</details>

#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | Number of logs |
| pageSize | Body | Number | Page size |
| data | Body | List | Log list |
<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "scrollKey": "12345bd8-d5a3-3d42-8711-16bc225b0e59",
        "totalItems": 20943,
        "pageSize": 10,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Scroll Continue API

Continues searching logs by specifying the Scroll Key obtained from Scroll Start API or the previously called Scroll Continue API.<br>
Scroll Key is valid for 1 minute.
```
POST /v3/{appkey}/logs/scroll/{scrollKey}

Content-Type: application/json
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |
| scrollKey | String | Scroll Key | O |
#### Request Header

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |
#### Request Body

Scroll Continue API does not require the request body.

#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| scrollKey | Body | String | Scroll Key |
| totalItems | Body | Number | Number of logs |
| data | Body | List | Log list |
<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "scrollKey": "12345bd8-d5a3-3d42-8711-16bc225b0e59",
        "totalItems": 20943,
        "data": [
            {
                "logTime": 1609463102265,
                "logType": "NORMAL",
                "projectVersion": "1.0.0",
                ...
            },
            ...
        ]
    }
}
```
</details>

### Available Token API

Retrieves the number of available tokens.
```
GET /v3/{appkey}/logs/available-token
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |
#### Request Header

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| availableToken | Body | Number | Available tokens |
<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "body": {
        "availableToken": 9975
    }
}
```
</details>

### Symbol Upload API

Uploads the Symbol file for crash analysis.
```
POST /v3/{appkey}/symbols?platform={platform}&version={version}&description={description}

Content-Type: multipart/form-data
```

#### Request Parameter

| Name | Location | Format | Description | Required |
| --- | --- | --- | --- | -- |
| appkey | Path | String | Project appkey | O |
| platform | Query | String | Target platform for the Symbol (one of `iOS`, `Android`, `Android-NDK`, or `Windows`) | O |
| version | Query | String | Symbol version | O |
| description | Query | String | Symbol description (URL encoding required for special characters such as spaces) |  |
#### Request Header

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |
#### Request Body

| Name | Format | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| symbolfile | Binary | Symbol file | O | Delivers the files in the multipart/form-data format. |
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| result.data.id | Body | List | List of identifiers for the uploaded Symbol files |
<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "result": {
        "data": {
            "id": [
                "1239aaba9c74f678c6df8b8"
            ]
        }
    }
}
```
</details>

### Symbol List API

Retrieves the list of uploaded Symbol files. You can filter by `platform`/`version` values; to retrieve all records, call with both values set to `all`.
```
GET /v3/{appkey}/symbols/{platform}/{version}
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |
| platform | String | Symbol platform filter (`all` when retrieving all) | O |
| version | String | Symbol version filter (`all` for retrieving all) | O |
#### Request Header

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| result.data | Body | List | List of Symbol files |
<details>
<summary>Example</summary>

```json
{
    "header": {
        "isSuccessful": true,
        "resultMessage": "success",
        "resultCode": 0
    },
    "result": {
        "data": [
            {
                ...
            }
        ]
    }
}
```
</details>

### Symbol Delete API

Deletes a single Symbol file.
```
DELETE /v3/{appkey}/symbols/{sid}
```

#### Request Parameter

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |
| sid | String | Symbol file ID | O |
#### Request Header

| Name | Format | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |
#### Response

| Name | Type | Format | Description |
| --- | --- | --- | --- |
| header.isSuccessful | Body | Boolean | Whether the request was successful |
| header.resultCode | Body | Number | Result code |
| header.resultMessage | Body | String | Result message |
<details>
<summary>Example</summary>

```json
{
  "header": {
    "isSuccessful": true,
    "resultMessage": "success",
    "resultCode": 0
  }
}
```
</details>
