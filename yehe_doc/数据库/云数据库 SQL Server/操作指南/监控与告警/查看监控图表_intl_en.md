
To make it easier for you to view and stay up to date with how instances work, TencentDB for SQL Server provides a wide variety of performance monitoring metrics and convenient monitoring features (custom view, time comparison, merged monitoring metrics, etc.).

This document describes how to view monitoring chart info in the console.
>?If the number of tables in a single instance exceeds one million, database monitoring may be affected. Make sure that the number of tables in a single instance is below one million.

## Types of instances for monitoring
TencentDB for SQL Server primary and read-only instances can be monitored, and each instance is provided with a separate monitoring view for easy query.

## [Viewing monitoring data](id:ckjkxx)
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://qcloudimg.tencent-cloud.cn/raw/273f3f073d2dd195dae0926ab52dd708.png)
3. On the instance management page, select the **System monitoring** page to view monitoring metrics.
![](https://qcloudimg.tencent-cloud.cn/raw/72fe5eadb03993db12e0a8b6a45eca43.png)
>?On the instance list, you can also click the monitoring icon of the target instance to quickly view its monitoring status.
>![](https://qcloudimg.tencent-cloud.cn/raw/f23fd5341d823616580cf13619e381ee.png)

## Displaying a chart in full screen
You can display a single metric in full screen for a clearer preview of metric data.
1. On the [System Monitoring](#ckjkxx) page, you can click icon ![](https://qcloudimg.tencent-cloud.cn/raw/5ad2d8ff9f3dfcf99cc82d10f0c718ae.png) on the right of the corresponding metric to display the metric in full screen.
2. After the preview data is displayed in full screen, you can click the X in the upper right corner to close the full screen display window.
![](https://qcloudimg.tencent-cloud.cn/raw/67c8af1dce72f488fb5d7f542dc2cf32.png)

## Exporting data
You can export the desired metric data individually.
On the [System Monitoring](#ckjkxx) page, you can click icon ![](https://qcloudimg.tencent-cloud.cn/raw/96ac56f01426b5d7af37b10f181bf85a.png) on the right of the corresponding metric to export data or pictures of the metric to the local system.
![](https://qcloudimg.tencent-cloud.cn/raw/998d0541294395dd8d7dad5fe517d9e9.png)

## Selecting monitoring time range
You can select or customize a time range to query the monitoring over this time period.
1. On [System Monitoring] page, click the time box.
![](https://qcloudimg.tencent-cloud.cn/raw/0179ccba669135a7b2f3e79d904bd862.png)
2. In the pop-up window, you can select 5 minutes, 30 minutes, 1 hour, 3 hours, 12 hours, 24 hours, 2 days, 7 days, 30 days, today, yesterday, the start and end date, or the time range of them, then click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/ace670b8815b5dfc66d8edb0c01bc54f.png)

## Adding time comparison
You can compare monitoring data from multiple time ranges by adding time comparisons.
1. On [System Monitoring] page, click **Add Time** icon behind time box.
![](https://qcloudimg.tencent-cloud.cn/raw/46d924db19663714642e4e0a751bf002.png)
2. Select **Week-over-Week (Last Week)**, **Day-over-Day (Yesterday)**, or **Custom Date** from the drop-down list, and click **Ok**.
![](https://qcloudimg.tencent-cloud.cn/raw/25a57c04d50e2de1b210acaa31ddb981.png)

## Monitoring granularity
You can view instance monitoring at different time granularities within the selected time period.
On [System Monitoring] page, select the time period, and then you can select the desired time granularity in the drop-down list after **Time Granularity** to view the monitoring data.
![](https://qcloudimg.tencent-cloud.cn/raw/7ca17555648846fea1da31495d4e3989.png)

**Time Periods and Corresponding Chart Granularities**

| Time period | Time granularity |
|---------|---------|
| 5 minutes | 10 seconds, 1 minute |
| 30 minutes, 1 hour | 10 seconds, 1 minute, 5 minutes |
| 3 hours | 10 seconds, 1 minute, 5 minutes, 1 hour |
| 12 hours, today, yesterday | 1 minute, 5 minutes, 1 hour |
| 24 hours, 2 days | 1 minute, 5 minutes, 1 hour, 24 hours |
| 7 days, 30 days | 1 hour, 24 hours |

## Setting refresh time
You can set the refresh time on the system monitoring page (disabled by default) to observe changes of instance monitoring in real time.
On the [System Monitoring](#ckjkxx) page, click the drop-down button after ![](https://qcloudimg.tencent-cloud.cn/raw/21e447500165860dd294edff8c529116.png) to set time frequency of data refresh (30 seconds, 5 minutes, 30 minutes, and 1 hour are supported).
![](https://qcloudimg.tencent-cloud.cn/raw/2e5264740adae3d7b5a9b8d2db8473e9.png)
