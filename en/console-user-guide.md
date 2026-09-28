<!-- machine_translated: true -->

<!-- pre-align:aligned sig=a160539b5f44 -->

<a id="foundry.console.guide"></a>
## Machine Learning > NHN Cloud Foundry > Console User Guide { #foundry.console.guide }

This document describes how to manage data sources, pipelines, analytics (queries, charts, and dashboards), and apps in the NHN Cloud Foundry console.

In the settings tables, the Required column indicates the following:

- `O`: Required entry
- `X`: Optional entry
- `O*`: Required or optional depending on other settings

<a id="status"></a>
## Status { #status }

Console path: **Machine Learning > NHN Cloud Foundry > Status** tab

On the Status tab, you can check the service activation status and tenant settings. Before using the service, check the activation status on this tab, and submit an activation request if the service is not yet activated.

<a id="status.activate"></a>
### Request Service Activation { #status.activate }

Service activation cannot be performed directly from the console. Contact us through [1:1 Inquiry](https://www.nhncloud.com/kr/support/inquiry) with your preferred resource size. Once the requested cluster is created, you can use the service starting from creating a data source.

The features available for each resource size are as follows:

| Value | Description |
| --- | --- |
| SMALL | Basic resources: data sources, common features, and chart queries available |
| MEDIUM | Basic resources + data pipeline additionally available |
| LARGE | Basic resources + AI apps available |
| XLARGE | All features available (data pipeline + AI apps) |

<a id="status.info"></a>
### Check Service Status { #status.info }

After activation, the Status tab displays the following information:

| Item | Description |
| --- | --- |
| Service status | Current activation status of the service |
| Tenant domain | Domain used to access the service |

- If you need to change your resource size after activation, submit a request through 1:1 Inquiry.
- While the service environment is being configured or decommissioned, the progress is displayed.
- Click the **Deactivate** button to deactivate the service.

!!! danger "Caution"
    Deactivating the service deletes all created resources, and this action cannot be undone.

<a id="datasource"></a>
## Data Source { #datasource }

Console path: **Machine Learning > NHN Cloud Foundry > Data Source** tab

A data source is the unit that stores data for analysis in NHN Cloud Foundry. You can create, view, and delete data sources in the console.

!!! danger "Caution"
    When using this service, make sure not to enter information that contains personal data.
    This service does not provide separate security measures for personal data entered by customers. Refrain from entering and storing information that contains personal data.
    This notice is also displayed as a pop-up when you enter the console. If you select **Don't show again**, it will not be displayed again in the same browser, but it will be displayed again in a different browser or different project.

<a id="datasource.list"></a>
### Data Source List { #datasource.list }

The data source list screen displays the following information.

| Column | Description |
| --- | --- |
| Type | The type of the data source |
| Data source name | The name that identifies the data source |
| Table name | The name of the table where data is stored |
| Status | The current status of the data source |
| Data volume | The number of rows of ingested data |
| Created on | The date and time the data source was created |
| Details | Click the magnifying glass icon to view detailed information |

Type:

| Value | Description |
| --- | --- |
| File | A data source created from an uploaded CSV file |
| Recommendation | A data source where recommendation results are stored |
| Dataset | A data source created by a pipeline |

Status:

| Value | Description |
| --- | --- |
| INITIALIZING | The data source is being initialized |
| PROCESSING | Data is being processed |
| INGESTING | Data is being ingested |
| COMPLETED | Data source processing is complete |
| FAILED | Data source processing has failed |
| DELETING | The data source is being deleted |

For data sources of type File, the result of the most recent file upload is displayed as an icon next to the status.

| Value | Description |
| --- | --- |
| Applying | The most recently uploaded file is being applied |
| Review recommended | The most recently uploaded file has been applied, but there are items to review. Check the details in the data source detail view |
| Review required | The data source is available, but the most recently uploaded file has not been applied. Check the file and re-upload |

- Hovering over the question mark icon next to the status badge displays a status description.
- You can filter by data source name or ID using the search feature at the top.
- You can also narrow results using the column header filters for the Type, Data source name, Table name, and Status columns.
- You can adjust the number of items displayed per page (10, 20, or 50 items; default is 10).

!!! tip "Note"
    Items of type Recommendation and Dataset cannot be created directly by users. Recommendation data sources are created automatically when a recommendation system app is created, and Dataset data sources are created automatically when a pipeline runs.

<a id="datasource.create"></a>
### Create a Data Source { #datasource.create }

Click the **Create data source** button to open the creation modal.

<a id="datasource.create.basic"></a>
#### Basic Settings { #datasource.create.basic }

| Item | Required | Description |
| --- | --- | --- |
| Data source name | O | Korean, Japanese, English, numbers, spaces, -, _ allowed (between 1 and 64 characters) |
| Table name | O | Lowercase English letters, numbers, and _ allowed (between 1 and 64 characters). Cannot start with a number; SQL reserved words not allowed |
| Description | X | A description of the data source |

Data source names and table names that are already in use cannot be used.

<a id="datasource.create.detail"></a>
#### Advanced Settings { #datasource.create.detail }

| Item | Required | Description |
| --- | --- | --- |
| CSV file | X | Select the CSV file to upload using the **Select File** button (up to 100 MB) |
| Header settings | X | When **First row is the header** is checked, the first row of the CSV is used as column names |
| Primary key field | X | Specify the column to use as the row identifier from the dropdown |
| Schema | O | Define the field names and types for the data |

Specify the primary key field as follows:

- When you select a CSV file, a dropdown is automatically created with the first column selected. Click the dropdown to change to a different column.
- Click the **Add primary key** button to add another dropdown and specify two or more columns as a composite key. Columns already selected will not appear as options in other dropdowns.
- If all dropdowns are cleared, no primary key will be specified.
- For files without a header, columns are displayed with their sequence number and the value from the first data row.

Enter the schema using one of the following methods:

- Type inference: After selecting a CSV file, click the **Infer types** button to infer column types from a sample of up to 1,000 rows at the beginning of the CSV and populate the schema input fields. Correct any incorrectly inferred types manually.
- Table edit: Click the **Add field** button to add rows, then specify the field name and type for each row. The Remarks column displays any items from the type inference results that require review.
- JSON edit: Click the **Edit directly as JSON** button and enter a JSON array in the format shown below.

Schema JSON format example:

```json
[
  { "fieldName": "hostname", "fieldType": "string" },
  { "fieldName": "portName", "fieldType": "string" },
  { "fieldName": "trafficIn", "fieldType": "double" },
  { "fieldName": "eventTimestamp", "fieldType": "timestamp" }
]
```

Supported field types:

| Value | Description |
| --- | --- |
| boolean | Boolean |
| int | Integer (32-bit) |
| long | Integer (64-bit) |
| float | Float (32-bit) |
| double | Double (64-bit) |
| string | String |
| timestamp | Timestamp |
| datetime | Date and time (YYYY-MM-DD HH:MM:SS) |
| date | Date |
| array | Array (default) |
| array&lt;double&gt; | Double array |
| array&lt;int&gt; | Int array |
| array&lt;string&gt; | String array (for recommendation models) |
| array&lt;float&gt; | Float array (for recommendation models) |

!!! danger "Caution"
    The reserved field name `system_eventTimestamp` cannot be used.

After completing the settings, click the **Add** button to create the data source.

<a id="datasource.create.detail.prometheus"></a>
#### Prometheus API Detailed Settings { #datasource.create.detail.prometheus }

The Prometheus API type has a fixed record format sent by the collection API, so you don't enter the schema directly. The fixed schema below is displayed as a read-only table in the schema field of basic settings, and a table is created with this schema as-is.

| Field Name | Data Type | Description |
| --- | --- | --- |
| timestamp | timestamp | Metric timestamp. Millisecond epoch |
| value | double | Measured value |
| labels | array&lt;struct&gt; | All labels attached to the metric |
| labelHash | string | Automatically calculated series identifier |
| groupHash | string | Automatically calculated group identifier |
| metadata | map | Additional information stored as sent |

System columns `eventTimestamp`, `ingestTimestamp` are automatically added.

In detailed settings, you specify the following two items:

| Item | Required | Description |
| --- | --- | --- |
| Series Identification Label | O | Specify how to distinguish one time series by what label combinations. Choose between **Use All Labels** or **Specify Directly**, with the default being **Use All Labels** |
| Group Label | X | Unit to manage time series by grouping them. Time series with the same specified label values become one group. If left empty, the entire data source becomes one group. |

- Series Identification Label: Training and inference are performed separately for each time series. **Use All Labels** treats different label combinations as different time series. **Specify Directly** groups only data with the same specified label values as one time series and does not use other labels for differentiation.
- Group Label: For example, if you specify a rule ID label, one group is created for each rule value. If left empty, the entire data source becomes one group. A group is registered only when metrics are received.
- Label names must start with a letter or underscore (`_`) and can only use letters, numbers, and underscores (`_`). Enter multiple labels separated by commas, and you cannot enter the same label twice.
- If you **Specify Directly** for the Series Identification Label but the Group Label is not in that list, a warning is displayed. Because time series can be merged even if they belong to different groups, we recommend including the Group Label in the Series Identification Label.

Below the Group Label, the **View Example** row displays how the example metric is divided into several series and groups based on the entered label settings in the format 'N series·M groups'. If the Group Label is left empty, it displays 'One group·The entire data source is one group'.

- Click **View Example** and a table showing series divided by group and a request body example expands. If you click a row in the table, the request body example changes to the labels of that series.
- If you **Specify Directly** for the Series Identification Label and multiple metrics are merged into one series, the merged count is displayed together.
- If you change the input, it is recalculated immediately.

Click the **Add** button and the completion window displays the data source readiness status and the **Collection Method** (endpoint, request headers, request body example, and rules). When it changes to 'Ready', you can send metrics using the guided method.

!!! tip "Note"
    For how to send data to the Prometheus API data source, see the **Collection Method** tab in the data source creation completion window, View Details, or 'Collecting metrics' in [API Guide](../api-guide/#metrics.ingest.api).

<a id="datasource.delete"></a>
### Delete a Data Source { #datasource.delete }

Select the data sources to delete using the checkboxes in the list, then click the **Delete** button.

- Deleting a data source also deletes the table and all ingested data.
- You cannot delete a data source if a data loading task or another task is in progress. Try again after the task completes.

- You cannot delete a data source in use by an app or data pipeline. Delete the associated app or data pipeline first.
- Deleting an app does not delete the inference result data source. If needed, delete it separately from the Data Source List.

<a id="datasource.detail"></a>
### View Details / Preview { #datasource.detail }

- **Details** (magnifying glass icon): View information about the data source.
- **Preview** (⌄ icon): Preview the ingested data in table format.

The Details view consists of the following tabs.

| Tab | Description |
| --- | --- |
| Connection info | Data source ID, data source name, table name, type, description, and status |
| Catalog | View the list of field names and data types, and **Add field** |

| Event Settings | Displayed only for data sources of file type. Check and toggle the Event API activation status. |
| Collection Method | Displayed only for data sources of Prometheus API type. Instructions for sending metrics. |

Data sources of type Prometheus API display **Series Identification Label** and **Group Label** together in the Connection Information tab. If no value is specified, they are displayed as 'use all labels' and 'single group (entire data source)' respectively. If multiple different values for the same time series are received within any 1-minute period in the recent 5 minutes, this is also displayed in the Connection Information tab.

<a id="datasource.detail.ingest"></a>
#### Collection method { #datasource.detail.ingest }

This guide describes how to send metrics to a data source of type Prometheus API. Each item can be copied using the **Copy** button.

| Item | Description |
| --- | --- |
| Endpoint | API path for sending metrics |
| Request Header | The `X-NC-APP-KEY` header populated with this data source's app key and the `X-NHN-Authorization` header for the authentication token |
| Request Body Example | Request body example with this data source's group label applied |
| Rules | Authentication token, time unit, transmission interval, labels, additional information, values, and response notes |

The same content is also displayed in the completion window immediately after creating the data source.

!!! danger "Caution"
    You must insert the issued authentication token in the token field of the `X-NHN-Authorization` header. If you send only the app key, the request will be rejected.

For the detailed request format, see 'Metric Collection' in the [API Guide](../api-guide/#metrics.ingest.api).

<a id="datasource.edit"></a>
### Update Data { #datasource.edit }

The data source name and table name cannot be changed after creation. You can update ingested data by uploading a new CSV file, and you can add new fields.

<a id="datasource.edit.csv"></a>
#### Edit Data with CSV { #datasource.edit.csv }

In the list, click **Edit with CSV** from the more options (⋯) menu in the row of a data source of type File.

1. Review the existing column list.
2. Click the **Select File** button to select a new CSV file (up to 100 MB).
3. Check the preview and review notes for the selected file.
4. Click the **Overwrite** button to start the upload. You can track the progress on the list screen.

Upload is restricted in the following cases.

| Situation | Guidance |
| --- | --- |
| The number of columns in the file exceeds the number of existing columns | Add fields to the catalog first, then re-upload |
| The file contains columns not in the catalog | Add fields to the catalog first, then re-upload |
| The header setting does not match the first row of the file | Upload a file that includes a column header row, or change the header setting in the data source |

<a id="datasource.edit.field"></a>
#### Add a Field { #datasource.edit.field }

Click the **Add field** button in the **Catalog** tab of the Details view.

| Item | Required | Description |
| --- | --- | --- |
| Field name | O | Must start with a letter or underscore (_); only letters, numbers, and _ allowed |
| Type | O | Select from the supported field types in the schema |
| Description | X | A description of the field |

- You can add up to 20 fields at a time using the **Add row** button.
- System-reserved field names and field names that already exist cannot be used.

!!! tip "Note"
    You can update data not only through the console but also via the API. For details, see the 'Ingest API' section in the [API guide](../api-guide/#ingest.api).

<a id="pipeline"></a>
## Pipeline { #pipeline }

Console path: **Machine Learning > NHN Cloud Foundry > Pipeline** tab

A pipeline processes data from a data source through a workflow of connected nodes, transforming it into an analyzable dataset.

<a id="pipeline.list"></a>
### Pipeline List { #pipeline.list }

When you enter the pipeline menu, the list of created pipelines is displayed in table format.

| Column | Description |
| --- | --- |
| Checkbox | Pipeline selection |
| Enabled | Icon indicating whether it is enabled |
| Pipeline Name | Name that identifies the pipeline |
| Batch Schedule | Configured schedule. Displayed as a hyphen if not configured |
| Start Date/Time | Schedule start date and time |
| End Date/Time | Schedule end date and time |
| Last Run Date | Most recent run date and time |
| Pipeline Status | Current status of the pipeline |
| Manual Run | Run button |

- Clicking a row takes you to the edit screen.
- For a running pipeline, a progress indicator appears in the Manual Run column, and the button is disabled when the pipeline cannot be run.

You can create, modify, delete, enable, and disable pipelines from the toolbar. Enable and disable options are in the **More (⋯)** menu.

<a id="pipeline.create"></a>
### Create a Pipeline { #pipeline.create }

1. On the list screen, click the **Create Pipeline** button.
2. In the **Settings** panel on the right, enter the basic information.

    | Item | Required | Description |
    | --- | --- | --- |
    | Pipeline Name | O | Name that identifies the pipeline (up to 30 characters). Korean, Japanese, English, numbers, spaces, -, and _ are allowed. |
    | Pipeline Description | X | Additional description for the pipeline (up to 255 characters) |
    | Tag | X | Tags for classification (up to 10 tags, 50 characters each) |

3. Click the **Create** button to create the pipeline in draft status.

!!! danger "Caution"
    Saving the settings of an enabled pipeline disables the pipeline. Building by clicking the Run button automatically enables it again.

<a id="pipeline.editor"></a>
### Pipeline editor { #pipeline.editor }

This is the main editing screen that you enter when creating or editing a pipeline.

- **Header**: Pipeline name, description, and back button
- **Tab bar (left)**: Run/Stop, run history, and add source node buttons
- **Tab bar (right)**: Last run date and time, status/build/activation badges, and save button
- **Editor area**: Node-edge editor (supports drag and drop and auto-layout)
- **Side panel**: Settings, schedule, and computing resources panels

<a id="pipeline.status"></a>
#### Pipeline status { #pipeline.status }

You can hover over the status badge to view a detailed description in a tooltip.

| Value | Description |
| --- | --- |
| Draft | Pipeline has been created with no nodes |
| Modified | Pipeline configuration has been changed, requiring a rebuild (run) |
| Building | Pipeline build in progress |
| Waiting | Pipeline build is complete and ready to run |
| Running | Pipeline run in progress |
| Completed | Pipeline run completed successfully |
| Failed | Pipeline run stopped or an error occurred |
| Terminated | User has stopped the pipeline run |
| Deleting | Pipeline deletion in progress |

<a id="pipeline.node"></a>
### Node configuration { #pipeline.node }

A pipeline is configured by combining the following five node types.

| Node Type | Role | Input | Output | Description |
| --- | --- | --- | --- | --- |
| Source | Data source | None | Data | Connects to an external data source |
| Transform | Data processing | Data | Transformed data | Filter, derived columns, aggregation, label encoding, etc. |
| Join | Table join | 2 inputs | Joined data | Inner/Left/Right/Full Outer/Semi/Anti joins |
| Union | Table merge | 2 inputs | Merged data | Full Merge/Intersect Merge/Left-First Merge |
| Dataset | Output table | Data | None | Saves results as a table (final node) |

Connection constraints:

- SOURCE nodes cannot have inputs connected to them (root node).
- DATASET nodes cannot have outputs connected to them (final node).
- Circular references (loops) and self-connections are not allowed.

!!! danger "Caution"
    The pipeline configuration is validated when saved. All nodes must be connected in a single flow (disconnected nodes are not allowed), and the last node in the flow must be exactly one DATASET node.

<a id="pipeline.node.source"></a>
#### Add source node { #pipeline.node.source }

1. Click the **Add Source Node** button in the tab bar.
2. A list of available data sources is displayed in a modal.
3. Select the desired source to add it.

| Value | Description |
| --- | --- |
| FILE | CSV file data source |
| Recommendation | Recommendation result store |
| Dataset | Data generated by a Dataset node in a pipeline. Can be reused as input for other pipelines. |

<a id="pipeline.node.transform"></a>
#### Transform node (TRANSFORM) { #pipeline.node.transform }

Each transform operation requires a node name (up to 30 characters; Korean, Japanese, English, numbers, spaces, `-`, and `_` are allowed). Adding multiple transform operations to a single node creates nodes connected in sequence.

The following transform methods are supported:

| Category | Method | Description |
| --- | --- | --- |
| Row (row-level operations) | Filter | Extracts only rows that match the condition |
| Row (row-level operations) | Explode | Splits a delimited string into separate rows |
| Row (row-level operations) | Derive | Creates derived columns using allowlisted functions |
| Aggregation (aggregation operations) | Aggregate | Grouping and aggregation |
| Window (window operations) | Rank Top N | Global sort + top N rows |
| Column (column operations) | Label Encode FIT | Creates a category-to-integer mapping table |
| Column (column operations) | Label Encode Apply | Applies encoding using a mapping table |
| LLM (LLM-based operations) | Classify | Classifies text into categories using an LLM |

<a id="pipeline.node.transform.filter"></a>
##### Filter { #pipeline.node.transform.filter }

| Value | Description | Example |
| --- | --- | --- |
| = | Equal | field = 'value' |
| ≠ | Not equal | field ≠ 'value' |
| > | Greater than | field > 100 |
| ≥ | Greater than or equal to | field ≥ 100 |
| &lt; | Less than | field < 100 |
| ≤ | Less than or equal to | field ≤ 100 |
| LIKE | Pattern matching | field LIKE '%keyword%' |
| IN | Included in list | field IN ('a', 'b', 'c') |
| IS NULL | Is NULL | field IS NULL |
| IS NOT NULL | Is not NULL | field IS NOT NULL |

Only operators available for the selected column type are displayed.

| Column Type | Available Operators |
| --- | --- |
| String | =, ≠, LIKE, IN, IS NULL, IS NOT NULL |
| Number | =, ≠, >, ≥, &lt;, ≤, IN, IS NULL, IS NOT NULL |
| Date/Time | =, ≠, >, ≥, &lt;, ≤, IS NULL, IS NOT NULL |
| Boolean | =, ≠, IS NULL, IS NOT NULL |

The comparison value can be selected from **Direct input**, **Time (relative to now)**, **Another column**, or **Functions and Expressions**.

- Enter a constant expression in **Function/Expression**. This is used when filtering a time column stored in millisecond epoch by the current time. Example: `CAST(UNIX_TIMESTAMP(NOW() - INTERVAL 7 DAY) * 1000 AS BIGINT)`
- In **Function/Expression**, you can use only time calculation and type conversion functions, CAST target types, and INTERVAL units. Column references, quotation marks, semicolons, comments, and entries exceeding 500 characters are rejected when saved.

Logical operators `AND` and `OR` are supported. Use the **Add Group** button to nest conditions up to three levels deep.

<a id="pipeline.node.transform.explode"></a>
##### Explode { #pipeline.node.transform.explode }

Splits a delimited string column into separate rows for each token.

| Item | Required | Description |
| --- | --- | --- |
| Column to split | O | Column containing the delimited string |
| Output column name | O | Name of the column to hold each split token |
| Delimiter | O | Default is a comma (,) |
| Trim whitespace | X | When ON, removes leading and trailing whitespace from each token |
| Remove empty tokens | X | When ON, excludes empty string tokens from the output rows after splitting |
| Output type | X | STRING, BIGINT, INT, DOUBLE. Defaults to STRING if not specified. |
| Original columns to retain | X | Original columns to include in the output. If not selected, all original columns are retained. |

- The delimiter is interpreted as a regular expression, so special characters must be escaped (e.g., `\.`, `\|`).
- If an output type is specified, each split value is cast to that type. For example, if numeric IDs are comma-separated, specifying BIGINT ensures the type matches your join key.

<a id="pipeline.node.transform.derive"></a>
##### Derive { #pipeline.node.transform.derive }

Creates new columns from existing ones using provided functions. Use the **Add Derived Column** button to add multiple definitions, specifying a function and a derived column name for each.

| Value | Description | Additional Settings |
| --- | --- | --- |
| DATE_BUCKET | Date bucket (epoch ms → date in specified timezone) | Source column, timezone (e.g., Asia/Seoul) |
| JSON_ARRAY_LENGTH | Number of elements in a JSON array | Source column, element schema |
| CONCAT | Concatenates multiple columns with a delimiter | 2 or more source columns, delimiter, default value (optional) |
| RATIO | Calculates numerator/denominator ratio | Numerator, denominator, multiplier (optional, default 1), rounding decimal places (optional) |
| COALESCE | First non-null value among multiple columns | 2 or more source columns |

- Definitions are applied in order from top to bottom. A derived column created earlier can be referenced as a source column in a later definition.
- Derived column names can contain English letters, numbers, underscores (_), and Korean characters.

<a id="pipeline.node.transform.aggregate"></a>
##### Aggregate { #pipeline.node.transform.aggregate }

1. **Select grouping criteria** (optional): Groups rows that share the same value. If not selected, all data is aggregated as a single group.
2. **Define aggregation functions** (required): Specify the column to aggregate, the aggregation function, and the result column name. Multiple definitions can be added.

| Value | Description |
| --- | --- |
| COUNT | Count |
| COUNT_DISTINCT | Count of distinct values |
| SUM | Sum |
| AVG | Average |
| MIN | Minimum value |
| MAX | Maximum value |
| FIRST | First value |
| LAST | Last value |
| STDDEV | Standard deviation |
| VARIANCE | Variance |
| ARRAY_AGG | Collects group values into an array |

- For COUNT, you can select `* (all)` as the column to aggregate.
- FIRST and LAST require a sort column and direction (ascending/descending), and return the first or last value after sorting.

Selecting ARRAY_AGG adds the following settings:

| Item | Required | Description |
| --- | --- | --- |
| Array element type | O | Single column or JSON object |
| Column to collect | O* | Required when the array element type is a single column. The column to include in the array. |
| JSON object field definition | O* | Required when the array element type is a JSON object. A combination of key names and columns. |
| Array element sort | X | Sort column and direction. No sorting if not specified. |
| Output format | O | STRUCT_ARRAY, JSON_STRING_ARRAY, JSON_STRING |
| Deduplicate (DISTINCT) | X | Ignored if sort is configured. |

<a id="pipeline.node.transform.rank"></a>
##### Rank Top N { #pipeline.node.transform.rank }

Sorts all data by the specified criteria and retains only the top N rows.

| Item | Required | Description |
| --- | --- | --- |
| Sort criteria | O | Column to sort by and direction (DESC / ASC) |
| Top N rows | O | Number of rows to include in the result after sorting |
| Result rank column name | O | Name of the rank column (1 to N) added to the output |

- Use the **Add Sort Criteria** button to specify multiple criteria, which are applied as primary sort, secondary sort, and so on. You can drag to reorder them.
- Sorting by the rank column when querying preserves the original order.

<a id="pipeline.node.transform.label.encode"></a>
##### Label encoding (Label Encode FIT / Label Encode Apply) { #pipeline.node.transform.label.encode }

This feature converts categorical data to numeric (integer) values. It consists of two stages: **FIT (training)** and **APPLY (application)**. You must create the FIT node first and then reference it in the APPLY node.

FIT node settings:

| Item | Required | Description |
| --- | --- | --- |
| Select columns to encode | O | Columns to apply label encoding to (one or more) |
| Starting index | X | Starting value for encoding (default: 0) |

APPLY node settings:

| Item | Required | Description |
| --- | --- | --- |
| Select mapping table node | O | Select the FIT node |
| Overwrite original column | X | When checked, replaces the original column with the encoded value (default: unchecked) |
| Result column suffix | X | Suffix appended to the new column name when the original is retained (default: _encoded) |

!!! tip "Note"
    Values not found in the mapping table (OOV, Out-of-Vocabulary) are encoded as `-1`.

!!! danger "Caution"
    Re-running FIT may change encoding numbers depending on data changes. Be aware of compatibility issues with existing models.

<a id="pipeline.node.transform.classify"></a>
##### Classify { #pipeline.node.transform.classify }

Classifies text column values into categories using an LLM. The category list used as the classification criteria must be prepared as a separate data source node.

When the pipeline runs, input data rows are grouped into batches, and the LLM is called once per batch. Each call's prompt includes the category list and the rows in that batch. The LLM returns an appropriate category ID for each row, and the result is stored in the classification result column.

**LLM Settings**

| Item | Required | Description |
| --- | --- | --- |
| LLM provider | O | Claude |
| Model name | O | claude-haiku-4-5, claude-sonnet-4-6 |
| API key | O | API key for the LLM. Stored only for this pipeline and not displayed again after saving. |
| Batch size | X | Number of rows to include in a single LLM call (1–30) |
| Max retries | X | Number of retry attempts on call failure (0–10) |
| Timeout (seconds) | X | Wait time for a call (1–600) |
| Incremental classification | X | Classifies only changed rows using the LLM, and reuses the previous run's results for unchanged rows. |

**Input Columns**

| Item | Required | Description |
| --- | --- | --- |
| Input column | O | Column(s) to pass to the LLM. Multiple columns can be selected. |
| Column join delimiter | X | Delimiter used when concatenating multiple input column values |
| User prompt template | X | Template for composing per-row input values. The {{ column name }} pattern is replaced with the corresponding column value. When set, this takes precedence over the column join delimiter. Only columns selected in the input column setting can be referenced. |

**Axes (Category Table)**

Register the category list used as the classification criteria as axes. Up to 5 axes can be added.

| Item | Required | Description |
| --- | --- | --- |
| Category node | O | Data source node containing the category list |
| Category ID column | O | Column that identifies the category |
| Category name column | O | Category name column |
| Category metadata column | X | Additional columns such as category descriptions and classification criteria. Passed along in the prompt to improve classification accuracy. |
| Classification result column (array) | O | Name of the array column to hold classification results |
| Representative column | X | Name of the column to store the most representative classification ID. If left empty, the column is not created. |

**Output**

| Item | Required | Description |
| --- | --- | --- |
| Output type | O | SINGLE_LABEL, MULTI_LABEL |
| Classification rationale column | X | Name of the column to store the classification rationale provided by the LLM. If left empty, rationale is not requested, reducing token costs. |
| Content rationale column | X | Name of the column to store a short description generated from the input content |
| Content rationale max length | X | Maximum number of characters for the content rationale column (1–200) |

**System prompt** (optional): Instructs the LLM on its role and classification criteria. If not set, the default prompt is used.

!!! danger "Caution"
    The more rows you process, the more LLM calls and token usage increase proportionally, raising costs. For large datasets, validate on a small scale first to verify cost and quality before applying at full scale.

<a id="pipeline.node.join"></a>
#### Join node (JOIN) { #pipeline.node.join }

Combines two data streams.

| Item | Required | Description |
| --- | --- | --- |
| Node name | O | Name of the join result node (up to 30 characters) |
| Join type | O | Select from Inner Join / Left Join / Right Join / Full Outer Join / Semi Join (EXISTS) / Anti Join (NOT EXISTS) |
| Join tables | O | Select the left and right table nodes |
| Join condition | O | Left field = right field mapping (multiple conditions supported) |
| Column selection | X | Select columns to include in the output; a prefix can be set. |

!!! tip "Note"
    If both tables have columns with the same name, you can set a **prefix** for the right table to prevent column name conflicts.

<a id="pipeline.node.union"></a>
#### Union node (UNION) { #pipeline.node.union }

Vertically combines two data streams.

| Value | Description |
| --- | --- |
| Full Merge | Includes all columns from both sides. Columns missing from one side are NULL. |
| Intersect Merge | Includes only columns common to both sides. |
| Left-First Merge | Based on the left table schema. Columns not present in the right table are NULL. |

<a id="pipeline.node.dataset"></a>
#### Dataset node (DATASET) { #pipeline.node.dataset }

The final output node in the pipeline. Saves processed data as a table.

| Item | Required | Description |
| --- | --- | --- |
| Dataset name | O | Used as the table name (up to 30 characters). Only lowercase English letters, numbers, and underscores (_) are allowed; must not start with a number. |
| Description | X | Dataset description (up to 500 characters) |
| Column selection | O | Select columns to include in the dataset (at least one required) |

The dataset name is used as both the data source name and the table name, so it cannot duplicate an existing data source name or table name. Duplicate checks are performed both when saving and when running the pipeline.

!!! danger "Caution"
    An executed dataset cannot be modified. Delete it and recreate it (the data source is retained).

<a id="pipeline.schedule"></a>
### Configure a Schedule { #pipeline.schedule }

Click the schedule icon in the right side panel to configure the batch schedule.

| Interval Type | Settings | Example |
| --- | --- | --- |
| Every minute | Interval (5/10/15/20/30 minutes) | Execute every 10 minutes |
| Every hour | Interval (1/2/3/4/6/8/12 hours), minute | Execute every 2 hours at 30 minutes |
| Every day | Hour, minute | Execute every day at 9:30 AM |
| Every week | Day of week (multiple selection), hour, minute | Execute every Monday, Wednesday, and Friday at 9:00 AM |
| Every month | Day, hour, minute | Execute on the 1st of every month at 9:30 AM |

Date range settings:

| Item | Required | Description |
| --- | --- | --- |
| Start date | X | When checked, the schedule starts from the configured date onward. If not set, the schedule starts from the time of saving. |
| End date | X | When checked, the schedule does not run after the configured date. |

After the schedule is saved and executed for the first time, it runs at the configured interval.

<a id="pipeline.resource"></a>
### Configure Computing Resources { #pipeline.resource }

Click the computing resource icon in the right side panel to configure the computing resources to use when running the pipeline.

| Type | Driver | Executor |
| --- | --- | --- |
| Small (default) | 1 CPU, 1 GB memory | 1 CPU, 1 GB memory × 1 |
| Medium | 1 CPU, 2 GB memory | 1 CPU, 2 GB memory × 2 |
| Large | 2 CPU, 4 GB memory | 2 CPU, 4 GB memory × 4 |
| XLarge | 4 CPU, 8 GB memory | 4 CPU, 8 GB memory × 8 |

!!! danger "Caution"
    If you change the resource settings, the changes are applied after a rebuild. You cannot change the resources before creating a pipeline.

<a id="pipeline.run"></a>
### Run Pipeline { #pipeline.run }

On the first run or after a settings change, the build and execution proceed together.

1. Click **Run** on the tab bar.
2. Click **Run** in the confirmation modal.

Execution is performed using the last saved configuration. If there are unsaved changes, a confirmation modal appears first to notify you that execution will proceed with the pre-save configuration — save your changes first if you want to include them in the run.
A pipeline that has already been built runs immediately without going through the build process.
Clicking **Stop** during execution transitions the pipeline to the Terminated status.
When the build is complete, pipelines with a schedule configured are automatically activated.

<a id="pipeline.run.history"></a>
#### View Run History { #pipeline.run.history }

Click **Run History** on the tab bar to view the run ID, start/end time, duration, run status, and per-node execution details.

<a id="pipeline.activation"></a>
### Activate/Deactivate { #pipeline.activation }

- **Activate**: Select one pipeline from the list and click **Activate Pipeline** in the More (⋯) menu. The pipeline runs automatically according to the configured schedule.
- **Deactivate**: Select one pipeline from the list and click **Deactivate Pipeline** in the More (⋯) menu. The pipeline does not run automatically even if a schedule is configured.

<a id="pipeline.delete"></a>
### Delete Pipeline { #pipeline.delete }

1. Select the pipeline to delete from the list (multiple selections allowed).
2. Click **Delete**.
3. Click **Delete** in the confirmation modal.

<a id="query"></a>
## Analysis - Query { #query }

Console path: **Machine Learning > NHN Cloud Foundry > Analysis** tab > **Query** tab

Use SQL to query and analyze data from a data source.

<a id="query.run"></a>
### Run a Query { #query.run }

1. Select a **Data Source**.
2. Load a saved query from **Query Selection**. Queries saved for the selected data source appear in the list; you can also write a query directly without loading one.
3. Enter SQL in the query input field.
4. Select a **Row Limit** (10, 100, 1,000, 10,000, or 100,000; default: 1,000).
5. Click **Run Query**.

- The execution results are displayed in a data grid format. The column structure is dynamically generated based on the query results, and pagination is supported.
- When you select a data source, a schema panel appears to the right of the query input field, where you can view field names and data types. You can search by field name.
- Press **Ctrl+Enter** (or **⌘+Enter** on macOS) in the query input field to run the query.
- If a query fails to run, the reason for the failure is displayed in the results area.
- Click **Reset** to clear the query that you have written.
- Click **Download Query Results** to save the results as a CSV file (file name: `query_name_date_time.csv`).
- Use the table name as shown in the data source list in the FROM clause (`SELECT * FROM {table_name}`).
- Only a single SELECT statement can be executed. All other statements are rejected.

<a id="query.save"></a>
### Modify a Saved Query { #query.save }

After loading a query with **Query Selection** and modifying its content, click **Save Query** to save your changes. The button is disabled if no query is loaded or if no changes have been made.

<a id="query.list"></a>
### Query List { #query.list }

Every query that you run is automatically recorded in the execution history. You can also create queries in the query list for repeated use. Click **Query List** to open the modal for managing saved queries.

| Column | Description |
| --- | --- |
| Query Name | Name assigned when saving |
| Query Statement | Saved SQL |
| Saved At | Date and time the query was last saved |
| Details | View the full content of the query |

- You can search by query name.
- Click **Add** to register a new query. Select a query and click **Modify** or **Delete** to edit or delete it. Deleted queries cannot be recovered.

The fields that you enter when adding or modifying a query are as follows:

| Field | Required | Description |
| --- | --- | --- |
| Query Name | O | Name to identify the query |
| Data Source | O | Data source on which to run the query |
| Statement | O | SQL to execute |

<a id="query.history"></a>
### Query Execution History { #query.history }

This screen shows all queries that have been run. You can search by **Time** range and **Query Content**, and click **Reset** to clear the search conditions.

| Column | Description |
| --- | --- |
| Query Name | Name of the executed query |
| Query Run Date | Date and time the query was run |
| Data Source Name | Data source on which the query was run |
| Query/Result | Executed SQL and its result |

Click an item in the list to view query details. Click **Use Query** to load the query to the execution screen.

<a id="chart"></a>
## Analysis - Chart { #chart }

Console path: **Machine Learning > NHN Cloud Foundry > Analysis** tab > **Chart** tab

<a id="chart.list"></a>
### Chart List { #chart.list }

- You can filter chart names using the search feature at the top.

<a id="chart.create"></a>
### Create a Chart { #chart.create }

Click the **Create Chart** button to go to the chart editor screen. In the editor, configure the following settings in order.

<a id="chart.create.basic"></a>
#### Basic Settings { #chart.create.basic }

| Item | Required | Description |
| --- | --- | --- |
| Chart Name | O | Name to identify the chart (up to 30 characters) |
| Chart Type | O | Categorizes the chart purpose (currently only the default type is available) |
| Chart Visualization Type | O | Line Chart, Bar Chart, Pie Chart, Scatter Chart |

<a id="chart.create.datasource"></a>
#### Data Source Settings { #chart.create.datasource }

| Item | Required | Description |
| --- | --- | --- |
| Data Source Type | O | FILE, DATASET, RECOMMENDATION SINK |
| Data Source Name | O | Select the data source to use |

<a id="chart.create.query"></a>
#### Query Settings { #chart.create.query }

| Item | Required | Description |
| --- | --- | --- |
| X-axis | O* | Field to use for the horizontal axis. Not displayed in Pie charts |
| Aggregation Interval | O* | 5 minutes, 15 minutes, 30 minutes, 45 minutes, 1 hour, 2 hours, 6 hours, 12 hours, 1 day, 3 days, 7 days. Displayed in Line and Bar charts only |
| Reference Time | O | Specifies the time range of the data |
| Column | O | Select the column and aggregation function to aggregate. At least one is required |
| Group Key | O* | Column to split values by. At least one is required for Pie charts; optional for other chart types |
| Filter | X | Set data filtering conditions |
| Sort | X | Sort column and direction. Displayed in Pie and Bar charts only |
| Row Limit | O | Maximum number of rows to retrieve |

The required settings for each chart visualization type are as follows:

| Chart Visualization Type | Required Settings |
| --- | --- |
| Line, Bar | X-axis (time axis), Aggregation Interval, at least one Column |
| Pie | Base time column, at least one column, at least one group key |
| Scatter | At least one Column |

When a sort is specified for a Bar chart, the top N categories are displayed instead of the time axis.

<a id="chart.create.preview"></a>
#### Chart Preview { #chart.create.preview }

After completing the configuration, click the **UPDATE CHART** button to preview the chart.

- Verify that the chart is displayed correctly.
- You can review the data in the table view at the bottom and toggle the table view on or off.
- If the query fails, a **Chart Query Failure** panel is displayed in the chart area, and you can check the error message returned by the query engine. Modify the query settings based on the error message and query again.
- If there are columns without an aggregation function selected, guidance is displayed when you click **UPDATE CHART**. If there is no aggregation function, the chart may not display correctly.

<a id="chart.create.save"></a>
#### Save a Chart { #chart.create.save }

- After reviewing the preview, click the **Create** button in the header.
- The Create button is enabled once input validation is complete.

<a id="chart.edit"></a>
### Edit a Chart { #chart.edit }

Click a chart in the chart list to open the edit screen.

- You can modify the basic settings, data source settings, and query settings.
- Preview the changes by clicking **UPDATE CHART**, then save them by clicking **Save**.

<a id="chart.delete"></a>
### Delete a Chart { #chart.delete }

1. Select the chart to delete by checking the checkbox in the chart list.
2. Click the **Delete** button.
3. Click **Delete** in the confirmation modal.

!!! danger "Caution"
    Deleting a chart that is in use on a dashboard will also remove it from that dashboard.

<a id="dashboard"></a>
## Analytics - Dashboard { #dashboard }

Console path: **Machine Learning > NHN Cloud Foundry > Analytics** tab > **Dashboard** tab

<a id="dashboard.list"></a>
### Dashboard List { #dashboard.list }

- You can filter dashboards by name using the search feature.
- You can adjust the number of items displayed per page.

<a id="dashboard.create"></a>
### Create a Dashboard { #dashboard.create }

Click the **Create Dashboard** button to go to the dashboard editor screen.

| Item | Required | Description |
| --- | --- | --- |
| Dashboard Name | O | Name to identify the dashboard |
| Dashboard Description | X | Description of the dashboard |

The edit panel consists of two tabs.

| Tab | Description |
| --- | --- |
| CHARTS | List of charts that can be added to the dashboard. Searchable by chart name |
| LAYOUT ELEMENTS | Layout elements to add to the canvas |

<a id="dashboard.create.chart"></a>
#### Add a Chart { #dashboard.create.chart }

1. Click or drag the chart card to add.
2. Place the chart on the dashboard canvas.

<a id="dashboard.create.tabgroup"></a>
#### Add a Tab Group { #dashboard.create.tabgroup }

You can group multiple charts into tabs and switch between them in one place. Click **Tab** in the **LAYOUT ELEMENTS** tab of the edit panel to add a tab group to the canvas.

- Use **Add Tab** in the tab group to add more tabs. When there are two or more tabs, a delete icon appears on each tab. You cannot delete a tab if only one tab remains.
- Double-click a tab to change its name.
- Drag a chart from the edit panel and drop it onto the tab area to place it in the tab. To move a chart that is already on the canvas into a tab, drag the handle on the left of the chart title. You can also move a chart from a tab back to the canvas in the same way.
- To delete a tab group from the dashboard, click the trash icon in the top right corner, just as you would for a chart.

<a id="dashboard.create.layout"></a>
#### Adjust the Layout { #dashboard.create.layout }

Drag a chart placed on the canvas to reposition it, and drag its corners to resize it. Click the trash icon in the top right corner of a chart to delete it from the dashboard.

<a id="dashboard.create.save"></a>
#### Save the Dashboard { #dashboard.create.save }

After completing the configuration, click the **Save** button in the header.

<a id="dashboard.view"></a>
### View a Dashboard { #dashboard.view }

Click a dashboard in the dashboard list to open the details screen.

<a id="dashboard.edit"></a>
### Edit a Dashboard { #dashboard.edit }

On the dashboard details screen, click the **Edit Mode** toggle to switch to edit mode.

In edit mode, you can perform the following operations:

- Add, delete, or reposition charts
- Change the dashboard name

To modify a chart placed on the dashboard, turn off edit mode. When edit mode is off, a more options menu appears on each chart. Choose **Edit Chart** to go to the chart editing page. Charts inside a tab group can be accessed in the same way. After editing and saving a chart, the changes are reflected on the dashboard.

<a id="dashboard.delete"></a>
### Delete a Dashboard { #dashboard.delete }

1. In the dashboard list, select the dashboard to delete.
2. Click the **Delete** button.
3. Click **Confirm** in the confirmation modal.

<a id="app"></a>
## App { #app }

Console path: **Machine Learning > NHN Cloud Foundry > App** tab

Create and manage recommendation system serving pipelines that use AI models.

<a id="app.list"></a>
### App List { #app.list }

| Column | Description |
| --- | --- |
| App type | Type of the app |
| App ID | Unique identifier of the app |
| App name | Name that identifies the app |
| App description | Description of the app |
| Status | Current app status |
| Created on | Date and time the app was created |

<a id="app.list.status"></a>
#### App Status { #app.list.status }

Hover over the app status badge to view a detailed description in a tooltip.

| Value | Description |
| --- | --- |
| Initializing | App initialization in progress |
| Training | AI model training in progress |
| Deploying | App deployment in progress |
| Activating | App activation in progress |
| Active | App is active |
| Deleting | App deletion in progress |
| Failed | An error occurred while processing the app |
| Unknown | Status information is unavailable |

- After an app is created, training and deployment proceed automatically.
- If an error occurs at any stage, the app transitions to the Failed status.

!!! tip "Note"
    The training and deployment that occur immediately after app creation are part of the preparation process. At this point, the recommendation model has not yet been trained. If you call the recommendation API, a response is returned, but it does not contain results from a trained model.
    The first training run executes at the time specified in the batch schedule (status: Training → Deploying → Activating → Active). Valid recommendation results are available only after the trained model has been deployed.

<a id="app.create"></a>
### Create App { #app.create }

Click the **Create App** button to go to the app creation screen. App creation proceeds in three steps.

| Step | Description |
| --- | --- |
| Basic Settings | Select app name, description, and type |
| Detail Settings | Select model, serving resources, batch schedule, data connections, and additional settings |
| Final Review | Review input and create |

<a id="app.create.basic"></a>
#### Basic Settings { #app.create.basic }

| Item | Required | Description |
| --- | --- | --- |
| App name | O | Name to identify the app (up to 255 characters). Supports Korean, Japanese, English, numbers, spaces, hyphens (-), and underscores (_). |
| App description | O | Description of the app |
| App type | O | Select **Recommendation System** |

<a id="app.create.detail"></a>
#### Detail Settings { #app.create.detail }

Click the **Add Model** button to add a model card. You can configure multiple models in a single app, and each model card has the sections described below.

<a id="app.create.detail.model"></a>
##### Basic Model Settings { #app.create.detail.model }

| Item | Required | Description |
| --- | --- | --- |
| Model name | O | Select the recommendation model to use |
| Longtail mode | X | When enabled, includes low-popularity items in recommendations |

The following models are available:

| Name | Description |
| --- | --- |
| Cold User | Recommends items to users with little activity history (e.g., new users) based on item attributes. |
| Warm User (Transformer) | Recommends the next item based on the sequence of items that a user recently interacted with. |

The same model with a different Longtail mode setting can be added as a separate model.

<a id="app.create.detail.resources"></a>
##### Serving Resource Settings { #app.create.detail.resources }

Specify the resources to allocate to the serving container for each model. If left blank, the default values are applied.

| Item | Required | Description |
| --- | --- | --- |
| CPU request / CPU limit | X | In cores. Default: 2 / 4 |
| Memory request / Memory limit | X | In Gi. Default: 4 / 4 |

The `request` value cannot exceed the `limit` value.

<a id="app.create.detail.schedule"></a>
##### Batch Schedule Settings { #app.create.detail.schedule }

Set the execution frequency for the batch that retrains the model. This is enabled by default and can be turned off with the toggle.
The first training run for the model also executes at the time specified in this schedule. Recommendation responses returned before the first training is complete are not results from a trained model.

| Frequency | Settings |
| --- | --- |
| Daily | Hour, Minute |
| Weekly | Day of week, Hour, Minute |
| Hourly | Hour interval, Minute |

The configured time is applied based on the time zone of the browser you are using.

<a id="app.create.detail.connection"></a>
##### Data Connection Settings { #app.create.detail.connection }

Connect the data sources required by the selected model.

General recommendation model:

| Item | Required | Description |
| --- | --- | --- |
| User data source | O | Data source for user information |
| User ID column | O | Column that identifies users |
| User feature column | X | Additional user attribute columns (multiple selections allowed) |
| Item data source | O | Data source for item information |
| Item ID column | O | Column that identifies items |
| Item feature column | X | Additional item attribute columns (multiple selections allowed) |
| History data source | O | Data source for user-item interaction |
| History user ID column | O | Column that identifies users in the history |
| History item ID column | O | Column that identifies items in the history |
| Time column | X | Column for interaction time |
| History feature column | X | Additional interaction attribute columns |

Tag embedding model:

| Item | Required | Description |
| --- | --- | --- |
| Tag data source | O | Data source for tag information |
| Attribute column | O | Column for tag values |
| Item ID column | O | Column that identifies items |
| Time column | X | Time column |

<a id="app.create.detail.extra"></a>
##### Additional Settings (Skills) { #app.create.detail.extra }

This is an optional setting for connecting skill and category data used to construct recommendation reasons (reason). Click the **Add Field** button to add entries.

| Item | Description |
| --- | --- |
| Skill data source | Skill information table. Specify the skill ID column and skill column. |
| Default skill category / Common skill category | Skill classification table. Specify the skill ID column and skill label column. |
| User group data source | A unit that groups users targeted for recommendations (e.g., department, grade, interest group). Specify the user group ID column and skill column. |
| User interest skill data source | Table of interest skills per user. When no interest skill is passed to the recommendation API, this table is queried to generate interest-based recommendation reasons. |
| User attribute mapping | Specifies the key name for passing each item in the userAttributes of the recommendation API. |
| Recommendation reason template data source | Table of recommendation reason phrase templates. If not selected, reasons are not included in recommendation results. |
| Cold start data source | Only user IDs in this table are identified as cold starters. Both the data source and user ID column must be selected. |

<a id="app.create.detail.univariate"></a>
#### Univariate Anomaly Detection Advanced Settings { #app.create.detail.univariate }

A univariate anomaly detection app learns each metric individually to detect values that fall outside the normal range. Advanced settings are configured in the following order: Data Source, Model Resources, Retraining, Detection Options, and Result Transmission.

<a id="app.create.detail.univariate.source"></a>

##### Data Source { #app.create.detail.univariate.source }

| Field | Required | Description |
| --- | --- | --- |
| Metric Data Source | O | The data source that receives the target metric for detection. Only data sources with Prometheus API type can be selected |

- You must create a data source with Prometheus API type first for it to appear in the list.
- The Series Identification Label and Group Label specified in the selected data source become the criteria for dividing time series and groups.
- Only one univariate anomaly detection app can be created per Metric Data Source. Data sources already in use by other univariate anomaly detection apps are not displayed in the list.
- If there is no data in the selected data source, a message "No data yet" appears under the field, and a **Check Data** box appears below the Resource Check section at the bottom of the screen. If no Retraining Cycle is specified, training during creation is the only training, so you cannot proceed to the next step until data arrives. If a Retraining Cycle is specified, only a notice is displayed that the initial training will fail and will be retried at the next Retraining, and you can proceed.
- If multiple different values for the same time series arrive within one minute in the past 5 minutes, a notice box is displayed. Creation is not prevented, but in this state, only the first value to arrive each minute is used in the analysis and the rest are discarded. Send the same time series only once per minute. If collected at shorter intervals, aggregate them by averaging over one minute before sending.

<a id="app.create.detail.univariate.resource"></a>

##### Model Resources { #app.create.detail.univariate.resource }

| Field | Required | Description |
| --- | --- | --- |
| CPU Limit | O | The CPU upper limit assigned to the inference server. Use Kubernetes notation. Example: 2, 500m. Minimum 2 vCPU, default value 2 |
| Memory Limit | O | The memory upper limit assigned to the inference server. Use Kubernetes notation. Example: 1Gi, 512Mi. Minimum 1Gi, default value 1Gi |

Model Resources cannot be changed after the app is created.

<a id="app.create.detail.univariate.retrain"></a>

##### Retraining { #app.create.detail.univariate.retrain }

| Field | Required | Description |
| --- | --- | --- |
| Retraining Cycle | X | Toggle to specify whether to use it. Default is off. When enabled, specify the cycle below |

| Cycle | Setting Items |
| --- | --- |
| Daily | Hour and minute. Hour is 0–23, minute is in 10-minute increments with default of 03:00 |
| Weekly | Day of the week, hour, and minute |
| Hourly Interval | Interval and minute. Interval is selected from 1, 2, 3, 4, 6, 8, 12 hours |

- The configured time is applied based on the time zone of the browser you are accessing.
- If no cycle is specified, training occurs only once when creating the app, and no automatic retraining occurs afterwards. In this case, you cannot create an app with a data source that has no data.
- We recommend that you specify a time period with light traffic, as training consumes many resources.

<a id="app.create.detail.univariate.option"></a>

##### Detection Options { #app.create.detail.univariate.option }

| Field | Required | Description |
| --- | --- | --- |
| Transmission Mode | O | Select when to export the anomaly score and threshold |
| Score Scale | X | Toggle **Export as 0–100 (%) scale**. Default is off |
| Device | O | The computing device to use for inference and training. Choose between CPU or GPU, default is CPU |

Transmission Mode can be selected from the following:

| Value | Description |
| --- | --- |
| Accuracy Mode | Default. Sends only reliable values after metric preparation is complete |
| Immediate Mode | Sends immediately after activation. Values before preparation is complete are for reference only |

- The app groups metrics in 1-minute intervals and makes judgments for each time series. The data source connected to the app must send the same time series uninterrupted, one per minute. If sent at longer intervals, gaps appear and preparation may not complete in Accuracy Mode. If multiple values are sent within one minute, only the first arriving value is used in the judgment. Loading metrics to the data source itself is independent of the transmission cycle.
- New incoming metrics take several hours until sufficient data is accumulated for judgment and the threshold is calibrated to the distribution of those metrics.
- If transmission is interrupted for several minutes or longer, the accumulated intervals are broken and the state returns to preparation. In Accuracy Mode, no results are sent until the intervals are refilled.
- When Score Scale is enabled, scores are compressed to 0–1, multiplied by 100 to export as 0–100, and thresholds are also calculated on the same scale. Use this when matching the scale with a dashboard that uses a percentage axis. When disabled, raw values are exported as-is.
- The same device is applied for inference and training. Learning and inference work with the default CPU, but GPU may not be available depending on the resource status of your service environment.

!!! danger "Caution"
    Score Scale cannot be changed after the app is created.

<a id="app.create.detail.univariate.sink"></a>

##### Result Transmission { #app.create.detail.univariate.sink }

Configuration for sending detection results to Prometheus.

| Field | Required | Description |
| --- | --- | --- |
| Transmission URL | O | The address to send results to |
| API Path | O | The path appended after the Transmission URL. Default /api/v1/write |
| Score Metric Name | O | The metric name where the anomaly score is stored. Default AD_SCORE |
| Threshold Metric Name | X | The metric name where the automatically calculated threshold is stored. Default AD_AUTO_THRESHOLD |

Click **Expand Additional Transmission Settings** to configure the following items.

| Field | Required | Description |
| --- | --- | --- |
| Static Header | X | HTTP header always attached to transmission requests. Used for adding authentication tokens |
| Dynamic Header | X | Sends field values from result records as HTTP headers. Use only when the receiving end requires it |
| Metric Family Name | X | Name for grouping the score and threshold metrics together. Leave blank to not group |

- Enter static headers in the format `HeaderName:Value` and separate multiple entries with commas. Example: `Authorization:Bearer abc123`
- Enter dynamic headers in the format `RecordField:HeaderName` and separate multiple entries with commas. Example: `tenant:x-monitoring-tenant-alias`
- The same header name or the same record field cannot be entered twice. If the format is incorrect, an error message is displayed below the input field.
- You cannot create an app if another app is already sending the same score and threshold metric names to the same transmission address. Specify different metric names or transmission addresses to prevent result time series from being mixed.
- Transmission failures to the transmission URL are not displayed in the console. If results are not visible in the receiving Prometheus, verify by cross-checking with the results stored in the Result Data Source.

!!! tip "Note"
    Inference results are always stored in the Result Data Source separately from Prometheus transmission. The Result Data Source is automatically created when the app is created and can be queried from the Analysis menu.

The schema of the Result Data Source is as follows. Query by these columns from queries or charts in the Analysis menu.

| Field Name | Data Type | Description |
| --- | --- | --- |
| labelHash | string | Time series identifier. Same value as labelHash from the Metric Data Source |
| identityLabels | string | Original label text of the time series |
| score_aggregate | double | Anomaly score |
| threshold | double | Anomaly judgment threshold value |
| eventTimestamp | long | Time of the target metric for judgment. Milliseconds epoch |

The system column `ingestTimestamp` is automatically added.

<a id="app.create.review"></a>
#### Final Review { #app.create.review }

Display the content entered in the previous step, summarized according to the app type.

Recommendation System:

| Review Item | Description |
| --- | --- |
| Basic Settings | App name, description, and type |
| Model Settings | Selected model, serving resources, batch schedule, and data connection information |
| Additional Settings | Additional settings such as skill tables |

Click the **Save** button to create the app. On success, a completion modal is displayed and you are redirected to the list. On failure, an error message is displayed.

| Review Item | Description |
| --- | --- |
| Basic Settings | App name, description, type |
| Detailed Settings | Metric Data Source, Model Resources, Retraining Cycle, Detection Options, Result Transmission Settings |

- If no retraining cycle is specified, it displays as 'None (1 time training at creation)'.
- Fixed headers and dynamic headers are displayed as 'Configured', 'None', or a hyphen instead of the entered values.

Click **Save** to create the app. On success, a completion modal is displayed and you are taken to the list. On failure, an error message is displayed.

The completion modal of the univariate anomaly detection app displays the next steps.

- Train and deploy the model. Check the progress by viewing the status in the app list.
- In Accuracy mode, even after activation, results will not be output until metrics for determination have accumulated. This typically takes several hours.
- During that time, you must continue sending metrics.

<a id="app.delete"></a>
### Delete App { #app.delete }

1. Select the checkbox for the app you want to delete. You can select only one app at a time. When you select another app, the previous selection is deselected.
2. Click the **Delete** button.
3. In the confirmation dialog, verify the app name and click **Confirm**.

!!! danger "Caution"
    Deleted apps cannot be recovered. The associated serving pipeline is also deleted.
    Inference Result Data Sources are not deleted and remain. Delete them separately from the Data Source List if needed. Metric Data Sources in use by the app can be deleted after deleting the app.

<a id="app.detail"></a>
### App Details { #app.detail }

Click an app in the app list to go to the details screen. The details screen consists of two tabs: **Recommendation API Call** and **App Info**.

<a id="app.detail.recommend"></a>
#### Recommendation API Call { #app.detail.recommend }

You can call the recommendation API directly by entering request parameters and view the results. The screen consists of three areas: input form, request preview, and recommendation results.

Input form:

| Item | Description |
| --- | --- |
| Recommendation app ID | App ID to call. Automatically populated with the current app. |
| User ID | Select the user to receive recommendations. |
| Recommendation mode | Choose between Sequential (history-based) and Cold Start (attribute-based). |
| Maximum recommendations | Maximum number of items to include in the response (1–100, default: 10). |
| Longtail mode | Improves recommendation diversity by including unpopular items. Not available in Cold Start mode. |
| context | Add contextual information for the recommendation request (e.g., current or recently viewed items) on a field-by-field basis. |
| userAttributes | Add user attribute information (e.g., group, age, interests) on a field-by-field basis. |
| options | Add recommendation request options on a field-by-field basis. |

- **Request Preview**: Displays the actual API request JSON built from your input. You can copy it using the **Copy** button and use it for API integration development.
- **Recommendation Results**: Click the **Request Recommendation** button to display rankings, item keys, scores, and recommendation reasons. The total result count and response time are also shown.

!!! tip "Note"
    Recommendation API calls are only available when the app is in the Active status.

<a id="app.detail.info"></a>
#### App Info { #app.detail.info }

You can view the app ID, app name, status, app type, description, creation date, modification date, version, and input and output data sources.

- Input data source: The data sources used for model training. For recommendation apps, data sources are displayed separately by model.
- Output data source: The data source where recommendation results are stored.

<a id="app.detail.univariate.info"></a>
#### App Info { #app.detail.univariate.info }

The header displays the app name, status, app type, app ID, creation date, last modified date, and description. Below that, cards are displayed in the following order: **Input → Processing → Output**.

**Input**: Metric Data Source

| Item | Description |
| --- | --- |
| Name | Metric Data Source name |
| Type | Data Source type |
| Group Key Field | Label to categorize groups. The data source's group label setting is displayed; if not set, shows "Not configured (single group)" |
| Series Identification Label | A label to distinguish time series. If not set, shows "Use all labels" |
| Data Source ID, Data Source table name | Used for inquiries or log verification |

**Processing**: Univariate Anomaly Detection Model

| Item | Description |
| --- | --- |
| Model Resources | Maximum CPU and memory limits used for training and inference |
| Device | CPU or GPU |
| Training status | Training pending, Training in progress, Training completed, Retraining stopped, Training failed, Deleted |
| Last training date | The last time training was performed |
| Retraining cycle | Format: "Daily 03:00", "Every Monday at 03:00", "Every 6 hours". If not set, shows "No automatic retraining (trained once at creation)" |
| Transmission Mode | Precise mode, Immediate mode |
| Score Scale | Original value or 0–100 scale |

**Output**: Result Transmission

| Item | Description |
| --- | --- |
| Transmission address | The address where results are sent. Combined value of transmission URL and API path |
| Score Metric Name | Metric name where anomaly scores are stored |
| Threshold Metric Name | Metric name where anomaly detection thresholds are stored |
| Result Data Source | Name of the data source where results are stored |
| Data Source ID, Data Source table name | Used for inquiries or log verification |

- Hover your mouse over the question mark icon next to an item label to view the description.
- For apps without a transmission address configured, the message "Results are saved only to the Result Data Source without being sent externally" is displayed.
- Values entered in static and dynamic headers are not displayed on the screen.
- Inference results are always saved to the Result Data Source separately from Prometheus transmission and can be viewed in the Analysis menu.
- Below the card, the group status is displayed as four numbers: **All**, **Active**, **Activation Pending**, **Inactive**. Clicking a number takes you to the Group List tab and filters by that status.
- Hover your mouse over the question mark icon next to the Group Status title to see the meaning of the three states. Activation Pending usually takes several hours in Precise mode, and the group is activated immediately after being turned on in Immediate mode.
- If retraining fails, the training status is shown as Training failed. Results continue to be produced using the previously trained model, and training will be attempted again in the next retraining cycle. If initial training fails, the app enters a failed state and can be deleted.
- Date and time are displayed in the time zone of the browser you are accessing.

<a id="app.detail.univariate.groups"></a>
#### Group List { #app.detail.univariate.groups }

Anomaly detection is performed for each time series, and a group is a unit for bundling those time series to check their detection results and status.

| Column | Description |
| --- | --- |
| Group Key | The label name that serves as the criterion for dividing groups. Groups without a Group Key field are displayed as a hyphen |
| Value | The value of that label. Apps without a Group Key field show "single group" |
| Group Hash | A 16-character hash that identifies the group. Automatically calculated from the Group Key values |
| Status | The current status of the group |
| Activation Time | The time when sufficient data for judgment has been collected and results start to be sent out. Groups in the Activation Pending status are displayed as a hyphen |
| Deactivation Time | The time when the group was last deactivated. The history is retained even after reactivation, and is displayed as a hyphen if never deactivated |
| Created on | The date and time when the group was registered |
| Modified on | The date and time when the group information was last changed |

Status:

| Value | Description |
| --- | --- |
| Active | Detection results for this group are being sent out |
| Activation Pending | The group is enabled, but results are not yet being sent out because data is still being collected |
| Inactive | A group that has been disabled for non-use |

- When you specify a Group Label in the data source, one group is created for each value. If not specified, the entire data source becomes a single group.
- Groups are registered when metrics arrive, not when the app is created. The list is empty immediately after creating an app.
- Activation Pending usually takes several hours in precision mode. Immediate mode is activated immediately after the group is enabled.
- Errors are determined at the group level. If inference stops for even one time series within a group, the entire group enters an error state, and the group returns to normal only when that time series recovers.
- You can narrow the list by filtering by status or searching by Group Key or Group Hash.
- The Group Key, Activation Time, Deactivation Time, Created on, and Modified on columns can be sorted by clicking the header. Sorting is based on all groups, and changing the sort order takes you to page 1. The Value, Group Hash, and Status columns cannot be sorted; the Value is sorted from the Group Key column.
- You can adjust the number of items displayed per page (20, 50, 100 / default 20).
- If there are no registered groups, "There are no registered groups. They will be displayed here when data arrives and groups are registered." is shown. If there are no groups matching the search or filter conditions, "There are no groups matching the conditions." is shown.
- To start, stop, or delete only specific groups, see "Starting, Stopping, and Deleting Group Usage" in [API Guide](../api-guide/#univariate.group.api). This operation is not available in the console.

<a id="app.detail.univariate.groups.hash"></a>
##### Hash Calculator { #app.detail.univariate.groups.hash }

Click the **Hash Calculator** button in the toolbar to directly calculate a hash from labels.

- Paste the label JSON as-is or enter `name=value` one per line.
- The canonical form and 16-character hash are displayed, and you can copy them with the **Copy** button.
- For Group Hash, enter only labels corresponding to the Group Key field; for Series Hash, enter only labels that distinguish time series.
- You can also check the hash in advance for groups that are not yet registered.
- If the hash differs from expected, compare it with the canonical form first. The canonical form is a value formed by sorting labels alphabetically by name and connecting them with commas.