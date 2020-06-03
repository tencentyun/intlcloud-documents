Using the capacity analysis feature of DBbrain, you can view the instance capacity utilization, including the sizes of data and log capacities, the daily increase in capacity utilization, the estimated number of available days, and the capacity used by tablespaces under the instance.

>Currently, capacity analysis is supported only for TencentDB for MySQL (excluding the Basic Edition).

## Disk Capacity
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/slow-sql), select **Diagnosis and Optimization** on the left sidebar, and select **Space Analysis** at the top.
On the capacity analysis page, you can view the comparison of daily increases in the last week, the available disk capacity, the estimated number of available days, and the trend in disk capacity usage in the last week.
![](https://main.qcloudimg.com/raw/ecd64ab4f412169e7a2fe6478ec18f04.png)

## Top Tablespaces
The **Top Tablespaces** section displays the details of your tables that have relatively high capacity usage, including the storage engine, number of rows, total used capacity, data capacity, index capacity, fragment capacity, and fragment percentage. Each column of data can be sorted in ascending or descending order. You can view the disk capacity usage details in this section and perform optimization promptly.
![](https://main.qcloudimg.com/raw/cb0705e2cc6b84bdc0962ff06f5f71e9.png)
