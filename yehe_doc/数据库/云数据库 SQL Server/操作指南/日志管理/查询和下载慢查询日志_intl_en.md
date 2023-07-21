The slow query log records the query statements that take more time than the specified value to execute in TencentDB for SQL Server, through which you can find out inefficient query statements for optimization. The TencentDB for SQL Server slow query log is a SQL statement for troubleshooting and an important feature for checking the performance of the current TencentDB for SQL Server instance.
This document describes how to query and download a slow query log in the console.

## Notes on slow queries in TencentDB for SQL Server
- The collection of slow query is enabled by default and cannot be disabled.
- The collection threshold of slow query is 1 second (1,000 ms) by default, and SQL executions exceeding 1 second will be recorded as a slow query log.
- The slow query log will be collected every 5 minutes by default, and SQL statements exceeding 1 second will be recorded.
- The slow query logs are retained for 7 days by default and will be automatically deleted upon expiration.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TaUU102_34.png)
3. On the instance management page, select the **Operation Log** > **Slow Query Log** to view the list of the slow query logs.
 - You can view the following fields: **File Name**, **Start Time of File Generation**, **End Time of File Generation**, **File Size**, and **Operation** (**Download**).
 - You can search for slow logs generated in the last 5/15/30 minutes, last 1/3/24 hours, today, yesterday, last 3 days, last 7 days, last 30 days or a custom time range.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rA8t034_35.png)
4. Click **Download** in the **Operation** column to download slow query log files.
