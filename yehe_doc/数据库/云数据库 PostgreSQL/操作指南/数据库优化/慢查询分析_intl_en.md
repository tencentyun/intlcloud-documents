## Feature Description
By default, an SQL query that takes more than one second is a slow query, and the corresponding statement is a slow query statement. The process where a database administrator (DBA) analyzes slow query statements and finds out the reasons why slow queries occur is known as slow query analysis.

You can log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql), click an instance ID in the instance list to access the instance management page, and select the **Performance Optimization** tab to analyze slow queries, as shown below:
![](https://main.qcloudimg.com/raw/5837567fd0b5a75c1a682e7dfa80dc70.png)

## Monitoring Views
There are two monitoring views in the console, visually and conveniently illustrating the monitoring data of database slow queries.
**Combined View (Slow Log and Other Metrics)**: this view shows and compares the monitoring data of the slow query metric and another metric in the same chart. Supported metrics include CPU utilization, QPS, requests, read requests, write requests, other requests, buffer cache hit rate, and average execution latency.
**Slow SQL Execution Time Distribution**: this view shows in what time period slow queries mainly occur.

## Slow SQL List
The slow SQL list shows slow query statements of the database in real time. The list is arranged in descending order by time, that is, the latest slow query statement is automatically displayed in the first row.
The slow SQL list has the following fields: the execution time, the slow SQL statement, the total time, the client IP, the database name, and the account executing the statement.

>! By default, the slow SQL list displays slow SQL data over the past seven days. The slow SQL data is stored in a log, and the oldest data is automatically deleted from the log to ensure that the log only stores data within the past seven days and the log size does not exceed 50 GiB.

## Slow SQL Statistics and Analysis
The slow SQL statistics and analysis page shows the slow query statements with abstract parameter values within the specified time range and their aggregated statistical analysis results. The page has the following fields:
- **Last Execution Time**: the time when the abstract statement is executed for the last time within the specified time range. As some statements may take a long time to execute, the `begin_time` of statement execution is logged as the last execution time.
- **Abstract SQL Statement**: a slow query statement whose constants are removed. The abstract statement can be used for summary statistics of similar statements to facilitate your analysis.
- **Database**: the database queried by the statement.
- **Account**: the account executing the statement.
- **Client IP**: the clients executing the statement.
- **First Execution Time**: the time when the abstract slow query statement is executed for the first time within the specified time range (there may be many records after abstraction).
- **Total Execution Time**: the total time consumed by the abstract slow query statement within the specified time range.
- **Avg Execution Time**: the average time is calculated by dividing the total time consumed by the abstract slow query statement by the total number of its executions.
- **Min Execution Time**: the minimum among all execution time of the abstract slow query statement. This parameter is used to determine whether the statement is sporadic.
- **Max Execution Time**: the maximum among all execution time of the abstract slow query statement. This parameter is used to determine whether the statement is sporadic.
- **Total Time (%)**: the ratio in percentage of the total time consumed by the abstract slow query statement to the total time consumed by all abstract slow query statements within the specified time range.

