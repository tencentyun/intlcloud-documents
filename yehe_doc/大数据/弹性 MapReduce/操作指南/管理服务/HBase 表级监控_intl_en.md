## Description
HBase table-level monitoring enables you to monitor the numbers of read and write requests and storage usage of each table in HBase.
## HBase Table Load List
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click a **Cluster ID/Name** on the **Cluster List** page to enter the cluster details page.
2. On the cluster details page, click **Cluster Service** and select **Operation** > **Table-Level Monitoring** in the top-right corner of the HBase component block to query HBase table loads.
![](https://qcloudimg.tencent-cloud.cn/raw/6d062e13f9b62dc8998ae662b09f8704.png)

## Viewing Table Details
Click a table name to pop up the table details. The details page can display the numbers of read and write requests and size of store (including MemStore and StoreFile) of the selected table in the dimension of the entire table or node. You can switch between nodes by using the **Node Filter** in the top-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/3f5f82ba954706c21398bce89ee01b85.png)

## Regions Operation
Click **Regions Operation** to view the numbers of read and write requests of each region contained in the table.
![](https://qcloudimg.tencent-cloud.cn/raw/2d4a3f7e2eb22d5d7e38dd17e312e9c4.png)

## Region Details
Click a region name to pop up the region details page, where the numbers of read and write requests of the selected table are displayed at different time granularities. Click **Time Granularity** in the top-right corner to switch between time granularities.
![](https://qcloudimg.tencent-cloud.cn/raw/7bd425872b04d87c303f228e58906bd1.png)

## RegionServers Operation
Click **RegionServers Operation** to view the request delay of each RegionServer where the table is distributed.
![](https://qcloudimg.tencent-cloud.cn/raw/c68cfd7ac497c8e3a9d96fd5ebf7f344.png)
