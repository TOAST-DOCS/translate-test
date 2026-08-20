<!-- machine_translated: true -->

<a id="foundry.getting.started"></a>

## Machine Learning > NHN Cloud Foundry > Get Started { #foundry.getting.started }

This document describes the process of creating a **recommendation system app** in NHN Cloud Foundry and using the recommendation results.
After completing the prerequisites (service application and data preparation), proceed in the following order:

1. Create a data source
2. Create an app
3. Check the app status
4. Query recommendation results
5. Collect recommendation events

<a id="preparation"></a>

## Prerequisites { #preparation }

<a id="preparation.service.enable"></a>

### Service Application { #preparation.service.enable }

NHN Cloud Foundry cannot be activated directly from the console. To use the service, you must apply through [1:1 inquiry](https://www.nhncloud.com/kr/support/inquiry).

1. In the NHN Cloud console, select the organization and project for which you want to use the service.
2. On the **Machine Learning > NHN Cloud Foundry > Status** tab, click the **1:1 Inquiry** button and submit your application, including the desired resource size.
3. Once a representative activates the service for your project, all features become available.

![Service application](../static/images/quick-start/서비스이용신청.png){ height="70%" }

<a id="preparation.data"></a>

### Prepare Data { #preparation.data }

To create a recommendation system app, you need the following three CSV data files:

| Data | Required Columns | Description |
| --- | --- | --- |
| User table | User ID | User information (additional attribute columns are optional) |
| Item table | Item ID | Item information (additional attribute columns are optional) |
| History table | User ID, Item ID, Timestamp | User-item interaction history (rating and category columns are optional) |

<a id="datasource.create"></a>

## 1. Create a Data Source { #datasource.create }

Go to the **Machine Learning > NHN Cloud Foundry > Data Source** tab.
For detailed descriptions of each setting, see "Create Data Source" in the [Console User Guide](./console-user-guide/#datasource.create).

1. Click the **Create Data Source** button.

    ![Create data source](../static/images/quick-start/데이터소스생성모달1.png){ height="70%" }

2. In the basic settings, enter a data source name and table name.
3. In the detailed settings, select a CSV file. If the first row of the file contains column names, check **First row is a header**. Enter the primary key field (e.g., `user_id`).
4. Click the **Infer Type** button to automatically populate the schema from the CSV sample. Correct any types that were inferred incorrectly.

    ![Create data source - file selection and type inference](../static/images/quick-start/데이터소스생성모달2.png){ height="70%" }

5. Click the **Add** button to create the data source.
6. Repeat the same steps to create data sources for **user, item, and history** data respectively.
7. Wait until the status in the list shows COMPLETED.

    ![Data source list](../static/images/quick-start/데이터소스목록.png){ height="70%" }

<a id="app.create"></a>

## 2. Create an App { #app.create }

Go to the **Machine Learning > NHN Cloud Foundry > App** tab and click the **Create App** button.
For detailed descriptions of each setting, see "Create App" in the [Console User Guide](./console-user-guide/#app.create).

<a id="app.create.basic"></a>

### Basic Settings { #app.create.basic }

Enter the app name and description, select **Recommendation System** as the app type, and click **Next**.

![Create app - basic settings](../static/images/quick-start/앱생성화면1.png){ height="70%" }

<a id="app.create.detail"></a>

### Detailed Settings { #app.create.detail }

1. Click the **Add Model** button to add the model you want to use. For a new service, we recommend the **Cold User** model; if you have sufficient user interaction history, we recommend the **Warm User (Transformer/Graph)** model.

    ![Create app - model settings](../static/images/quick-start/앱생성화면2.png){ height="70%" }

2. In **Data Connection Settings** on the model card, select the user, item, and history data sources you created in "1. Create a Data Source", and specify the user ID, item ID, and history timestamp columns. Select feature columns only if needed.

    ![Create app - data connection settings](../static/images/quick-start/앱생성화면3.png){ height="70%" }

3. If needed, connect a skill table or other resources in **Additional Settings (Skills)**, and specify the Longtail mode (includes less popular items in recommendations) in the basic model settings. When you are done, click **Next**.

    ![Create app - additional settings](../static/images/quick-start/앱생성화면4.png){ height="70%" }

<a id="app.create.review"></a>

### Final Review { #app.create.review }

1. Review the basic settings, model settings, and additional settings that you entered.
2. Click the **Save** button to create the app.

![Create app - final review](../static/images/quick-start/앱생성화면5.png){ height="70%" }

<a id="app.status"></a>

## 3. Check the App Status { #app.status }

After the app is created, training and deployment proceed automatically. The status changes through Initializing, Training, Deploying, and Activating before becoming Active.
Wait until the status in the app list shows Active.

![App list](../static/images/quick-start/앱목록.png){ height="70%" }

For detailed descriptions of each status value, see "App Status" in the [Console User Guide](./console-user-guide/#app.list.status).

<a id="recommendation.query"></a>

## 4. Query Recommendation Results { #recommendation.query }

Once the app is in the Active status, you can check recommendation results on the Recommendation API call screen in the console, or query recommendation results by calling the recommendation query API.
For detailed descriptions of each item, see "Call Recommendation API" in the [Console User Guide](./console-user-guide/#app.detail.recommend).

1. In the app list, click the app you created to go to the **Recommendation API Call** tab on the details screen.
2. Enter a user ID and specify the recommendation mode and maximum number of recommendations.
3. Click the **Request Recommendation** button. The recommendation results display the rank, item key, and score, along with the total number of results and response time.

    ![Call Recommendation API](../static/images/quick-start/추천API호출.png){ height="70%" }

The **Request Preview** section displays the actual API request JSON composed from the input values. You can click the **Copy** button to copy it and use it for API integration development.
For information on how to call the recommendation query API directly, see "Recommendation Query API" in the [API Guide](./api-guide/#recommendation.api).

The response includes the request identifier (`metadata.requestId`) and the list of recommended items (`recommendations[].itemKey`). These values are used to send recommendation events in the next step.

On the **App Info** tab, you can check the app ID, status, and version used for API calls.

![App info](../static/images/quick-start/앱정보.png){ height="70%" }

<a id="recommendation.event"></a>

## 5. Collect Recommendation Events (Success Rate Analysis) { #recommendation.event }

When a user reacts to a recommendation result — for example, by clicking on it — send the event using the recommendation event API. The loaded event data can be used to analyze the recommendation success rate.
For detailed descriptions of the request fields, see "Recommendation Event API" in the [API Guide](./api-guide/#recommendation.event.api).

```bash
curl -X POST '{URL}/api/v1.0/recommendation-apps/{APP_ID}/events' \
  -H "X-NC-APP-KEY: {APP_KEY}" \
  -H "Content-Type: application/json" \
  -H "X-NHN-Authorization: {AUTH_TOKEN}" \
  -d '{
    "eventType": "CLICK",
    "requestId": "{RecommendApiResponse.body.metadata.requestId}",
    "itemKey": "{RecommendApiResponse.body.recommendations.itemKey}",
    "userId": "{RecommendApiResponse.body.userId}",
    "context": {
      "position": 1,
      "placement": "home_main"
    }
  }'
```

!!! tip "Note"
    It can take up to 10 minutes for data to be loaded into the dataset after a request to the event API.