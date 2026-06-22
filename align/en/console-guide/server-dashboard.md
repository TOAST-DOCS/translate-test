# Server Dashboard

**Database > EasyCache > Console User Guide > Server Dashboard**

Server Dashboard helps to visualize performance metrics on a chart. The charts are arranged according to a preset layout. Metrics are collected at every minute and retained for up to 5 years. Metric data are collected by the average of 5 minutes, 30 minutes, 2 hours, or 1 day. Each collecting unit provides a different retention period like below:

| Collecting Unit | Retention Period |
|-------|-------|
| 1 minute    | 7 days    |
| 5 minutes    | 1 month   |
| 30 minutes   | 6 months   |
| 2 hours   | 2 years    |
| 1 day    | 5 years    |

## Layout

You can use layouts to define the size and position of charts. When the service is activated, **Default System Metrics** and **Default Redis Metrics** are provided as default layouts. Default layouts cannot be modified or deleted. In addition, charts cannot be added to, modified in, or deleted from default layouts. To view information not included in a default layout, you can create a new layout and add charts to it.

![server-dashboard-layout](https://static.toastoven.net/prod_rds_postgres/20240611/server-dashboard-layout-ko.png)

❶ Click **Manage Layout** to open the layout management pop-up.
❷ Click **+ Create Layout** to create a layout.
- Enter a layout name and click **Create** to create the layout.
❸ Click the button to modify an added layout.
❹ Click the button to delete an added layout.

### Add a Chart to a Layout

![server-dashboard-chart-add](https://static.toastoven.net/prod_rds_postgres/20240611/server-dashboard-chart-add-ko.png)

❶ Select the desired layout.
❷ Click **+ Add Chart** to open a pop-up where you can add charts.
❸ Select checkboxes to choose multiple metrics to add.
❹ Click a metric name to display the chart in the preview area on the left.
❺ Click **Add** to add all selected charts.

### Change and Delete Layout Charts

![server-dashboard-chart-manage](https://static.toastoven.net/prod_rds_postgres/20240611/server-dashboard-chart-manage-ko.png)

❶ Click and drag the top area of a chart to move it to a different position.
❷ Drag and drop the bottom-right area of a chart to resize it.
❸ Click **x** in the top-right corner of a chart to remove it from the layout.

## Chart

You can view various performance metrics of nodes in chart format. The format of chart is different for each performance metric. In addition to the basic system metrics, the performance metrics provided by Redis are provided as charts. The following are the metrics:

| Chart                 | Metric (Unit)                                                                                           | Note                                |
|--------------------|--------------------------------------------------------------------------------------------------|-----------------------------------|
| CPU utilization            | CPU used (%)                                                                                     |                                   |
| CPU details             | CPU user (%)<br/>CPU system (%)<br/>CPU Nice (%)<br/>CPU IO wait (%)                             |                                   |
| CPU average load          | 1 m<br/>5 m<br/>15 m                                                                                |                                   |
| Memory usage            | Memory used (%)                                                                                  |                                   |
| Memory details             | Memory used (bytes)<br/>Memory free (bytes)<br/>Memory cached (bytes)<br/>Memory buffers (bytes) |                                   |
| Swap usage             | Swap used (bytes)<br> Swap total (bytes)                                                         |                                   |
| Storage usage        | Storage used (%)                                                                                 |                                   |
| Remaining storage usage     | Storage free (%)                                                                                 |                                   |
| Storage IO         | Disk read (bytes)<br> Disk write (bytes)                                                         |                                   |
| Network data transfer       | nic incoming (bytes)<br> nic outgoing (bytes)                                                    | The basic network data transfer used by Redis occurs. |
| Storage defects        | Disk fault status                                                                                | Abnormal: 0, normal: 1                     |
| Redis memory usage      | Redis memory usage (bytes)                                                                            |                                   |
| Redis memory usage (rss) | Redis memory usage rss (bytes)                                                                       |                                   |
| Number of connected clients        | Number of connected clients (counts)                                                                             |                                   |
| Number of connected replicas           | Number of connected replicas (counts)                                                                                |                                   |
| Number of blocked clients        | Number of blocked clients (counts)                                                                             |                                   |
| Memory fragmentation rate         | Memory fragmentation rate (%)                                                                                   |                                   |
| Commands processed per second        | Commands processed per second (ops/1sec)                                                                           |                                   |
| Input bytes             | Input bytes (bytes)                                                                                   |                                   |
| Output bytes             | Output bytes (bytes)                                                                                   |                                   |
| Number of expired keys (expired)   | Number of expired keys (counts)                                                                                 |                                   |
| Number of keys deleted (evicted)   | Number of keys deleted (counts)                                                                                 |                                   |
| Successful lookups            | Successful lookups (counts)                                                                                 |                                   |
| Failed lookups            | Failed lookups (counts)                                                                                 |                                   |
| Lookup success rate             | Lookup success rate (%)                                                                                       |                                   |
| Number of keys               | Key counts (counts)                                                                                    |                                   |
| get execution count          | get execution count (counts)                                                                               |                                   |
| hget execution count         | Number of hget executions (counts)                                                                              |                                   |
| get usec/get calls | get usec/get calls (counts)                                                                      |                                   |
| set execution count          | set execution count (counts)                                                                               |                                   |
| hset execution count         | HSET execution count (counts)                                                                              |                                   |
| set usec/get calls | set usec/get calls (counts)                                                                      |                                   |

## Server Group

Using server groups, you can view performance metrics for multiple nodes in a single chart. Performance metrics for each node in a server group are displayed in a single chart. Charts consisting of multiple performance metrics are all converted to individual performance metrics in a server group.

### Create a Server Group

![server-dashboard-group-add](https://static.toastoven.net/prod_rds_postgres/20240611/server-dashboard-group-add-ko.png)

❶ Click **+ Add Group** to open a pop-up where you can create a group.
❷ Select the nodes to add to the server group.

### Configure a Server Group

Nodes and server groups are displayed together in the server list on the left side of the server dashboard.

![server-dashboard-group-manage](https://static.toastoven.net/prod_rds_postgres/20240611/server-dashboard-group-manage-ko.png)

❶ Click **+** or - to expand or collapse a server group.
❷ Click a node in a server group to open a color selection pop-up where you can change the color displayed in the chart.

![server-dashboard-group-menu](https://static.toastoven.net/prod_rds_postgres/20240611/server-dashboard-group-menu-ko.png)

❶ Click Learn More icon displayed on the right side of each item in the server list to modify or delete a server group.