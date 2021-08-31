## Overview
An SQL statement query that takes more time than the specified value is referred to as a "slow query", and the corresponding statement is called a "slow query statement". The process where a database administrator (DBA) analyzes slow query statements and finds out the reasons why slow queries occur is known as slow log analysis.

You can log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql), click an instance ID/name in the instance list to access the instance management page, and select the **Performance Optimization**tab to perform slow log analysis, as shown below:
![](https://main.qcloudimg.com/raw/5837567fd0b5a75c1a682e7dfa80dc70.png)

## Main Parameters

### Default settings of slow log analysis
- **Slow log feature**: enabled by default.
- **log_min_duration_statement**: slow query statements that have been executed for more than `log_min_duration_statement` seconds will be logged. Default value: `1`.
- **Analyzed data output delay**: 1–5 minutes.
- **Log retention period**: 7 days (up to the last 10,000 records).

### Descriptions of analysis result list fields
On the **Slow Log Analysis** tab, the analysis result list has the following fields.

#### Basic information
- **Last Execution Time**: the time when the abstract statement was executed for the last time within the specified time range. As some statements may be executed for a long time, we log the `begin_time` of the statement execution.
- **Abstracted SQL Statement**: a slow query statement whose constants are removed. The abstracted statement can be used for summary statistics of similar statements to facilitate your analysis.
- **Database**: the database called by the statement
- **Account**: the account used by the statement
- **First Execution Time**: the time when the slow query statement was executed for the first time within the specified time range. There may be many records after abstraction.
- **Total**: the number of executions of the slow query statement within the specified time range
- **Total Executions (%)**: the ratio of the total executions of the slow query statement to the total executions of all slow query statements within the specified time range
- **Sent Rows**: the total number of result rows sent (returned) from database server to client within the specified time range

#### Statistics of query information
- **Total Time (sec)**: the total time consumed by the slow query statement within the specified time range
- **Total Time (%)**: the ratio in percentage of the total time consumed by the slow query statement to the total time consumed by all slow query statements within the specified time range
- **Avg. Time (sec)**: the average time is calculated by dividing the total time consumed by the slow query statement by the total number of executions of the slow query statement.
- **Min. Time (sec)**: the minimum among all execution time of the slow query statement. This parameter is used to determine whether the statement is sporadic.
- **Max. Time (sec)**: the maximum among all execution time of the slow query statement. This parameter is used to determine whether the statement is sporadic.

#### Statistics of reads and writes
- **Blocks Read from Shared Memory**: the blocks read by the slow query statement from the shared memory within the specified time range
- **Blocks Written to Shared Memory**: the blocks written by the slow query statement to the shared memory within the specified time range


#### Statistics of read/write I/O response time
- **Read I/O Response Time**: the total time consumed by the slow query statement to perform read I/O operations within the specified time range. This parameter is used to determine whether the statement performs time-consuming operations such as full scans.
- **Write I/O Response Time**: the total time consumed by the slow query statement to perform write I/O operations within the specified time range. This parameter is used to determine whether the statement writes large amounts of (temporary) data at once.

