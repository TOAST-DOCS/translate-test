<!-- machine_translated: true -->

## Anomaly Detection

**Monitoring > Cloud Monitoring > Anomaly Detection** learns the patterns of metrics collected by Cloud Monitoring and automatically detects abnormalities that deviate from normal behavior.

Unlike standard notifications where you define thresholds manually, anomaly detection automatically calculates a **Score** and a **Score Threshold** at each point in time based on the historical patterns of the metric. Both the Score and Score Threshold are values in the range of 0 to 100. When the Score exceeds the Score Threshold, the system determines that an anomaly has occurred.

Use anomaly detection in the following order:

1. Create anomaly detection items by selecting the metrics and resources to monitor.
2. Check the Score and Score Threshold in the widget chart to identify time intervals where anomalies occurred.
3. Configure anomaly detection notifications to receive alerts when an anomaly is detected.

!!! tip "Note"
    Created anomaly detection items are evaluated every minute.

### Create Anomaly Detection

Click **Create Anomaly Detection** to go to the anomaly detection creation screen. You can create anomaly detection items by selecting a service and target.

- **Service**: Only NHN Cloud services that support anomaly detection are displayed. Only a single service can be selected.
- **Target**: Configure in the following order:
  - **Type**: Select the metric type for the service.
  - **Metric Item**: Metric items belonging to the selected type are displayed, and you can select multiple items. The number of selected resources is displayed next to each metric item.
  - **Resource**: Resources within NHN Cloud that belong to the selected type/metric item are displayed, and you can select multiple resources.

One anomaly detection item is created for each combination of selected metric item and resource, and the anomaly detection name is automatically generated based on the selected metric item and resource.

You cannot create additional items using a combination that already exists. Such cases are displayed as **Already Created**.

You can preview the name, metric, and resource of the anomaly detection items to be created in **Preview Created Items**.
When **Create** is complete, each item shown in the preview is created as an individual anomaly detection item. At this point, you can choose whether to immediately navigate to the notification configuration screen for those items.

!!! danger "Caution"
    Creation is processed as either complete success or complete failure.
    If even one of the selected items cannot be created, none of the items are created.

Immediately after creation, the status of an anomaly detection item is **Active - Waiting**. Once the training and inference required for anomaly detection are complete, the status changes to **Active - Normal**. The Score and Score Threshold may not appear in the chart until the status changes to Active - Normal.
For more information, see **Anomaly Detection Status** below.

### Anomaly Detection List

The anomaly detection screen consists of a list area on the left and a dashboard area on the right. Each anomaly detection item in the list is displayed as a single widget in the dashboard on the right.

For each item in the list, you can view the anomaly detection name, service, creation date and time, and status. The checkboxes next to items are used for bulk operations such as deletion.

- Filters, sorting, and search are applied simultaneously to both the left list and the right dashboard.
- **Filter**: You can filter the items displayed in the list and dashboard using the service and target filters. Filters are configured based on the existing anomaly detection items. For example, if only Instance service items exist, only Instance is displayed in the service filter.
- **Sort**: You can sort by newest or oldest.
- **Search**: You can search by anomaly detection name.


### Anomaly Detection Dashboard

The anomaly detection dashboard automatically displays all created anomaly detection items as individual widgets.

- Select **Show Active (Normal) Only** to display only widgets for items in the **Active - Normal** status.
- In **Download Widget Data**, you can download the widget data displayed on the dashboard as a .csv or .xlsx file.

!!! tip "Note"
    You can add anomaly detection widgets not only to the anomaly detection dashboard, but also to dashboards you have configured yourself in the Dashboard tab.

#### Anomaly Detection Widget Chart

The widget chart displays the following elements together:

- **Metric Value**: The actual collected value of the metric selected as the anomaly detection target. Displayed based on the left Y-axis.
- **Score**: A value from 0 to 100 that represents the degree to which the current data deviates from past patterns. A value closer to 100 indicates a greater anomaly compared to normal patterns. Displayed based on the right Y-axis.
- **Score Threshold**: When the Score exceeds the threshold, the system determines that an anomaly has occurred. Displayed based on the same right Y-axis as the Score.

The interval where the Score exceeds the Score Threshold is the interval determined to be in an anomalous state.

#### Delete Anomaly Detection

You can delete selected items from the anomaly detection list.

- If you recreate an item using the same metric item and resource combination as a deleted item, it is automatically re-linked to the widgets and notifications that were previously associated with the deleted item. (However, the data acquisition process may start again.)

!!! danger "Caution"
    Deleting an anomaly detection item does not automatically delete widgets or notifications that use that item.
    Widgets using a deleted item will no longer display anomaly detection data, and notifications will no longer be generated. If these are no longer needed, you must clean them up manually.

#### Configure Anomaly Detection Activation

You can change the activation status of selected items from the anomaly detection list.

- **Enable**: When you create an anomaly detection item, it is automatically set to enabled by default. When switching from disabled to enabled, the data acquisition process may start again.
- **Disable**: Anomaly detection for the item stops immediately. Anomaly detection data is no longer displayed in widgets created with that item, and notifications are no longer generated.

#### Configure Anomaly Detection Notifications

You can configure notifications for selected items from the anomaly detection list.

- You are taken to the notification creation screen with the selected items pre-configured. Since one notification can only be created for metrics of a single service, this is only available when you select anomaly detection items from the same service.


### Anomaly Detection Status

| Status | Description | 
| --- | --- |
| Active - Normal | - Anomaly detection is enabled and operating normally. <br> - Anomaly detection data is displayed in widgets and notifications are generated. |
| Active - Waiting | - Anomaly detection is enabled and data acquisition is in progress. <br> - It may take approximately 6 hours to acquire the data required for anomaly detection training and inference. Anomaly detection data is displayed and notifications are generated once data acquisition is complete. | 
| Active - Insufficient Data | - Anomaly detection is not operating due to insufficient collected metric data for the anomaly detection target. <br> - This may be caused by a service failure or resource deletion. Check the resource status in each service console. <br>(If the resource has been deleted, delete the corresponding anomaly detection configuration. If this status persists even when there are no issues, contact customer support.) | 
| Active - Suspended | - Anomaly detection operation has been temporarily suspended due to a transient issue. <br> - The system recovers automatically. After recovery, an additional data acquisition process may occur to support analysis. <br>(If this status persists for an extended period, contact customer support.) |
| Disabled | - Anomaly detection is disabled and not operating. <br> - You can restart anomaly detection by enabling it. <br>(Note that time is required to acquire additional data after enabling, and anomaly detection data will be displayed and notifications will be generated only after data acquisition is complete.) | 

!!! tip "Note"
    In all states except Active - Normal, no anomaly detection data is generated and therefore no notifications are generated.



## Using Anomaly Detection

### Add Anomaly Detection Widgets

You can freely add anomaly detection widgets to dashboards that you have created yourself.

- In the Add Widget screen, select **Anomaly Detection** for **Target Type**.
- The **Graph Type** is fixed to `Anomaly Detection`.
- When you select a service, the list of anomaly detection items created for that service is displayed. If the desired anomaly detection item is not in the list, you must first create it in the Anomaly Detection tab.
- One Metric Setting Block is added for each selected anomaly detection item.
- The Query Setting Block automatically includes three legends: metric value, Score, and Score Threshold. Widgets created with anomaly detection always display these three data elements together. (However, they may not be displayed depending on the status.) The legend names, units, and Y-axis positions of the Score and Score Threshold are fixed values.
- For metrics that support aggregation, you can use aggregation settings. The configured aggregation is applied to the metric value, Score, and Score Threshold.

!!! danger "Caution"
    If an anomaly detection item used by a widget is deleted, the widget can still be viewed and saved, but the query settings for the deleted item cannot be changed.

#### Specify Threshold Manually

Because anomaly detection determines the threshold independently for each data point, the baseline value varies over time. To use a fixed baseline, select **Specify Threshold Manually** and enter a value.

- Only numbers from 0 to 100 (inclusive) can be entered as a threshold.
- When specified manually, anomalies are determined based on the entered value regardless of the data point.
- When deselected, the chart displays anomalies based on the threshold determined by anomaly detection.

### Anomaly Detection Notifications

To receive notifications when an anomaly is detected, create an anomaly detection notification. Anomaly detection notifications can be created in the same way as standard metric notifications, from the Notification Management tab > Create Notification screen.

#### Configure Threshold

Because anomaly detection determines the threshold independently for each data point, the baseline value varies over time. To use a fixed baseline, select **Specify** for each condition and enter a value.

- Only numbers from 0 to 100 (inclusive) can be entered as a threshold.
- When specified manually, anomalies are determined based on the entered value regardless of the data point, and a notification is generated.
- When deselected, a notification is generated when the Score exceeds the threshold determined by anomaly detection for 5 consecutive minutes.

#### Check Anomaly Detection Notifications

- Anomaly detection notifications can be checked in the same way as standard metric notifications, in the Notification Settings tab and the Notification History tab. Anomaly detection notifications are displayed with a distinct badge for easy identification.
- In Notification History, you can filter to show only anomaly detection notifications using the **Target Type** filter.

!!! danger "Caution"
    Notifications are generated only when the anomaly detection item is in **Active - Normal** status. Notification conditions are not evaluated when the item is in a data acquisition, disabled, insufficient data, or suspended state. You can check the item status on the **Anomaly Detection** screen.
    If an anomaly detection item used by a notification is deleted, the notification can still be viewed and saved, but the notification conditions for the deleted item cannot be changed.


### Notes

- Immediately after creating an item, the Score and Score Threshold may not be displayed until training and inference for anomaly detection are complete.
- If the source metric used by anomaly detection is not collected for 30 consecutive minutes, the status changes to insufficient data, and the Score and Score Threshold are no longer generated. Once metric collection resumes, the status recovers to either 'Active - Waiting' or 'Active - Normal'.