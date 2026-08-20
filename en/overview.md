<!-- machine_translated: true -->

<a id="foundry.overview"></a>

## Machine Learning > NHN Cloud Foundry > Overview { #foundry.overview }

NHN Cloud Foundry is an AI data platform service that allows you to perform everything from data collection, processing, and analysis to AI model serving in one place.
You can load data, process it with a visual workflow, analyze it using queries, charts, and dashboards, or create apps connected to AI models and use inference results in your services.

> [Image required] NHN Cloud Foundry service architecture (overall configuration diagram) image

<a id="main.feature"></a>

## Key Features { #main.feature }

| Feature | Description |
| --- | --- |
| **Data Source** | A unit for storing data to be analyzed. You can define a schema to create a data source and load data into it. For an existing data source, you can add or update data using the Ingest API. |
| **Pipeline** | Processes data from a data source using a visual workflow of connected nodes and converts it into an analyzable dataset. Supports automatic execution according to a batch schedule. |
| **Analysis** | You can query data using SQL **queries**, visualize it with **charts**, and monitor everything in one place using **dashboards**. |
| **App** | Creates and manages apps by connecting AI models to data. You can view inference results in the console or via API. |

<a id="datasource"></a>

## Data Source { #datasource }

A data source is a unit for storing data to be analyzed in NHN Cloud Foundry.
When you define a schema and create a data source, data is loaded into a table, which is then used by pipelines, analysis, and apps.

You create a data source in the console, and you can upload data at the same time.
When you need to add or update data in an existing data source, use the Ingest API.

<a id="pipeline"></a>

## Pipeline { #pipeline }

Pipeline is a feature that processes data from a data source using a visual workflow of connected nodes and converts it into an analyzable dataset.

- Connect source data and automatically detect schema
- Apply transformation operations such as row filtering, column processing, aggregation, join, and union
- Automatically execute according to a batch schedule configuration
- Configure computing resources and manage execution history

<a id="analysis"></a>

## Analysis { #analysis }

Query, visualize, and monitor data stored in a data source.
You can use it by querying data to check it, creating charts, and placing them on a dashboard.

| Feature | Description |
| --- | --- |
| Query | Query data from a data source using SQL and manage the execution history. |
| Chart | Visualize queried data. |
| Dashboard | Place multiple charts on a single screen for integrated monitoring. |

<a id="app"></a>

## App { #app }

App is a feature for creating and managing apps that provide inference services by connecting AI models to data.
When you select a model and connect a data source, training and deployment proceed automatically. Once the app is in an active state, you can use the inference results.

You can view inference results by calling them directly in the console or by making requests via API.

<a id="public.api"></a>

## API { #public.api }

NHN Cloud Foundry provides APIs in addition to the console.
You can use the Ingest API to add or update data in an existing data source, as well as APIs to request inference results from a created app and send user interaction events.

For more information, see the [API Guide](./api-guide/).

<a id="target"></a>

## Service Targets { #target }

- Teams that need an environment for loading, processing, and analyzing data without building their own data infrastructure
- Services that want to consolidate scattered data in one place, process it on a regular basis, and monitor it through metrics
- Teams that want to apply AI inference results to their services without a separate model training and serving environment