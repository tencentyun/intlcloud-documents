The slow query log is used to record query statements that take more time than the specified value to execute in SQL Server. You can find out inefficient query statements to optimize by slow query log. In short, the SQL Server slow query log is an important feature for troubleshooting SQL statements and checking the current performance of SQL Server.
This document describes how to query and download slow query logs.

## Notes on slow queries in SQL Server
The collection threshold of slow query is 1 second, and SQL executions exceeding 1 second will be recorded as a slow query log.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://qcloudimg.tencent-cloud.cn/raw/c98cd605b59406bf95f53a58c35d6509.png)
3. On the instance management page, select the **Slow Log** tab to see slow log list.
 - You can view the following fields: **File Name**, **Start Time of File Generation**, **End Time of File Generation**, **File Size**, and **Operation** (**Download**).
 - You can search for slow logs generated in the last 5/15/30 minutes, last 1/3/24 hours, today, last 3 days, or a custom time range.
![](https://qcloudimg.tencent-cloud.cn/raw/4ce15827444cca9421dd87f0093204dd.png)
4. Click **Download** in the **Operation** column to download slow query log files.
