## Overview
The **Service status** page provides detailed monitoring for main services installed in the cluster, including HDFS, YARN, Hive, ZooKeeper, Spark, HBase, and Presto. This document describes how to view cluster service status in the console.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list.
2. On the cluster details page, select **Cluster services** and click **Operation** > **Service status** in the top-right corner of the target component block. The following uses HDFS as an example.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/aQix759_%E5%9B%BD%E9%99%8526.png)
3. The service status page provides monitoring views of three service dimensions, namely, service summary, health status, and service overview. As different service components have different services, the dimensions of display vary.
4. **Service overview** displays 6 metrics of service components by default and their statistical rules during a specified time period. You can click **Set metrics** to customize the displayed metrics.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/69h2639_%E5%9B%BD%E9%99%8527%E5%92%8C31.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/pdsL052_%E5%9B%BD%E9%99%8528.png)
5. **Service summary** displays the current overall status of the service.
6. **Health status** displays running overview of each component in the current service. Clicking a role name or running overview will redirect you to **Roles** or **Role status** page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/JUTg277_%E5%9B%BD%E9%99%8529.png)
On a role status page, you can click **Set metrics** to customize the displayed metrics.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/xBxE167_%E5%9B%BD%E9%99%8530.png)
7. **Service overview** enables you to view cluster-level metrics. You can click **Set metrics** to customize the displayed metrics.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/69h2639_%E5%9B%BD%E9%99%8527%E5%92%8C31.png)
>!
>- **Service monitoring** displays the HDFS service information by default. You can manually adjust to view other service components.
>- Service monitoring dimensions vary by service component due to different service types. For example, HBase supports table-level monitoring.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Wr8h385_%E5%9B%BD%E9%99%8532.png)
