## Feature Description
Service status provides detailed monitoring for main services installed in the cluster, including HDFS, Yarn, Hive, ZooKeeper, Spark, HBase, and Presto. This document describes how to view cluster service status in the console.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Service** and click **Operation** > **Service Status** in the top-right corner of the target component block. The following uses HDFS as an example.
![](https://main.qcloudimg.com/raw/02eb6360afd2e6515724a4496ff6e708.png)
3. The service status page provides monitoring views of three service dimensions, namely, service summary, health status, and service overview. As different service components have different services, the dimensions of display vary.
4. **Service Overview** displays six metrics of service components by default and their statistical rules during a specified time period. You can click **Set Metric** to customize the displayed metrics.
![](https://main.qcloudimg.com/raw/12c9e198bd534098a84e6b89ce9f1df8.png)
![](https://main.qcloudimg.com/raw/8955aa65869661cd2422b0195290844f.png)
5. **Service Summary** displays the current overall status of the service.
6. **Role List** displays the service deployment status of each role of the current service component. You can click a **node IP** to view the monitoring metrics and their statistical rules of the current node. Six metrics are displayed by default.
![](https://main.qcloudimg.com/raw/5502b61780676857e2a9a2ce941aa80f.png)
7. 	After entering a node page, you can click **Set Metric** to customize the displayed metrics.
>!
>- **Service Monitoring** displays the HDFS service component by default. You can manually adjust to view other service components.
>- Service monitoring dimensions vary by service component due to different service types. For example, HBase supports table-level monitoring.

![](https://main.qcloudimg.com/raw/274f47e0f4d7f36d7b7f18a3c6940a9e.png)
