The full instance monitoring page gives you an overview of the database monitoring metrics of all instances. The unified monitoring view displays the horizontal view of single monitoring metrics of all instances, allowing you to view and detect database exceptions and providing you with a new macro view on monitoring information.

>?Currently, full instance monitoring is supported only for TencentDB for MySQL (excluding basic single-node instances), TDSQL-C for MySQL, self-built MySQL, TencentDB for Redis, and TencentDB for MongoDB.

![](https://main.qcloudimg.com/raw/87cc8bd8578ee13e2fd25347544cbf72.png)

## Switching the region
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Monitoring and Alarming** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database at the top and select the **Full Instance Monitoring** tab.
2. The full instance monitoring page displays the database instances in all regions by default. You can filter instances by region in the drop-down list at the top.

## Switching the monitoring metric
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Monitoring and Alarming** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database at the top and select the **Full Instance Monitoring** tab.
2. You can filter and select a metric in the drop-down list at the top. All monitoring metrics of TencentDB for MySQL and TDSQL-C as well as the monitoring metrics of your self-built database are supported. The information of the selected monitoring metric is displayed and sorted by metric value on this tab.
![](https://main.qcloudimg.com/raw/ae4d123c71de10593fea06231a28317c.png)

## Viewing the real-time/historical monitoring data
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Monitoring and Alarming** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database at the top and select the **Full Instance Monitoring** tab.
2. You can view real-time and historical monitoring information on the full instance monitoring page. In historical monitoring information, the maximum value and its occurrence time of the selected metric in the specified time period will be displayed.

## Searching for an instance
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Monitoring and Alarming** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database at the top and select the **Full Instance Monitoring** tab.
2. On this tab, you can search instances. If you select TencentDB for MySQL, fuzzy search by instance ID/name or private IP is supported; if you select TDSQL-C, fuzzy search by cluster ID/name, instance ID/name, or access point address is supported; if you select self-built MySQL database, fuzzy search by instance ID, instance name, or IP address is supported.
>?Click the **i** icon on the right in the search box to view the help document for instance search.
>
![](https://main.qcloudimg.com/raw/31d45e4fd2f0df9f2e67677784438e80.png)

## Switching the grid view
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Monitoring and Alarming** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database at the top and select the **Full Instance Monitoring** tab.
2. You can switch between 9-grid view and 36-grid view. We recommend you use the **36-grid view** if the number of instances is high, as it provides a broader view and you can see the fluctuations of monitoring metrics more clearly.
![](https://main.qcloudimg.com/raw/3eb6194a721b2d7a66f7f6ed4b70fbb1.png)
Click the **Unfold** icon in the top-right corner of the block of an instance to view its information and metric trend details.
![](https://main.qcloudimg.com/raw/236209268a17b8dea994749521469e88.png)
