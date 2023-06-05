## Overview
Table analysis provides information such as the numbers of read/write requests and storage information for an entire HBase table, each individual region within the table, and each region server. The feature also supports analyzing the read/write queries per second (QPS) and their trends for the corresponding table or region server in practical scenarios.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the corresponding cluster in the cluster list.
2. On the cluster details page, click **Cluster Service** and choose **Operation** > **Table analysis** in the top-right corner of the HBase component block to query HBase table loads.

## Supported Operations in the Table List
In the HBase table list, you can view information about the read QPS, write QPS, MetaStore storage, and StoreFile size for each table. You can also identify the top tables in the cluster by using the sorting button in each column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8eaP605_%E5%9B%BD%E9%99%851.png)

### Viewing table details
Click a table name to obtain a detailed view of the table. The details page displays the numbers of read/write requests, MemStore storage, and storeFile size for the entire table or each individual node. You can switch between nodes by using the node filter in the top-right corner.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/DvIx551_%E5%9B%BD%E9%99%852.png)

### Viewing the overall region information
Click **Regions** to view the overall region information, including the number of read/write requests for each region in the table, which helps you identify hot spot regions.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/IRTT895_%E5%9B%BD%E9%99%853.png)

### Viewing region details
Click a region name to obtain the detailed view of the region. The details page displays the numbers of read/write requests for the table at different time granularities. Select an option from **Time granularity** in the top-right corner to switch between different time granularities.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WiUR800_%E5%9B%BD%E9%99%854.png)

### Viewing the overall region server information
Click **RegionServers** to view the request latencies of each region server that hosts one or more regions in the table.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mv8U638_%E5%9B%BD%E9%99%85%E7%AB%995.png)

## Region Analysis
With region analysis, you can search for the table that a specific region belongs to or filter results by the region server that hosts the region. By examining the average request QPS and average read/write QPS, you can identify hot spots in the cluster where a large number of requests are being processed.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5dI2042_%E5%9B%BD%E9%99%856.png)
By clicking the view button in the "Average read QPS" or "Average write QPS" column header, you can view the trend of read/write QPS for the current region and observe sudden changes in request traffic. You can specify the time range for the information displayed.
