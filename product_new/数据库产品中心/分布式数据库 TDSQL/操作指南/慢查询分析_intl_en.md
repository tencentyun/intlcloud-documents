## Feature Description
An SQL statement query that takes more time than the specified value is referred to as a "slow log", and the corresponding statement is called a "slow log statement". The process where a database administrator (DBA) analyzes slow log statements and finds out the reasons why slow logs occur is known as "slow log analysis".

Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb), click an instance name in the instance list to enter the management page, and select the **Performance Optimization** tab where you can perform slow log analysis.
![](https://main.qcloudimg.com/raw/ea4506813533ff1905223dfd58b4bff3.png)
>Currently, slow log analysis can only be performed and viewed in each shard separately.

## Descriptions of Main Parameters
### Main Default Settings
-   Slow log feature: Enabled by default.
-   Slow log time (long_query_time): 1 second by default, that is, only slow log statements that exceed 1 second will be logged.
-   Analyzed data output latency: 1-5 minutes.
-   Logging duration: 30 days, depending on the backup and log settings.

### Descriptions of Analysis List Fields
-   Checksum (checksum): A sequence of digits used to identify a slow log statement (64-bit by default).
-   Abstracted slow log statement (fingerprint): Slow log statement with user data hidden.
-   Database: The database in which a slow log statement occurs.
-   Account: The account under which a slow log statement occurs.
-   Last execution time (last_seen): The time when a slow log statement last occurred within the time range.
-   First execution time (first_seen): The time when a slow log statement first occurred within the time range.
-   Total number of occurrences (ts_cnt): Number of occurrences of a slow log statement within the time range.
-   Occurrence percentage: Occurrence percentage of a slow log statement in relation to all slow log statements within the time range.
-   Total time (query_time_sum): Total time of a slow log statement within the time range.
-   Total time percentage: Total time percentage of a slow log statement within the time range.
-   Average time (query_time_avg): Average time calculated by dividing the total time of a slow log statement with total number of occurrences.
-   Minimum time (query_time_min): Minimum occurrence time of a slow log statement;
-   Maximum time (query_time_max): Maximum occurrence time of a slow log statement.
-   Total lock time (lock_time_sum): Total lock time of a slow log statement.
-   Total lock time percentage: Time percentage of a slow log statement in relation to total slow log statement lock time within the time range.
-   Average lock time (lock_time_avg): Average time calculated by dividing total slow log statement lock time with total number of locks.
-   Minimum lock time (lock_time_min): Minimum slow log statement lock time.
-   Maximum lock time (lock_time_max): Maximum slow log statement lock time.
-   Number of rows sent (Rows_sent_sum): Total number of data rows sent by a slow log statement.
-   Number of rows scanned (Rows_examined_sum): Total number of data rows scanned by a slow log statement.
