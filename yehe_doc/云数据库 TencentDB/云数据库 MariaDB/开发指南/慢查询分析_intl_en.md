## 1. Feature Description
An SQL statement query that takes more time than the specified value is referred to as a "slow query", and the corresponding statement is called a "slow query statement". The process where a database administrator (DBA) analyzes slow query statements and finds out the reasons why slow queries occur is known as "slow query analysis".

TencentDB for MariaDB provides slow query analysis in **Instance Management** > **Performance Optimization**.
![](https://main.qcloudimg.com/raw/dcd710a8b0d0676bf9945695731173a6.png)
## 2. Main Parameters
### 2.1. Main default settings
-   Slow query feature: enabled by default.
-   Slow query time (long_query_time): 1 second by default, that is, only slow query statements that exceed 1 second will be logged.
-   Analyzed data output delay: 1–5 minutes.
-   Logging duration: 30 days, depending on the backup and log settings.

### 2.2. Fields in the analysis list
-   Checksum (checksum): a sequence of digits used to identify a slow query statement (64-bit by default);
-   Abstracted slow query statement (fingerprint): slow query statement with user data hidden;
-   Database: the database in which a slow query statement occurs;
-   Account: the account under which a slow query statement occurs;
-   Last execution time (last_seen): the time when a slow query statement last occurred within the time range;
-   First execution time (first_seen): the time when a slow query statement first occurred within the time range;
-   Total number of occurrences (ts_cnt): the number of occurrences of a slow query statement within the time range;
-   Occurrence percentage: occurrence percentage of a slow query statement in relation to all slow query statements within the time range;
-   Total time (query_time_sum): total time of a slow query statement within the time range;
-   Total time percentage: total time percentage of a slow query statement within the time range;
-   Average time (query_time_avg): average time calculated by dividing the total time of a slow query statement with total number of occurrences;
-   Minimum time (query_time_min): minimum occurrence time of a slow query statement;
-   Maximum time (query_time_max): maximum occurrence time of a slow query statement;
-   Total lock time (lock_time_sum): total lock time of a slow query statement;
-   Total lock time percentage: time percentage of a slow query statement in relation to total slow query statement lock time within the time range;
-   Average lock time (lock_time_avg): average time calculated by dividing total slow query statement lock time with total number of locks;
-   Minimum lock time (lock_time_min): minimum slow query statement lock time;
-   Maximum lock time (lock_time_max): maximum slow query statement lock time;
-   Number of rows sent (Rows_sent_sum): total number of data rows sent by a slow query statement;
-   Number of rows scanned (Rows_examined_sum): total number of data rows scanned by a slow query statement.
