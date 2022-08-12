## Feature description

With DBbrain's space analysis feature, you can view the instance space utilization, including the sizes of data and logs, the daily increase in space utilization, the estimated number of available days, and the space used by the tables and databases of the instance.

## Overview
![](https://qcloudimg.tencent-cloud.cn/raw/4872ab79304d80847883d30b6c7e430a.png)

## Directions

1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Space Analysis** tab.
2. Check the disk space.
   In the upper part of the **Space Analysis** tab, you can view the daily average growth in the past week, remaining disk space, estimated available days, daily distribution of disk usage, and disk space trend in the last 30 days.
   For TencentDB for MongoDB, the remaining disk space = purchased disk space - data space.
3. View top tables.
   The **Top Tables** section shows the details of the tables that have relatively high space usage. The table list in the section contains columns such as the **Collection Name**, **Collection Space**, **Physical File Size**, **Index Space**, **Data Space**, **Compression Ratio**, **Avg Data Size**, and **Rows in Collection**. The tables can be sorted by specified field in descending order. You can view the disk space usage details in this section and perform optimization promptly.
   ![](https://qcloudimg.tencent-cloud.cn/raw/f10ff1c97bd551c2b4c216b3f4332f8d.png)
   Select a table to further view its **Trend** and **Table Info** on the **Space Analysis** tab.
   - The **Trend** section displays the trends of the **Collection Space**, **Index Space**, and **Data Space** as well as the statistics of the **Physical File Size** and **Rows in Collection**.
     ![](https://qcloudimg.tencent-cloud.cn/raw/ae6809d5af13cd54257e0c01fd90f5c3.png)
   - The **Table Info** section allows you to locate an index and its details. This makes it easy for you to quickly locate data with a high space usage.
4. View top databases.
   The **Top Databases** section shows the details of the databases that have relatively high space usage. The database list in the section contains columns such as the **Physical File Size**, **Index Space**, **Data Space**, **Avg Data Size**, and **Rows in Collection**. The databases can be sorted by specified field in descending order. You can view the disk space usage details in this section and perform optimization promptly.
   ![](https://qcloudimg.tencent-cloud.cn/raw/dc44a53cf2a7e1cc7a203eb6fd770374.png)
   Select a database to view its statistical trends.
   <img src="https://qcloudimg.tencent-cloud.cn/raw/50f056761d5ce3d35a4596e60f563155.png" style="zoom:50%;" />
5. View the table retrieval.
   Enter a database name and a collection name to view their space statistics.
6. Download the space analysis data.
   On the **Top Tables** and **Top Databases** tabs, click the download icon in the top-right corner to download the data in CSV format.
   
