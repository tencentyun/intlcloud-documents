This document describes how to create a CM dashboard to view monitoring data.

## Directions
1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/dashboard2/dashboards).
2. On the left sidebar, select **Dashboard** > **Dashboard List**.
3. Below the dashboard list, click **Create Dashboard**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/su85086_1.png)
4. In the pop-up window, select **Create Chart**, or select **Create Chart Group** and then click **Create Chart** in the created chart group.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dBzd029_2.png)
5. On the chart editing page, configure the following parameters and click **Save** in the top-right corner.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Select Product</td><td>Select **Tencent Cloud services**.</td></tr>
<tr>
<td>Metric</td><td>Select **TencentDB** > **TDSQL-C** > **MySQL** and select the target monitoring metric.</td></tr>
<tr>
<td>Filter</td>
<td>Select a filter to extract the data that meets the conditions for display on the chart. You can add multiple filters, and the chart displays only the data meeting all of them. Data can be filtered by instance, tag, and template variable.</td></tr>
<tr>
<td>Group by</td><td>Select a tag to aggregate and display data by group (optional).</td></tr>
<tr>
<td>Comparison</td><td>You can select day-over-day (compared with the same period yesterday), week-over-week (compared with the same period last week), and custom dates for comparison.</td></tr>
<tr>
<td>Alias</td><td>Enter the legend alias.</td></tr>
<tr>
<td>Enable Sorting</td><td>After it is enabled, you can set a sorting rule.</td></tr>
<tr>
<td>Sorting Rule</td>
<td>You can select the maximum, minimum, average, or sum value and specify whether to display items in ascending or descending order.</td></tr>
<tr>
<td>Displayed Quantity</td><td>Set the number of instances to be displayed.</td></tr>
</tbody></table>
6. After the configuration is saved successfully, you can view the monitoring data of the metric selected during chart creation.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9eCP141_3.png)
>?This method is used to create a chart for a single monitoring metric. To create charts for multiple metrics, simply repeat the above steps.

