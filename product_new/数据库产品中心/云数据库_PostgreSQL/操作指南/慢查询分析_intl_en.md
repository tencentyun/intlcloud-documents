## Feature Description
An SQL statement query that takes more time than the specified value is referred to as a "slow log", and the corresponding statement is called a "slow log statement". The process where a database administrator (DBA) analyzes slow log statements and finds out the reasons why slow logs occur is known as "slow log analysis".

You can log in to the [TencentDB for PostgreSQL Console](https://console.cloud.tencent.com/pgsql) and go to the **Performance Optimization** module on the instance management page to perform slow query analysis.

## Descriptions of Main Parameters

### Default settings of slow log analysis
- **Slow log feature**: enabled by default.
- **Slow SQL log time (log_min_duration_statement)**: 1 second by default, that is, only slow log statements that exceed 1 second will be logged. If you need to adjust the time, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) with the instance ID and the desired time value.
- **Analyzed data output latency**: 1–5 minutes.
- **Log retention period**: 7 days (up to the last 10,000 records)

### Descriptions of analysis list fields
Currently, the slow log analysis feature provides the following information of slow SQL statements:

#### Basic information
- **Last execution time**: the time when the abstract statement appeared for the last time within the specified time range. As some statements may be executed for a long time, all statements are logged by the `begin_time` of statement execution.
- **Abstracted SQL statement**: the statement after constants are removed from the slow SQL. The abstracted statement can be used for aggregated statistics of similar statements to facilitate your analysis.
- **Database**: the database called by the statement.
- **Account**: the account used by the statement.
- **First execution time**: the time when the slow SQL statement appeared for the first time within the specified time range (there may be many records after abstraction and aggregation).
- **Total occurrences**: how many times in total the slow SQL statement appeared within the specified time range.
- **Occurrence percentage**: occurrence percentage of a slow log statement out of all slow log statements within the specified time range.
- **Number of rows sent**: total number of data rows sent (returned) to the client by the database server within the specified time range.

#### Query statistics
- **Total time**: total time of a slow log statement within the specified time range.
- **Total time percentage:** time percentage of a slow log statement out of all slow log statements within the specified time range.
-**Average time**: average time calculated by dividing the total time of a slow log statement by total number of occurrences.
- **Minimum time**: minimum occurrence time of a slow SQL in the abstracted statement, which is used to determine whether the statement is sporadic.
- **Maximum time**: maximum occurrence time of a slow SQL in the abstracted statement, which is used to determine whether the statement is sporadic.

#### Data read/write statistics
- **Blocks of shared memory read**: how much data in the shared memory is read by the slow SQL statement within the specified time range.
- **Blocks of shared memory written**: how much data is written to the shared memory by the slow SQL within the specified time range.


#### IO read/write time statistics
- **Total IO read time**: total time of IO reads by the slow SQL statement within the specified time range, which is used to help determine whether the statement performed time-consuming operations such as full scan.
- **Total IO write time**: total time of IO writes by the slow SQL within the specified time range, which is used to help determine whether the statement writes large amounts of (temporary) data at a time.

