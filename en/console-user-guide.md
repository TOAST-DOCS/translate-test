<!-- machine_translated: true -->

<a id="foundry.console.guide"></a>

## Machine Learning > NHN Cloud Foundry > Console User Guide { #foundry.console.guide }

This document describes how to manage data sources, pipelines, analysis (queries, charts, and dashboards), and apps in the NHN Cloud Foundry console.

The Required column in the settings table means the following:

- `O`: Required
- `X`: Optional
- `O*`: Required or optional depending on other settings

<a id="status"></a>

## Status { #status }

Console path: **Machine Learning > NHN Cloud Foundry > Status** tab

On the Status tab, check the service activation status and tenant settings. To use the service, first verify the activation status on this tab, and if the service is not activated, submit an activation request.

<a id="status.activate"></a>

### Enable Service { #status.activate }

Service activation cannot be performed directly from the console. Contact us via [1:1 inquiry](https://www.nhncloud.com/kr/support/inquiry) and include the resource size you want. Once the requested cluster is created, you can start using the service in order, beginning with data source creation.

The features available by resource size are as follows:

| Value | Description |
| --- | --- |
| SMALL | Basic resources: Data source, common features, and chart queries available |
| MEDIUM | Basic + data pipelines additionally available |
| LARGE | Basic + AI apps available |
| XLARGE | All features available (data pipelines + AI apps) |

<a id="status.info"></a>

### Check Service Status { #status.info }

After activation, you can check the following information on the Status tab.

| Item | Description |
| --- | --- |
| Service status | Current activation status of the service |
| Tenant domain | Domain used to access the service |

- If you need to change resources after activation, also submit the request via 1:1 inquiry.
- While the service environment is being set up or cleaned up, a progress indicator is displayed.
- Click the **Disable** button to deactivate the service.

!!! danger "Caution"
    Deactivating the service deletes all resources that were created, and this action cannot be undone.

<a id="datasource"></a>

## Data Source { #datasource }

Console path: **Machine Learning > NHN Cloud Foundry > Data Source** tab

A data source is a unit that stores data to be analyzed in NHN Cloud Foundry. You can create, view, and delete data sources from the console.

<a id="datasource.list"></a>

### Data Source List { #datasource.list }

You can check the following information on the data source list screen.

| Column | Description |
| --- | --- |
| Type | Type of the data source |
| Data source name | Name that identifies the data source |
| Table name | Name of the table where data is stored |
| Status | Current status of the data source |
| Created on | Date and time the data source was created |
| Details | Click the magnifying glass icon to view details |

Type:

| Value | Description |
| --- | --- |
| File | Data source created from an uploaded CSV file |
| Recommendation | Data source where recommendation results are stored |
| Dataset | Data source created by a pipeline |

Status:

| Value | Description |
| --- | --- |
| INITIALIZING | The data source is being initialized. |
| PROCESSING | Data is being processed. |
| INGESTING | Data is being loaded. |
| COMPLETED | Data source processing is complete. |
| FAILED | Data source processing failed. |
| DELETING | The data source is being deleted. |

For data sources of type File, the most recent file upload result is displayed as an icon next to the status.

| Value | Description |
| --- | --- |
| Reflecting | The most recently uploaded file is being applied. |
| Review recommended | The most recently uploaded file has been applied, but there are items to review. Check the details in the data source details view. |
| Review required | The data source is available, but the most recently uploaded file was not applied. Check the file and upload it again. |

- Hover over the question mark icon next to a status badge to see the status description.
- Use the search feature at the top to filter by data source name or ID.
- You can also narrow down results using the column header filters for the Type, Data source name, Table name, and Status columns.
- You can adjust the number of items displayed per page (10, 20, or 50 items; default is 10).

!!! tip "Note"
    Items of type Recommendation and Dataset cannot be created directly by the user. Recommendation data sources are created automatically when you create a recommendation system app, and Dataset data sources are created automatically when you run a pipeline.

<a id="datasource.create"></a>

### Create Data Source { #datasource.create }

Click the **Create Data Source** button to open the creation modal.

<a id="datasource.create.basic"></a>

#### Basic Settings { #datasource.create.basic }

| Item | Required | Description |
| --- | --- | --- |
| Data source name | O | Use letters, numbers, hyphens (-), or underscores (_) (1–255 characters) |
| Table name | O | Use lowercase letters, numbers, or underscores (_) (1–255 characters) |
| Description | X | Description of the data source |

<a id="datasource.create.detail"></a>

#### Detail Settings { #datasource.create.detail }

| Item | Required | Description |
| --- | --- | --- |
| CSV file | X | Click the **Select File** button to select a CSV file to upload (up to 100 MB) |
| Header settings | X | If "First row is header" is checked, the first row of the CSV is used as column names |
| Primary key fields | X | Enter fields separated by commas (e.g., user_id,item_id) |
| Schema | O | Define the field names and types for the data |

Enter the schema using one of the following methods:

- Type inference: Select a CSV file and click the **Infer Types** button to infer column types from a sample of the first rows (up to 1,000 rows) of the CSV, which fills in the schema input. Manually correct any incorrectly inferred types.
- Table editing: Click the **Add Fields** button to add rows, and specify the field name and type for each row. The Remarks column displays any items that need to be reviewed from the type inference results.
- JSON editing: Click the **Edit as JSON** button and enter a JSON array directly in the following format.

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
| float | Floating point (32-bit) |
| double | Floating point (64-bit) |
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

<a id="datasource.delete"></a>

### Delete Data Source { #datasource.delete }

Select the data sources to delete using the checkboxes in the list, then click the **Delete** button.

- Deleting a data source also deletes the table and the loaded data.
- You cannot delete a data source while a data ingestion job is in progress.

<a id="datasource.detail"></a>

### Details / Preview { #datasource.detail }

- **Details** (magnifying glass icon): View information about the data source.
- **Preview** (⌄ icon): Preview the loaded data in table format.

The Details view consists of the following tabs:

| Tab | Description |
| --- | --- |
| Connection information | Data source ID, data source name, table name, type, description, and status |
| Catalog | View the list of field names and data types, and **Add Fields** |

<a id="datasource.edit"></a>

### Update Data { #datasource.edit }

The data source name and table name cannot be changed after creation. You can update the loaded data with a new CSV file and add new fields.

<a id="datasource.edit.csv"></a>

#### Update Data with CSV { #datasource.edit.csv }

In the list, click the more options (⋯) menu for a data source row of type File, and choose **Update with CSV**.

1. Review the existing column list.
2. Click the **Select File** button to select a new CSV file (up to 100 MB).
3. Review the preview and any notes for the selected file.
4. Click the **Overwrite** button to start the upload. Check the progress on the list screen.

Upload is restricted in the following cases:

| Situation | Guidance |
| --- | --- |
| The file has more columns than the existing columns | Add fields to the catalog first, then upload again. |
| The file contains columns not in the catalog | Add fields to the catalog first, then upload again. |
| The header settings do not match the first row of the file | Upload a file that includes a column name row, or change the header settings of the data source. |

<a id="datasource.edit.field"></a>

#### Add Fields { #datasource.edit.field }

In the Details view, go to the **Catalog** tab and click the **Add Fields** button.

| Item | Required | Description |
| --- | --- | --- |
| Field name | O | Must start with a letter or underscore (_), and contain only letters, numbers, and underscores (_) |
| Type | O | Select from the field types supported by the schema |
| Description | X | Description of the field |

- You can add up to 20 fields at a time using the **Add Row** button.
- System reserved field names and names of existing fields cannot be used.

!!! tip "Note"
    You can update data not only through the console but also via the API. For instructions, see 'Ingest API' in the [API Guide](./api-guide/#ingest.api).

<a id="pipeline"></a>

## Pipeline { #pipeline }

Console path: **Machine Learning > NHN Cloud Foundry > Pipeline** tab

A pipeline processes data from a data source through a workflow of connected nodes and converts it into an analyzable dataset.

<a id="pipeline.list"></a>

### Pipeline List { #pipeline.list }

When you enter the Pipeline menu, a table of created pipelines is displayed.

| Column | Description |
| --- | --- |
| Checkbox | Select a pipeline |
| Enabled | Icon indicating whether the pipeline is enabled |
| Pipeline name | Name that identifies the pipeline |
| Batch schedule | Configured schedule. Displayed as a hyphen if not set |
| Started on | Schedule start date and time |
| Ended on | Schedule end date and time |
| Last run date | Date and time of the most recent execution |
| Pipeline status | Current status of the pipeline |
| Manual run | Run button |

- Click a row to go to the edit screen.
- A running pipeline shows a progress indicator in the Manual Run column, and the button is disabled when the pipeline cannot be run.

You can create, modify, delete, enable, and disable pipelines from the toolbar. Enable and Disable options are available in the more options (⋯) menu.

<a id="pipeline.create"></a>

### Create Pipeline { #pipeline.create }

1. Click the **Create Pipeline** button on the list screen.
2. Enter the basic information in the **Settings panel** on the right.

    | Item | Required | Description |
    | --- | --- | --- |
    | Pipeline name | O | Name that identifies the pipeline (up to 255 characters) |
    | Pipeline description | X | Additional description of the pipeline (up to 255 characters) |
    | Tag | X | Tags for classification (up to 10 tags, 50 characters each) |

3. Click the **Create** button to create the pipeline in draft status.

!!! danger "Caution"
    Saving the settings of an enabled pipeline disables the pipeline. Click the Run button to build it, which will automatically enable it again.

<a id="pipeline.editor"></a>

### Pipeline Editor { #pipeline.editor }

This is the main editing screen that you enter when creating or editing a pipeline.

- **Header**: Pipeline name, description, and back button
- **Tab bar (left)**: Run/Stop, execution history, and add source node buttons
- **Tab bar (right)**: Last run date and time, status/build/activation badges, and Save button
- **Editor area**: Node-edge editor (supports drag and drop and auto-layout)
- **Side panel**: Settings, schedule, and computing resources panels

<a id="pipeline.status"></a>

#### Pipeline Status { #pipeline.status }

Hover over a status badge to see a detailed description in a tooltip.

| Value | Description |
| --- | --- |
| Draft | The pipeline has been created and no nodes exist. |
| Modified | The pipeline settings have been changed and a rebuild (run) is required. |
| Building | The pipeline is being built. Please wait. |
| Waiting | The pipeline build is complete and it is ready to run. |
| Running | The pipeline is currently running. |
| Completed | The pipeline ran successfully. |
| Failed | The pipeline run was stopped or an error occurred. |
| Finished | The user stopped the pipeline run. |
| Deleting | The pipeline is being deleted. |

<a id="pipeline.node"></a>

### Node Configuration { #pipeline.node }

A pipeline is built by combining the following five types of nodes.

| Node Type | Role | Input | Output | Description |
| --- | --- | --- | --- | --- |
| Source | Data origin | None | Data | Connects external data sources |
| Transform | Data processing | Data | Transformed data | Filtering, derived columns, aggregation, label encoding, etc. |
| Join | Table joining | 2 data streams | Combined data | Inner / Left / Right / Full Outer / Semi / Anti Join |
| Union | Table merging | 2 data streams | Merged data | Full Merge / Intersect Merge / Left-First Merge |
| Dataset | Output table | Data | None | Saves results as a table (final node) |

Connection constraints:

- A SOURCE node cannot have any input connections (root node).
- A DATASET node cannot have any output connections (final node).
- Circular references (loops) and self-connections are not allowed.

!!! danger "Caution"
    At least one DATASET node must exist for a pipeline to run.

<a id="pipeline.node.source"></a>

#### Add Source Node { #pipeline.node.source }

1. Click the **Add Source Node** button in the tab bar.
2. A modal displays a list of available data sources.
3. Select the source you want to add.

| Value | Description |
| --- | --- |
| FILE | CSV file data source |
| Recommendation | Recommendation result store |
| Dataset | Data generated by a Dataset node in a pipeline. Can be reused as input for another pipeline. |

<a id="pipeline.node.transform"></a>

#### Transform Node (TRANSFORM) { #pipeline.node.transform }

Each transform operation requires a node name (up to 30 characters; letters, numbers, `-`, `_`, and Korean characters are allowed). If you add multiple transform operations to a single node, they are applied as sequentially connected nodes.

The supported transform methods are as follows:

| Category | Method | Description |
| --- | --- | --- |
| Row | Filter | Extracts only rows that match the specified condition |
| Row | Explode | Splits a delimited string into separate rows |
| Row | Derive | Creates derived columns using whitelist functions |
| Aggregation | Aggregate | Groups and aggregates data |
| Window | Rank Top N | Globally sorts data and keeps the top N rows |
| Column | Label Encode FIT | Creates a category-to-integer mapping table |
| Column | Label Encode Apply | Applies encoding using a mapping table |
| LLM | Classify | Classifies text into categories using an LLM |

<a id="pipeline.node.transform.filter"></a>

##### Filter { #pipeline.node.transform.filter }

| Value | Description | Example |
| --- | --- | --- |
| = | Equal to | field = 'value' |
| ≠ | Not equal to | field ≠ 'value' |
| > | Greater than | field > 100 |
| ≥ | Greater than or equal to | field ≥ 100 |
| &lt; | Less than | field < 100 |
| ≤ | Less than or equal to | field ≤ 100 |
| LIKE | Pattern matching | field LIKE '%keyword%' |
| IN | Included in list | field IN ('a', 'b', 'c') |
| IS NULL | Checks for NULL | field IS NULL |
| IS NOT NULL | Checks for NOT NULL | field IS NOT NULL |

Only operators compatible with the selected column type are displayed.

| Column Type | Available Operators |
| --- | --- |
| String | =, ≠, LIKE, IN, IS NULL, IS NOT NULL |
| Number | =, ≠, >, ≥, &lt;, ≤, IN, IS NULL, IS NOT NULL |
| Date/Time | =, ≠, >, ≥, &lt;, ≤, IS NULL, IS NOT NULL |
| Boolean | =, ≠, IS NULL, IS NOT NULL |

For the comparison value, choose from **Direct Input**, **Time (relative to now)**, or **Another Column**.

Logical operators `AND` and `OR` are supported. You can use the **Add Group** button to nest conditions up to three levels deep.

<a id="pipeline.node.transform.explode"></a>

##### Explode { #pipeline.node.transform.explode }

Splits a string column containing delimiter-separated values into separate rows, one per token.

| Item | Required | Description |
| --- | --- | --- |
| Column to explode | O | The column containing delimiter-separated strings |
| Output column name | O | The name of the column that will hold each split token |
| Delimiter | O | Default is a comma (,) |
| Trim whitespace | X | When ON, strips leading and trailing whitespace from each token |
| Remove empty tokens | X | When ON, excludes empty string tokens from the output rows after splitting |
| Output type | X | STRING, BIGINT, INT, or DOUBLE. Defaults to STRING if not specified |
| Original columns to retain | X | Original columns to include in the output. If none are selected, all original columns are retained. |

- The delimiter is interpreted as a regular expression, so special characters must be escaped (e.g., `\.`, `\|`).
- If an output type is specified, the split values are converted to that type. For example, if numeric IDs are comma-separated, specifying BIGINT allows you to match the join key type.

<a id="pipeline.node.transform.derive"></a>

##### Derive { #pipeline.node.transform.derive }

Creates new columns from existing ones using the provided functions. You can add multiple definitions using the **Add Derived Column** button. Each definition requires a function and a derived column name.

| Value | Description | Additional Settings |
| --- | --- | --- |
| DATE_BUCKET | Date bucket (epoch ms → date in the specified timezone) | Source column, timezone (e.g., Asia/Seoul) |
| JSON_ARRAY_LENGTH | Number of elements in a JSON array | Source column, element schema |
| CONCAT | Concatenates multiple columns with a delimiter | 2 or more source columns, delimiter, default value (optional) |
| RATIO | Calculates the ratio of numerator to denominator | Numerator, denominator, multiplier (optional, default 1), rounding precision (optional) |
| COALESCE | Returns the first non-null value from multiple columns | 2 or more source columns |

- Definitions are applied in order from top to bottom. A derived column created earlier can be referenced as a source column in a subsequent definition.
- Derived column names can contain letters, numbers, underscores, and Korean characters.

<a id="pipeline.node.transform.aggregate"></a>

##### Aggregate { #pipeline.node.transform.aggregate }

1. **Select grouping criteria** (optional): Groups rows with the same value. If not selected, all data is aggregated as a single group.
2. **Define aggregation functions** (required): Specify the column to aggregate, the aggregation function, and the output column name. You can add multiple definitions.

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

When you select ARRAY_AGG, the following additional settings become available:

| Item | Required | Description |
| --- | --- | --- |
| Array element type | O | Single column or JSON object |
| Column to collect | O* | Required when the array element type is a single column. The column to include in the array. |
| JSON object field definition | O* | Required when the array element type is a JSON object. A combination of key names and columns. |
| Array element sort | X | Sort column and direction. If not specified, no sorting is applied. |
| Output format | O | STRUCT_ARRAY, JSON_STRING_ARRAY, or JSON_STRING |
| Remove duplicates (DISTINCT) | X | Ignored if sorting is configured. |

<a id="pipeline.node.transform.rank"></a>

##### Rank Top N { #pipeline.node.transform.rank }

Sorts all data by the specified criteria and keeps only the top N rows.

| Item | Required | Description |
| --- | --- | --- |
| Sort criteria | O | The column to sort by and the direction (DESC / ASC) |
| Top N | O | The number of rows to include in the result after sorting |
| Rank column name | O | The name of the rank column (1 through N) added to the result |

- Click the **Add Sort Criteria** button to specify multiple criteria. They are applied in order as the primary sort, secondary sort, and so on. You can drag to reorder them.
- When querying, sorting by the rank column preserves the original order.

<a id="pipeline.node.transform.label.encode"></a>

##### Label Encoding (Label Encode FIT / Label Encode Apply) { #pipeline.node.transform.label.encode }

Converts categorical data into numeric (integer) values. The process consists of two stages: **FIT (training)** and **APPLY**. You must create the FIT node first, then reference it in the APPLY node.

FIT node settings:

| Item | Required | Description |
| --- | --- | --- |
| Columns to encode | O | The columns to apply label encoding to (one or more) |
| Start index | X | The starting value for encoding (default: 0) |

APPLY node settings:

| Item | Required | Description |
| --- | --- | --- |
| Mapping table node | O | Select the FIT node |
| Overwrite original column | X | When checked, replaces the original column with the encoded value (default: unchecked) |
| Result column suffix | X | The suffix appended to the new column name when the original is retained (default: _encoded) |

!!! tip "Note"
    Values not present in the mapping table (OOV, Out-of-Vocabulary) are encoded as `-1`.

!!! danger "Caution"
    Re-running FIT may produce different encoding numbers as the data changes. Be careful about compatibility with existing models.

<a id="pipeline.node.transform.classify"></a>

##### Classify { #pipeline.node.transform.classify }

Uses an LLM to classify the values in a text column into categories. The list of categories used as classification criteria must be prepared as a separate data source node.

When the pipeline runs, it groups the input data rows into batches and calls the LLM once per batch. Each call's prompt includes the category list and the rows in that batch. The LLM responds with an appropriate category ID for each row, and the result is stored in the classification result column.

**LLM Settings**

| Item | Required | Description |
| --- | --- | --- |
| LLM provider | O | Claude |
| Model name | O | claude-haiku-4-5, claude-sonnet-4-6 |
| API key | O | The API key for the LLM to use. It is stored only for this pipeline and will not be displayed again after saving. |
| Batch size | X | Number of rows to include in a single LLM call (1–30) |
| Max retries | X | Number of retry attempts on call failure (0–10) |
| Timeout (seconds) | X | Wait time for a call (1–600) |
| Incremental classification | X | Classifies only changed rows using the LLM and reuses the previous run's results for unchanged rows |

**Input Columns**

| Item | Required | Description |
| --- | --- | --- |
| Input columns | O | The columns to pass to the LLM. Multiple columns can be selected. |
| Column join delimiter | X | The delimiter used to concatenate multiple input column values |
| User prompt template | X | A template for composing the input value per row. The `{{ column name }}` pattern is replaced with the corresponding column value. When set, takes precedence over the column join delimiter. Only columns selected as input columns can be referenced. |

**Axes (Category Table)**

Register the category list used as classification criteria as axes. Up to five axes can be added.

| Item | Required | Description |
| --- | --- | --- |
| Category node | O | The data source node containing the category list |
| Category ID column | O | The column that identifies each category |
| Category name column | O | The column containing the category name |
| Category metadata columns | X | Additional columns such as category descriptions or judgment criteria. Passed along in the prompt to improve classification accuracy. |
| Classification result column (array) | O | The name of the array column that stores the classification results |
| Representative column | X | The name of the column to store the most representative classification ID. If left empty, this column is not created. |

**Output**

| Item | Required | Description |
| --- | --- | --- |
| Output type | O | SINGLE_LABEL or MULTI_LABEL |
| Classification rationale column | X | The name of the column to store the classification rationale provided by the LLM. If left empty, the rationale is not requested, which reduces token costs. |
| Content rationale column | X | The name of the column to store a short description generated from the input content |
| Content rationale max length | X | Maximum number of characters for the content rationale column (1–200) |

**System prompt** (optional): Instructs the LLM on its role and classification criteria. If not set, the default prompt is used.

!!! danger "Caution"
    The more rows there are to process, the more LLM calls and token usage are required, which increases costs proportionally. For large-scale data, validate with a small subset first to verify costs and quality before applying at full scale.

<a id="pipeline.node.join"></a>

#### Join Node (JOIN) { #pipeline.node.join }

Combines two data streams.

| Item | Required | Description |
| --- | --- | --- |
| Node name | O | The name of the join result node (up to 30 characters) |
| Join type | O | Select from: Inner Join / Left Join / Right Join / Full Outer Join / Semi Join (EXISTS) / Anti Join (NOT EXISTS) |
| Join tables | O | Select the left and right table nodes |
| Join conditions | O | Maps left field = right field (multiple conditions are supported) |
| Column selection | X | Select columns to include in the result; a prefix can be configured |

!!! tip "Note"
    If both tables have columns with the same name, you can set a **prefix** on the right table to prevent column name conflicts.

<a id="pipeline.node.union"></a>

#### Union Node (UNION) { #pipeline.node.union }

Vertically merges two data streams.

| Value | Description |
| --- | --- |
| Full Merge | Includes all columns from both sides. Missing values on either side are filled with NULL. |
| Intersect Merge | Includes only columns common to both sides |
| Left-First Merge | Uses the left table's schema as the reference. Columns not present in the right table are filled with NULL. |

<a id="pipeline.node.dataset"></a>

#### Dataset Node (DATASET) { #pipeline.node.dataset }

The final output node of a pipeline. It saves the processed data as a table.

| Item | Required | Description |
| --- | --- | --- |
| Dataset name | O | Used as the table name (up to 30 characters) |
| Description | X | A description of the dataset (up to 500 characters) |
| Column selection | O | Select the columns to include in the dataset (at least one required) |

!!! danger "Caution"
    An executed dataset cannot be modified. Delete it and recreate it (the data source is retained).

<a id="pipeline.schedule"></a>

### Schedule Settings { #pipeline.schedule }

Click the schedule icon in the right side panel to configure a batch schedule.

| Frequency Type | Settings | Example |
| --- | --- | --- |
| Every minute | Interval (5 / 10 / 15 / 20 / 30 minutes) | Run every 10 minutes |
| Every hour | Interval (1 / 2 / 3 / 4 / 6 / 8 / 12 hours), minute | Run every 2 hours at the 30-minute mark |
| Every day | Hour, minute | Run every day at 09:30 |
| Every week | Day of the week (multiple selection), hour, minute | Run every Monday, Wednesday, and Friday at 09:00 |
| Every month | Day, hour, minute | Run on the 1st of every month at 09:30 |

Date range settings:

| Item | Required | Description |
| --- | --- | --- |
| Set start date | X | When checked, the schedule starts from the specified date. If not set, it starts from the time of saving. |
| Set end date | X | When checked, the schedule does not run after the specified date. |

After the schedule is saved and runs for the first time, subsequent runs are scheduled according to the configured frequency.

<a id="pipeline.resource"></a>

### Computing Resource Settings { #pipeline.resource }

Click the computing resource icon in the right side panel to configure the computing resources used when the pipeline runs.

| Type | Driver | Executor |
| --- | --- | --- |
| Small (default) | 1 CPU, 1 GB memory | 1 CPU, 1 GB memory × 1 |
| Medium | 1 CPU, 2 GB memory | 1 CPU, 2 GB memory × 2 |
| Large | 2 CPU, 4 GB memory | 2 CPU, 4 GB memory × 4 |
| XLarge | 4 CPU, 8 GB memory | 4 CPU, 8 GB memory × 8 |

!!! danger "Caution"
    Changes to resource settings take effect after a rebuild. You cannot change resources before the pipeline is created.

<a id="pipeline.run"></a>

### Run Pipeline { #pipeline.run }

For the first run or the first run after changing settings, the build and run proceed together.

1. Click the **Run** button in the tab bar.
2. Click the **Run** button in the confirmation modal.

A pipeline that has already been built runs immediately without a build process. If you click the **Stop** button while it is running, the status changes to Finished. When the build is complete, pipelines with a schedule configured are automatically enabled.

<a id="pipeline.run.history"></a>

#### View Execution History { #pipeline.run.history }

Click the **Execution History** button in the tab bar to view the execution ID, start/end time, elapsed time, execution status, and execution details for each node.

<a id="pipeline.activation"></a>

### Enable/Disable { #pipeline.activation }

- **Enable**: Select one pipeline from the list and click **Enable Pipeline** in the more options (⋯) menu. The pipeline runs automatically according to the configured schedule.
- **Disable**: Select one pipeline from the list and click **Disable Pipeline** in the more options (⋯) menu. The pipeline does not run automatically even if a schedule is configured.

<a id="pipeline.delete"></a>

### Delete Pipeline { #pipeline.delete }

1. Select the pipeline to delete from the list (multiple selections allowed).
2. Click the **Delete** button.
3. Click **Delete** in the confirmation modal.

<a id="query"></a>

## Analysis - Query { #query }

Console path: **Machine Learning > NHN Cloud Foundry > Analysis** tab > **Query** tab

Use SQL to query and analyze data from data sources.

<a id="query.run"></a>

### Run Query { #query.run }

1. Select a **Data Source**.
2. Load a saved query from **Select Query**. If there are queries saved for the selected data source, they appear in the list. You can also write a query directly without loading one.
3. Write SQL in the query input field.
4. Select a **Row Limit** (10, 100, 1,000, 10,000, 100,000 / default: 1,000).
5. Click the **Run Query** button.

- The execution results are displayed in a data grid format. The column structure is dynamically generated based on the query results, and pagination is supported.
- Click the **Reset** button to clear the query that you have written.
- Click the **Download Query Results** button to save the results as a CSV file (filename: `query name_date_time.csv`).
- In the FROM clause, use the table name exactly as it appears in the data source list (`SELECT * FROM {table name}`).
- Only a single SELECT statement can be executed. All other statements are rejected.

<a id="query.save"></a>

### Modify Saved Query { #query.save }

After modifying the content of a query loaded from **Select Query**, click the **Save Query** button to save the changes. The button is disabled if no query is loaded or if the content has not been changed.

<a id="query.list"></a>

### Query List { #query.list }

Each time a query is executed, it is automatically recorded in the execution history. You can also create queries that you want to reuse directly in the query list. Click the **Query List** button to open the modal for managing saved queries.

| Column | Description |
| --- | --- |
| Query Name | Name specified when saving |
| Query Statement | Saved SQL |
| Details | View the full query content |

- You can search by query name.
- Click the **Add** button to register a new query. Select a query, then click **Modify** or **Delete** to edit or remove it. Deleted queries cannot be recovered.

The fields to enter when adding or modifying a query are as follows:

| Field | Required | Description |
| --- | --- | --- |
| Query Name | O | Name used to identify the query |
| Data Source | O | Data source on which to run the query |
| Statement | O | SQL to execute |

<a id="query.history"></a>

### Query Execution History { #query.history }

This screen shows all queries that have been executed. Search by **Time** range and **Query Content**, and click the **Reset** button to clear the search conditions.

| Column | Description |
| --- | --- |
| Query Name | Name of the executed query |
| Query Execution Date | Date and time when the query was executed |
| Data Source Name | Data source on which the query was executed |
| Query/Result | Executed SQL and its result |

Click an item in the list to view the query details. Click **Use Query** to load the query into the execution screen.

<a id="chart"></a>

## Analysis - Chart { #chart }

Console path: **Machine Learning > NHN Cloud Foundry > Analysis** tab > **Chart** tab

<a id="chart.list"></a>

### Chart List { #chart.list }

- You can filter charts by name using the search feature at the top.

<a id="chart.create"></a>

### Create Chart { #chart.create }

Click the **Create Chart** button to go to the chart editor screen. In the editor, configure the following items in order.

<a id="chart.create.basic"></a>

#### Basic Settings { #chart.create.basic }

| Item | Required | Description |
| --- | --- | --- |
| Chart Name | O | Name to identify the chart (up to 30 characters) |
| Chart Type | O | Default |
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
| X-Axis | O* | Field to use for the horizontal axis. Not displayed in Pie charts |
| Aggregation Interval | O* | 5 minutes, 15 minutes, 30 minutes, 45 minutes, 1 hour, 2 hours, 6 hours, 12 hours, 1 day, 3 days, 7 days. Displayed only in Line and Bar charts |
| Reference Time | O | Specifies the time range for the data |
| Columns | O | Select the columns to aggregate and the aggregation function. At least one is required |
| Group Key | O* | Column to split values by. At least one is required for Pie charts; optional for others |
| Filter | X | Set conditions for filtering data |
| Sort | X | Sort column and direction. Displayed only in Pie and Bar charts |
| Row Limit | O | Maximum number of rows to retrieve |

The required settings for each chart visualization type are as follows:

| Chart Visualization Type | Required Settings |
| --- | --- |
| Line, Bar | X-axis (time axis), aggregation interval, at least one column |
| Pie | At least one column, at least one group key |
| Scatter | At least one column |

If you specify sorting for a Bar chart, it is displayed as Top-N categories instead of a time axis.

<a id="chart.create.preview"></a>

#### Chart Preview { #chart.create.preview }

After completing the configuration, click the **UPDATE CHART** button to check the preview.

- Check that the chart is displayed correctly.
- You can view the data in the table view at the bottom, and you can toggle the table view to show or hide it.

<a id="chart.create.save"></a>

#### Save Chart { #chart.create.save }

- After checking the preview, click the **Create** button in the header.
- The Create button is activated when input validation is complete.

<a id="chart.edit"></a>

### Edit Chart { #chart.edit }

Click a chart in the chart list to go to the edit screen.

- You can change the basic settings, data source settings, and query settings.
- Click **UPDATE CHART** to check the preview, then click **Save** to save the changes.

<a id="chart.delete"></a>

### Delete Chart { #chart.delete }

1. Select the charts to delete using the checkboxes in the chart list.
2. Click the **Delete** button.
3. Click **Delete** in the confirmation modal.

!!! danger "Caution"
    If you delete a chart that is in use in a dashboard, it will also be deleted from that dashboard.

<a id="dashboard"></a>

## Analytics - Dashboard { #dashboard }

Console path: **Machine Learning > NHN Cloud Foundry > Analytics** tab > **Dashboard** tab

<a id="dashboard.list"></a>

### Dashboard List { #dashboard.list }

- You can filter dashboards by name using the search feature.
- You can adjust the number of items displayed per page.

<a id="dashboard.create"></a>

### Create Dashboard { #dashboard.create }

Click the **Create Dashboard** button to go to the dashboard editor screen.

| Item | Required | Description |
| --- | --- | --- |
| Dashboard name | O | A name to identify the dashboard |
| Dashboard description | X | A description of the dashboard |

The editing panel consists of two tabs.

| Tab | Description |
| --- | --- |
| CHARTS | List of charts that can be added to the dashboard. You can search by chart name |
| LAYOUT ELEMENTS | Layout elements to add to the canvas |

<a id="dashboard.create.chart"></a>

#### Add Chart { #dashboard.create.chart }

1. Click or drag the chart card that you want to add.
2. Place the chart on the dashboard canvas.

<a id="dashboard.create.tabgroup"></a>

#### Add Tab Group { #dashboard.create.tabgroup }

You can group multiple charts into tabs and switch between them in one place. Click **Tab** in the **LAYOUT ELEMENTS** tab of the editing panel to add a tab group to the canvas.

- Use **Add Tab** in the tab group to add more tabs. When there are two or more tabs, a delete icon appears on each tab. If only one tab remains, it cannot be deleted.
- Double-click a tab to change its name.
- Drag a chart from the editing panel and drop it onto a tab area to place it in that tab. To move a chart that is already on the canvas into a tab, drag it by the handle on the left side of the chart title. Use the same method to move a chart from a tab back to the canvas.
- To delete a tab group from the dashboard, click the trash icon in the top right corner of the tab group, just as you would with a chart.

<a id="dashboard.create.layout"></a>

#### Adjust Layout { #dashboard.create.layout }

Drag a chart placed on the canvas to reposition it, and drag its corners to resize it. Click the trash icon in the top right corner of the chart to delete it from the dashboard.

<a id="dashboard.create.save"></a>

#### Save Dashboard { #dashboard.create.save }

After completing the configuration, click the **Save** button in the header.

<a id="dashboard.view"></a>

### View Dashboard { #dashboard.view }

In the dashboard list, click a dashboard to go to its detail screen.

<a id="dashboard.edit"></a>

### Edit Dashboard { #dashboard.edit }

On the dashboard detail screen, click the **Edit Mode toggle** to switch to edit mode.

In edit mode, you can perform the following actions:

- Add, delete, and reposition charts
- Change the dashboard name

To modify a chart placed on the dashboard, turn off edit mode. When edit mode is off, a more options menu appears on each chart. Choose **Edit Chart** to go to the chart editing page. Charts inside a tab group can be accessed the same way. After editing and saving a chart, the changes are reflected in the dashboard.

<a id="dashboard.delete"></a>

### Delete Dashboard { #dashboard.delete }

1. In the dashboard list, select the dashboard that you want to delete.
2. Click the **Delete** button.
3. In the confirmation modal, click **Confirm**.

<a id="app"></a>

## App { #app }

Console path: **Machine Learning > NHN Cloud Foundry > App** tab

Create and manage recommendation system serving pipelines that use AI models.

<a id="app.list"></a>

### App List { #app.list }

| Column | Description |
| --- | --- |
| App Type | Type of the app |
| App ID | Unique identifier of the app |
| App Name | Name used to identify the app |
| App Description | Description of the app |
| Status | Current status of the app |
| Created On | Date and time the app was created |

<a id="app.list.status"></a>

#### App Status { #app.list.status }

Hover over the app status badge to view a detailed description in a tooltip.

| Value | Description |
| --- | --- |
| Initializing | App initialization is in progress. |
| Training | AI model training is in progress. |
| Deploying | App deployment is in progress. |
| Activating | App activation is in progress. |
| Active | The app is in an active state. |
| Deleting | App deletion is in progress. |
| Failed | An error occurred while processing the app. |
| Unknown | Status information cannot be retrieved. |

- After an app is created, training and deployment proceed automatically.
- If an error occurs at any stage, the app transitions to a failed status.

<a id="app.create"></a>

### Create App { #app.create }

Click the **Create App** button to go to the app creation screen. App creation proceeds in three steps.

| Step | Description |
| --- | --- |
| Basic Settings | Enter the app name, description, and select the app type |
| Detail Settings | Select a model, configure serving resources, batch schedule, data connections, and additional settings |
| Final Review | Review your inputs and create the app |

<a id="app.create.basic"></a>

#### Basic Settings { #app.create.basic }

| Item | Required | Description |
| --- | --- | --- |
| App Name | O | Name used to identify the app (only English letters, numbers, and hyphens are allowed) |
| App Description | O | Description of the app |
| App Type | O | Select **Recommendation System** |

<a id="app.create.detail"></a>

#### Detail Settings { #app.create.detail }

Click the **Add Model** button to add a model card. You can configure multiple models in a single app. Configure the sections below for each model card.

<a id="app.create.detail.model"></a>

##### Basic Model Settings { #app.create.detail.model }

| Item | Required | Description |
| --- | --- | --- |
| Model Name | O | Select the recommendation model to use |
| Longtail Mode | X | When enabled, items with low popularity are also included in recommendations |

The following models are available for selection.

| Name | Description |
| --- | --- |
| Cold User | Recommends items to users with limited activity history, such as new users, based on the intrinsic attributes of the items themselves. |
| Warm User (Transformer) | Recommends the next item based on the sequence of items that the user has recently interacted with. |
| Warm User (Graph) | Recommends items similar to those that the user has interacted with, based on graph relationships. |

Even if two entries share the same model, they can be added as separate models if their Longtail Mode settings differ.

<a id="app.create.detail.resources"></a>

##### Serving Resource Settings { #app.create.detail.resources }

Specify the resources to allocate to the serving container for each model. If left blank, the default values are applied.

| Item | Required | Description |
| --- | --- | --- |
| CPU request / CPU limit | X | In cores. Default: 2 / 4 |
| Memory request / Memory limit | X | In Gi. Default: 4 / 4 |

The request value cannot exceed the limit value.

<a id="app.create.detail.schedule"></a>

##### Batch Schedule Settings { #app.create.detail.schedule }

Set the execution interval for the batch that periodically retrains the model. This is enabled by default and can be turned off using the toggle.

| Interval | Settings |
| --- | --- |
| Daily | Hour, minute |
| Weekly | Day of week, hour, minute |
| Hourly | Hour interval, minute |

The configured time is applied based on the timezone of the browser you are using.

<a id="app.create.detail.connection"></a>

##### Data Connection Settings { #app.create.detail.connection }

Connect the required data sources based on the selected model.

General recommendation model:

| Item | Required | Description |
| --- | --- | --- |
| User Data Source | O | Data source for user information |
| User ID Column | O | Column used to identify users |
| User Feature Column | X | Additional user attribute columns (multiple selections allowed) |
| Item Data Source | O | Data source for item information |
| Item ID Column | O | Column used to identify items |
| Item Feature Column | X | Additional item attribute columns (multiple selections allowed) |
| History Data Source | O | Data source for user-item interaction data |
| History User ID Column | O | Column used to identify users in the history data |
| History Item ID Column | O | Column used to identify items in the history data |
| Time Column | X | Column for interaction timestamp |
| History Feature Column | X | Additional interaction attribute columns |

Tag embedding model:

| Item | Required | Description |
| --- | --- | --- |
| Tag Data Source | O | Data source for tag information |
| Attribute Column | O | Column for tag values |
| Item ID Column | O | Column used to identify items |
| Time Column | X | Column for timestamp |

<a id="app.create.detail.extra"></a>

##### Additional Settings (Skills) { #app.create.detail.extra }

This is an optional setting for connecting skill and category data to be used in composing recommendation reasons. Click the **Add Fields** button to add entries.

| Item | Description |
| --- | --- |
| Skill Data Source | Skill information table. Specify the skill ID column and skill column. |
| Default Skill Category / Common Skill Category | Skill classification table. Specify the skill ID column and skill label column. |
| User Group Data Source | A unit for grouping users targeted for recommendations (e.g., department, grade, interest group). Specify the user group ID column and skill column. |
| User Interest Skill Data Source | A table of skills that each user is interested in. When no interest skills are passed to the recommendation API, this table is queried to generate interest-based recommendation reasons. |
| User Attribute Mapping | Specifies the key names used to pass each item in the `userAttributes` of the recommendation API. |
| Recommendation Reason Template Data Source | A template table for recommendation reason text. If not selected, the recommendation results will not include reasons. |
| Cold Start Data Source | Only user IDs present in this table are classified as cold starters. You must select both the data source and the user ID column. |

<a id="app.create.review"></a>

#### Final Review { #app.create.review }

| Review Item | Description |
| --- | --- |
| Basic Settings | App name, description, and type |
| Model Settings | Selected model, serving resources, batch schedule, and data connection information |
| Additional Settings | Additional settings such as skill tables |

Click the **Save** button to create the app. On success, a completion modal is displayed and you are redirected to the list. On failure, an error message is displayed.

<a id="app.delete"></a>

### Delete App { #app.delete }

1. Select the checkbox of the app you want to delete.
2. Click the **Delete** button.
3. Click **Confirm** in the confirmation modal.

!!! danger "Caution"
    Deleted apps cannot be recovered. The associated serving pipeline is also deleted.

<a id="app.detail"></a>

### App Details { #app.detail }

Click an app in the app list to go to the details screen. The details screen consists of two tabs: **Recommendation API Call** and **App Information**.

<a id="app.detail.recommend"></a>

#### Recommendation API Call { #app.detail.recommend }

You can enter recommendation request parameters to directly call the recommendation API and view the results. The screen is divided into three areas: the input form, request preview, and recommendation results.

Input form:

| Item | Description |
| --- | --- |
| Recommendation App ID | The ID of the app to call. Automatically populated with the current app. |
| User ID | Select the user to receive recommendations |
| Recommendation Mode | Choose between Normal Flow (history-based) or Cold Start (attribute-based) |
| Maximum Recommendations | Maximum number of items to include in the response |
| Longtail Mode | Includes less popular items to increase recommendation diversity. Not available in Cold Start mode. |
| context | Add contextual information for the recommendation request (e.g., current or recently viewed items) as individual fields |
| userAttributes | Add user attribute information (e.g., group, age, interests) as individual fields |
| options | Add recommendation request options as individual fields |

- **Request Preview**: Displays the actual API request JSON constructed from your inputs. Click the **Copy** button to copy it and use it for API integration development.
- **Recommendation Results**: Click the **Request Recommendation** button to display the rank, item key, score, and recommendation reason, along with the total number of results and response time.

!!! tip "Note"
    The recommendation API can only be called when the app is in an active state.

<a id="app.detail.info"></a>

#### App Information { #app.detail.info }

You can view the app ID, app name, status, app type, description, creation date, modification date, and version.