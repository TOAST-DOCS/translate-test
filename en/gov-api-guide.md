<!-- machine_translated: true -->

<!-- pre-align:aligned sig=a929413d0034 -->

## Data & Analytics > Log & Crash Search > API Guide
### Appkey and SecretKey
To use the Log & Crash Search API, you need an Appkey and a SecretKey.

An Appkey is a unique authentication key issued for each NHN Cloud service, used to identify the service and validate API requests. A SecretKey is a private key used to control access to the API.

For more information on checking and using Appkeys and SecretKeys, see [Appkey](/nhncloud/en/public-api/appkey-gov).

## Log Collection API

You can send logs to the Log & Crash collector server using the HTTP protocol.

> - When sending logs to the Log & Crash collector server via JSON/HTTP, use the following address.
>     - Log & Crash: api-logncrash.gov-nhncloudservice.com
>     - Method of Delivery: POST
>     - URI: /v2/log
>     - Content-Type: "application/json"
> - Before sending logs, make sure that you have registered a project in Log & Crash.
> - "logTime" is used by the Log & Crash system. If this key is used, it will be ignored by Log & Crash.
> - Make sure that key names do not contain spaces. For example, "UserID" and "UserID " are recognized as different keys.
> - The maximum size of a single HTTP request is 52 MB.
> - The maximum size of a single log (JSON) is 8 MB (8,388,608 bytes).

Use the following JSON format.

```
{
	"projectName": "__appkey__",
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
	[in] Appkey.

projectVersion: string, required
	[in] Version. User-definable. Contains only "A~Z, a~z, 0~9, -._".

body: string, optional
	[in] Log message.

logVersion: string, required
	[in] Log format version. "v2".

logSource: string, optional
	[in] Log source. Used for filtering in Log Search. If not defined, defaults to "http".

logType: string, optional
	[in] Log type. Used for filtering in Log Search. If not defined, defaults to "log".

host: string, optional
	[in] Address of the device sending the log. If not defined, the collector server automatically fills this in using the peer address.
```

[Other Parameters]

```
sendTime: string, optional
	[in] Time sent by the device. Enter as a Unix timestamp.

logLevel: string, optional
	[in] For Syslog events.

UserBinaryData: string, optional
	[in] Displays a [Download|View] link on the log search page. Send the value encoded in base64.

UserTxtData: string, optional
	[in] Displays a [Download|View] link on the log search page. Send the value encoded in base64.

txt*: string, optional
	[in] Field names starting with txt (txtMessage, txt_description, etc.) are saved as text fields. Full text search by some character strings of a field value is available on the log search page. Field size is limited to 1 MB.

long*: long, optional
	[in] Field names starting with long (longElapsedTime, long_elapsed_time, etc.) are saved as long type fields. Range search for long type is available on the log search page.

double*: double, optional
	[in] Field names starting with double (doubleAvgScore, double_avg_score, etc.) are saved as double type fields. Range search for double type is available on the log search page.
```

[Custom Fields]

```
Custom field names must start with "A–Z, a–z" and can contain the characters "A–Z, a–z, 0–9, -, _".

Custom field names must not duplicate the names of the basic parameters or Crash parameters listed above.

Custom fields support only exact match searches (the entire field string must match).

The length of a custom field is limited to 1 KB. If you need to send data exceeding 1 KB, or if you need to search for a partial string within a field value, you must create the field with the txt* prefix.
```

[Return Values]  
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
	[out] true on success, false on failure

resultCode: int
	[out] 0 on success, error code on failure

resultMessage: string
	[out] "Success" on success, error message on failure
```

[Bulk Transfer]
To send logs in bulk, send them in JSON array format.

```
[
    {
        "projectName": "__AppKey__",
        "projectVersion": "1.0.0",
        "logVersion": "v2",
        "body": "This log message come from HTTP client. (1/2)",
        "logSource": "http",
        "logType": "nelo2-log",
        "host": "localhost"
    },
    {
        "projectName": "__AppKey__",
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
    * On the web, logs are sorted and displayed based on the time they are received. For bulk transfers, all logs in the batch are considered to have been received at the same time, so the order in which you sent them is not preserved.
        * To preserve the order of logs sent in bulk, add the `lncBulkIndex` field to each log with an Integer value. The server will then display the logs in descending order based on this value.

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
        * When sent as in the example above, the server displays the logs in the order: second message → first message.

The collector server returns the result for each log as a JSON array in the order that the logs were received.

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
    [out] Number of errors among the sent logs

resultList: array
    [out] Result values for each sent log
```

### Sample

[When logs are sent successfully using curl]

```
//Send logs using the POST method
$ curl -H "content-type:application/json" -XPOST 'https://api-logncrash.gov-nhncloudservice.com/v2/log' -d '{
	"projectName": "__appkey__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http"
}'
```

[When log sending fails]

```
//If the URL is incorrect (log -> loggg)
$ curl -v -H 'content-type:application/json' -XPOST "api-logncrash.gov-nhncloudservice.com/v2/loggg" -d '{
	"projectName": "__appkey__",
	"projectVersion": "1.0.0",
	"logVersion": "v2",
	"body": "this log message come from http client, and it is a simple sample.",
	"logSource": "http",
	"logType": "nelo2-http"
}'


//If an invalid field key is used (_xxx)
$ curl -v -H 'content-type:application/json' -XPOST "api-logncrash.gov-nhncloudservice.com/v2/log" -d '{
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

[When logs are sent in bulk using curl]

```
//POST method to send logs
$ curl -H "content-type:application/json" -XPOST 'https://api-logncrash.gov-nhncloudservice.com/v2/log' -d '[
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
API Endpoint: https://api-lncs-search.gov-nhncloudservice.com
```
```
Only logs created in the past 90 days can be searched. The range of start time and end time cannot exceed 31 days.
```

### Search API
You can view logs within the specified time frame using the Lucene query. There is no limit on search results (`totalItems`), but the range that can be viewed with paging is up to 100,000 logs (`pageNumber × pageSize ≤ 100,000`). To retrieve more logs than that, use the Search API (Cursor pagination) or the Scroll API.
```
POST /api/v2/search/{appkey}

Content-Type: application/json
```

#### Request Parameters
| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |

#### Request Headers
| Name | Format | Description | Required |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | Project SecretKey | O |

#### Request Body
| Name | Format | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageNumber | Number | Page number |  | Default: 0 |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort criteria |  | Set ascending (ASC) or descending (DESC) order per field |

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
You can use cursor (search_after)-based pagination by opting in with the URL query parameter `?cursor` at the same endpoint as the Search API. Even when navigating to deep pages, you can sequentially retrieve the next page without being affected by the result window limit of `pageNumber × pageSize` (100,000 logs for the default Search API).

```
POST /api/v2/search/{appkey}?cursor

Content-Type: application/json
```

> - Cursor pagination is activated when the URL query parameter `?cursor` or `?cursor=true` is specified. Without opt-in, the existing Search API behavior is maintained.
> - When opting in with cursor, `pageNumber` cannot be sent at the same time (a 400 response is returned if both are specified). Omit `cursor` for the first page request, and for subsequent pages, pass the `nextCursor` value from the previous response directly to the `cursor` field of the next request.
> - The `cursor` value is an opaque string that encodes the server's internal sort state. Do not parse or modify it on the client side.
> - The page size limit per call (`pageSize` maximum of 100) applies the same as with the standard Search API.
> - When the last page is reached, the `nextCursor` field is not included in the response body.

#### Request Parameters
| Name | Location | Format | Description | Required |
| --- | --- | --- | --- | --- |
| appkey | Path | String | Project appkey | O |
| cursor | Query | - | Opt-in flag for cursor-based pagination. Activated when `?cursor` or `?cursor=true` is specified | O |

#### Request Headers
| Name | Format | Description | Required |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | Project SecretKey | O |

#### Request Body
| Name | Format | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort criteria |  | Set ascending (ASC) or descending (DESC) order per field |
| cursor | String | Cursor for retrieving the next page |  | Omit on the first page request. For subsequent pages, pass the `nextCursor` value from the previous response as-is. Cannot be used together with `pageNumber` (returns 400) |

<details>
<summary>Example</summary>

First page request (without `cursor`):

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

Next page request (passing the `nextCursor` from the previous response as-is):

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
| nextCursor | Body | String | Cursor for retrieving the next page. Included only when more results exist; not included on the last page |

<details>
<summary>Example</summary>

When the next page exists (response includes `nextCursor`):

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

When on the last page (response does not include `nextCursor`):

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

#### Request Parameters
| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |

#### Request Headers
| Name | Format | Description | Required |
| --- | --- |----------------| --- |
| X-LNCS-SECRET | String | Project SecretKey | O |

#### Request Body
| Name | Format | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | ISO8601 format date (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort criteria |  | Set ascending (ASC) or descending (DESC) order per field |

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
The Scroll Key is valid for 1 minute.
```
POST /api/v2/search/scroll/{appkey}/{scrollKey}

Content-Type: application/json
```

#### Request Parameters
| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |
| scrollKey | String | Scroll Key | O |

#### Request Headers
| Name | Format | Description | Required |
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

#### Request Parameters
| Name | Format | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project appkey | O |

#### Request Headers
| Name | Format | Description | Required |
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

## v3 Log Search API

You can search stored logs using the Lucene query, and the API provides Symbol file upload, retrieval, and deletion features for crash analysis.<br>
The log search API limits the amount of requests per hour according to user pattern. The resources available while searching are represented as tokens, and some of them are deducted whenever the search API is called. The API is available for use as long as the number of remaining tokens is a positive number.<br>
The number of tokens deducted when searching an item varies depending on the search duration, size, and the complexity of a query. Tokens are automatically replenished over time.<br>

### Authentication

The API supports User Access Key tokens for API calls and authentication.<br>
For information on how to issue a token, see the link below.

[User Access Key Token](https://docs.gov-nhncloud.com/ko/nhncloud/ko/public-api/user-access-key-token/)

#### Example HTTP Header for API Requests
```
X-NHN-Authorization: Bearer {Access Token}
```

### Search API
You can view logs within the specified time frame using the Lucene query. There is no limit on the number of search results (`totalItems`), but the range that can be retrieved through paging is up to 100,000 entries (`pageNumber × pageSize ≤ 100,000`). To retrieve more logs than this limit, use the Cursor Search API or the Scroll API.
```
POST /v3/{appkey}/logs/search

Content-Type: application/json
```

#### Request Parameters
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project Appkey | O |

#### Request Headers
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |

#### Request Body
| Name | Type | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | ISO8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageNumber | Number | Page number |  | Default: 0 |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort criteria |  | Ascending (ASC) and descending (DESC) settings per field |

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
Even when navigating to deep pages, you can retrieve logs sequentially without being affected by the result window limit of `pageNumber × pageSize`.

- Omit `cursor` in the request body when requesting the first page.
- When requesting the next page, pass the `nextCursor` value from the previous response directly to the `cursor` field in the request body.
- When the last page is reached, `nextCursor` is not included in the response body.
- The `cursor` value is an opaque string that encodes the internal sort state of the backend. Do not parse or modify it on the client side.
- `pageNumber` is not used, and including it in the request body returns a 400 response.

```
POST /v3/{appkey}/logs/cursor

Content-Type: application/json
```

#### Request Parameters
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project Appkey | O |

#### Request Headers
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |

#### Request Body
| Name | Type | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | ISO8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort criteria |  | Ascending (ASC) and descending (DESC) settings per field |
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
| pageNumber | Body | Number | Page number (always fixed at `0` in cursor mode; not meaningful) |
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

#### Request Parameters
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project Appkey | O |

#### Request Headers
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |

#### Request Body
| Name | Type | Description | Required | Notes |
| --- | --- | --- | --- | --- |
| query | String | Lucene query | O |  |
| from | String | Start time | O | ISO8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| to | String | End time | O | ISO8601 date format (YYYY-MM-DDThh:mm:ss.sTZD) |
| pageSize | Number | Page size |  | Default: 10, maximum: 100 |
| sort | Object | Sort criteria |  | Ascending (ASC) and descending (DESC) settings per field |

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
The Scroll Key is valid for 1 minute.
```
POST /v3/{appkey}/logs/scroll/{scrollKey}

Content-Type: application/json
```

#### Request Parameters
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project Appkey | O |
| scrollKey | String | Scroll Key | O |

#### Request Headers
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |

#### Request Body
The Scroll Continue API does not require a request body.

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

#### Request Parameters
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| appkey | String | Project Appkey | O |

#### Request Headers
| Name | Type | Description | Required |
| --- | --- | --- | --- |
| X-NHN-Authorization | String | User Access Key token in `Bearer {Access Token}` format | O |

#### Response
| Name | Type | Format | Description |
| --- | --- | --- | --- |
| availableToken | Body | Number | Number of available tokens |

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