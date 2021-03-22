This document describes how to create an alarm monitoring chart to track the number of alarms triggered for Tencent Cloud products, custom cloud monitor, or Prometheus service.

## Directions
1. Log in to the Cloud Monitor console and go to the [**Default Dashboard**](https://console.cloud.tencent.com/monitor/dashboard2/default).
2. Select the target dashboard.
3. Click **<img src="https://main.qcloudimg.com/raw/827988040ba03fd73a5a95cc942eb5cd.png"  style="margin:0;" width="3%">** > **Create Chart** to go to the chart editing page, and configure the information as described below.
   - **Monitor Type**: select **Alarm Monitoring**
   - **Filter**: select **Cloud Product Monitoring**, **Custom Cloud Monitor**, or **Prometheus service**
     - Cloud Product Monitoring: if you select **Cloud Product Monitoring**, you need to specify the Tencent Cloud products you want to monitor. The system will track the number of alarms by product.
     - Custom Cloud Monitor: if you select **Custom Cloud Monitor**, you need to specify the namespaces you want to monitor. The system will track the number of alarms by namespace.
     - Prometheus service: if you select **Prometheus service**, the chart will display the number of alarms for all instances. Filter by instance is not supported currently.
 - **Group by**: is similar to the `Group by` statement in SQL. It groups Tencent Cloud products or namespaces and merges them by the method specified, as shown below.
 ![](https://main.qcloudimg.com/raw/241a82cfd3aa0a62557903b2aa640996.png)
 - **Merge by**: specifies the way multiple curves are merged into one. If `Group by` is not empty, curves in the same group will be merged into one.
 - **VS**: supports day-on-day (compare with the same period yesterday), week-on-week (compare with the same period last week), as well as custom time comparisons. If you select all of them, the chart will display the curves for the same period yesterday and last week so that you can compare them with the statistics of the day.
![](https://main.qcloudimg.com/raw/e7e73593a050749051b6072b7520349d.png)
4. After completing the above configuration, click **Save**.

>? To learn about different chart configurations, see [Use Cases of Different Chart Types](https://intl.cloud.tencent.com/document/product/248/38480).

