TencentDB for MongoDB allows you to view the change trend of each monitoring metric. This helps you stay up to date with the running status and performance of database resources, so that you can make prejudgments and prevent risks.

## Background
- CM is a real-time monitoring and alarming service for Tencent Cloud resources. It collects the data of various monitoring metrics of Tencent Cloud services and displays the data through visual charts, helping you intuitively understand the running status and performance of services. For more information, see [Product Overview](https://intl.cloud.tencent.com/document/product/248/32799).
- In TencentDB for MongoDB, you can use CM to create dashboards and various types of charts to compare the metric data of multiple instances. In this way, you can efficiently analyze the changes of monitoring metrics. You can also use CM to configure real-time alarms for exceptions during database operations, allowing you to remove risks as soon as they arise.

## Version Description
Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support instance monitoring.

## Billing Description
- Basic CM features such as alarming and monitoring data collection are free of charge.
- Currently, only **alarm SMS and phone calls** are billed.

## Notes
- The monitoring data is retained for 30 days.
- After receiving the alarms reported by Tencent Cloud, you need to troubleshoot problems accordingly.

## Prerequisites
- You have activated the CM service.
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).

## Directions
### Quickly viewing instance monitoring data
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Monitoring/Status** column of the target instance, click <img src="https://qcloudimg.tencent-cloud.cn/raw/e7563e7cc13faab92822ca56af11cf19.png" style="zoom:50%;" /> to open the instance monitoring panel, where you can quickly view the instance monitoring data. ![](https://qcloudimg.tencent-cloud.cn/raw/3160fb160516f421e06bb05ce82c6da6.png)
   - You can select **Real-Time**, **Last 24 Hours**, **Last 7 Days**, or any time period to view the corresponding monitoring data.
   - On the **Requests**, **Connections**, **Capacity and QPS**, and **Latency** tabs, you can view the data of monitoring metrics in different categories.
   - In the **Time Granularity** drop-down list, you can set the time granularity for monitoring data collection to get finer-grained data.
   - Select **Compare Monitoring Data of Instances** to enter the **Dashboard List** page in CM, [create a dashboard](https://intl.cloud.tencent.com/document/product/248/38468), select the instances to be monitored, set the [monitoring chart](https://intl.cloud.tencent.com/document/product/248/38477), and then you can compare the monitoring data of multiple instances in the same chart as shown below.
![](https://qcloudimg.tencent-cloud.cn/raw/3f30313c3f6182cb4ec99592d98ec41b.png)
   - Click **Configure Alarms** to enter the **Create Alarm Policy** page in CM, set **Policy Type** to **TencentDB for MongoDB Instance**, select an **alarm recipient**, set the **trigger condition** of the monitoring metric, and configure the alarm notification method. In this way, you can stay on top of the business exceptions and prevent risks and failures promptly. For detailed directions, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).

### Viewing monitoring details
1. In the [instance list](https://console.cloud.tencent.com/mongodb), find the target instance.
2. Click the target instance ID to enter the **Instance Details** page.
3. Click the **System Monitoring** tab to view the change trend of each monitoring metric of the entire cluster as shown below (with a replica set instance as an example):
![](https://qcloudimg.tencent-cloud.cn/raw/2ab708149259639ec41f02321a6cce7b.png)

### More operations
**Viewing monitoring data by monitoring object**
- Replica set: on the left of the instance monitoring page, select the specific instance name, primary node, and secondary node under the **Cluster Overview** to view the monitoring metric data of different monitoring objects.
- Sharded instance: on the left of the instance monitoring page, select the specific shard name, primary node, and secondary node under the **Cluster Overview** to view the monitoring metric data of different monitoring objects.

**Viewing monitoring data for specified time period**
In the top-right corner of the instance monitoring page, select **Real-Time**, **Last 24 Hours**, **Last 7 Days**, or any time period to view the corresponding monitoring data.

**Viewing monitoring data at different time granularities**
In the top-right corner of the instance monitoring page, select **5 seconds**, **1 minute**, **5 minutes**, or **1 day** in the drop-down list after **Time Granularity** to view the monitoring data at different time granularities.

**Zooming in change trend chart of single metric**
In the metric list on the right of the instance monitoring page, find the target metric and click <img src="https://qcloudimg.tencent-cloud.cn/raw/02851df41e781aa36044fc5b84d6c44e.png" style="zoom:45%;" /> to zoom in its change trend chart. You can select a time period and set a time granularity to analyze the metric change trend in a more refined manner.

**Exporting monitoring chart**
- Exporting one metric: in the metric list, select the target metric, click <img src="https://qcloudimg.tencent-cloud.cn/raw/d26c4e16aced2043172ab6a4f2529273.png" style="zoom:45%;" />, and select **Export as Image** to export its change trend chart. You can also select **Export Data** to view and analyze the monitoring data with Excel locally.
- Batch exporting monitoring data: click **Export Data** above the metric list, select the target metrics in the **Export Data** pop-up window, click **Export**, and then you can view and analyze the monitoring data with Excel locally.

**Setting alarm**
In the top-right corner of the instance monitoring page, click **Configure Alarms** to enter the **Create Alarm Policy** page in CM, set **Policy Type** to **TencentDB for MongoDB Instance**, select an **alarm recipient**, set the **trigger condition** of the monitoring metric, and configure the alarm notification method. In this way, you can stay on top of the metric exceptions and prevent risks and failures promptly. For detailed directions, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).

**Comparing data**
In the top-right corner of the instance monitoring page, click **Data Comparison** and set the start time for comparison as shown below. By default, the metric change trends for the previous minute and current minute are compared by default.
<img src="https://qcloudimg.tencent-cloud.cn/raw/acf38a2b41f51bfca33f401d39e796dc.png" style="zoom:80%;" />

