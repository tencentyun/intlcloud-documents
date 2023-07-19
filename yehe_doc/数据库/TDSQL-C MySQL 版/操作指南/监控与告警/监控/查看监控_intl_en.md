TDSQL-C for MySQL provides a rich set of performance monitoring metrics to help you stay up to date with the detailed status and performance of your database. Generally, you can view monitoring metrics and data in the TDSQL-C for MySQL console by creating a dashboard in Tencent Cloud Observability Platform (TCOP) or through TencentCloud API. We recommend that you choose the console, where you can quickly obtain fine-grained monitoring data for the target time range and locate Ops problems accordingly.

This document describes how to view the monitoring data and perform visual operations on the monitoring page.

## Viewing Monitoring Data

| Option | Strengths | Operation |
|---------|---------|---------|
| Viewing data in the TDSQL-C for MySQL console | The console is simple and visual, where you can quickly locate problems in a familiar way. | [Viewing Monitoring Data in the Console](https://www.tencentcloud.com/document/product/1098/50191) |
| Creating a TCOP dashboard to view data | You can visually create customized monitoring metric groups. | [Creating Dashboard to View Monitoring Data](https://www.tencentcloud.com/document/product/1098/50190) |
| Pulling data through TencentCloud API  | You can flexibly pull monitoring metric data to analyze and process it or connect it to other platforms. | [Pulling Monitoring Data Through TencentCloud API](https://www.tencentcloud.com/document/product/1098/50189) |

## Visual Operations on the Monitoring Page
### Selecting the standard monitoring view
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select **Monitoring and Alarms**, select one or multiple target instances in the drop-down list below the time picker, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/eHYk120_5.png)
4. On the **Monitoring and Alarms** tab, click ![](https://qcloudimg.tencent-cloud.cn/raw/a1567f0e8bda741fb886c32c55ec63d3.png) to switch the layout of the monitoring view.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Qwga114_7.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wADs994_8.png)

### Displaying a chart in full screen
You can display a single metric in full screen for a clearer preview of metric data.
1. On the **Monitoring and Alarms** tab, click ![](https://qcloudimg.tencent-cloud.cn/raw/5ad2d8ff9f3dfcf99cc82d10f0c718ae.png) on the right of the corresponding metric to display the metric in full screen.
2. After the data is displayed in full screen, you can filter the metric and select a time range and time granularity to view the metric data. You can click **X** in the top-right corner to close the full screen window.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/GYjK944_10.png)

### Selecting a monitoring time range
You can select or customize a time range to query the monitoring data over this time period.
On the **Monitoring and Alarms** tab, you can select **Last hour**, **Last 24 hours**, **Last 7 days**, or **Last 30 days**. You can also click the time picker to specify the start time and end time for monitoring data query.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ts5n101_11.png)

### Adding period-over-period comparison
You can compare monitoring data from multiple time ranges by adding period-over-period comparison.
>?The time range in the first time picker determines the time ranges in new time pickers. For example, if it is 3 days in the first time picker, then you can select only the start time in a new time picker, and the end time will be 3 days later by default.

**Use limits**
- If you select multiple instances to view monitoring data, the period-over-period comparison feature is not supported.
- You can compare the data of an instance monitoring metric within up to three time ranges.

**Directions**
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select the **Monitoring and Alarms** tab.
4. Select the target instance below the time picker on the right and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Js6j249_12.png)
5. Click **Period-over-Period Comparison** on the right of the time picker.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/eDaC391_13.png)
6. Select the time range for query in the first time picker and click **OK**. Then, select the start time of the second time range in the second time picker and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WT9y089_14.png)
>?In new time pickers, you only need to select the start time, and the time range will be automatically aligned with that in the first time picker. For example, if the time range in the first time picker is 3 days, then all time ranges added subsequently will also be 3 days.
7. After you select the time ranges for comparison, you can query the monitoring metric details of the instance within the selected time ranges at the specified time granularity.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/7TM5340_15.png)

### Setting a monitoring time granularity
You can select different time granularities for monitoring data query within the specified time range.
On the **Monitoring and Alarms** tab, select a time range and select a time granularity in the **Time Granularity** drop-down list.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/j8yh684_16.png)
**Time ranges and corresponding time granularities**

| Query time range | Range between query start time and current time | Default time granularity | Optional time granularities |
|-------|-------|--------|----|
| (0h, 1h] | (0d, 1d] | 5s | 5s/1min/5min | 
| (0h, 1h] | (1d, 15d]| 1min | 1min/5min | 
| (0h, 1h] |  (15d, 31d]| 5min | 5min |
| (1h, 24h] |(0d, 15d] | 1min | 1min/5min/1h |
| (1h, 24h] |  (15d, 31d]| 5min | 5min/1h |
| (24h, 7d] |  (0d, 31d]| 5min | 5min/1h/1d |
| (7d, 31d] |  (0d, 31d]| 1h | 1h/1d | 

**Example:**
Suppose the current time is 15:00, July 10, 2022, and the query time range is 15:00–16:00, June 29, 2022 (1 hour), then the query time range is 1 hour. As the time between the query start time and the current time is longer than 1 day but shorter than 15 days, the default time granularity is 1 minute. You can also select the option of 5 minutes.

>?Currently, you can view monitoring data of TDSQL-C for MySQL in the past 31 days.

