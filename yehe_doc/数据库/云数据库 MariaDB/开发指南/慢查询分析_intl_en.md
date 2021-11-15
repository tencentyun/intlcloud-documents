## 1. Feature Description
An SQL statement query that takes more time than the specified value is referred to as a "slow query", and the corresponding statement is called a "slow query statement". The process where a database administrator (DBA) analyzes slow query statements and finds out the reasons why slow queries occur is known as "slow query analysis".

TencentDB for MariaDB provides slow query analysis in **Instance Management** > **Performance Optimization**.

## 2. Main Parameters
### 2.1. Main default settings
-   Slow log feature: enabled by default.
-   Slow query threshold (long_query_time): 1 second by default, that is, only query statements executed for more than 1 second will be logged.
-   Analyzed data output delay: 1–5 minutes.
-   Logging duration: 30 days, depending on the backup and log settings.

### 2.2. Fields in the analysis list
-   **Checksum** (checksum): a sequence of digits used to identify a slow query statement (64-bit by default);
-   **Abstracted SQL Statement** (fingerprint): a slow query statement with user data hidden;
-   **Database**: the database in which the slow query statement was executed;
-   **Account**: the account under which the slow query statement was executed;
-   **Last Execution Time** (last_seen): the time when the slow query statement was last executed within the specified time range;
-   **First Execution Time** (first_seen): the time when the slow query statement was first executed within the specified time range;
-   **Total** (ts_cnt): the number of executions of the slow query statement within the specified time range;
-   **Total Executions (%)**: the ratio of total executions of the slow query statement to the total executions of all slow query statements within the specified time range;
-   **Total Time** (query_time_sum): the total time consumed by the slow query statement within the specified time range;
-   **Total Time (%)**: the ratio in percentage of the total time consumed by the slow query statement to the specified time range;
-   **Average Time** (query_time_avg): the average time is calculated by dividing the total time consumed by the slow query statement by the total number of executions of the slow query statement;
-   **Min. Time** (query_time_min): the minimum among all execution time of the slow query statement;
-   **Max. Time** (query_time_max): the maximum among all execution time of the slow query statement;
-   **Total Lock Time** (lock_time_sum): the total lock time of the slow query statement;
-   **Total Lock Time (%)**: the ratio in percentage of the total lock time of the slow query statement to the total lock time of all slow query statements;
-   **Average Lock Time** (lock_time_avg): the average time calculated by dividing the total lock time of the slow query statement by the total number of locks of the slow query statement;
-   **Min. Lock Time** (lock_time_min): the minimum among all lock time of the slow query statement;
-   **Max. Lock Time** (lock_time_max): the maximum among all lock time of the slow query statement;
-   **Sent Rows** (Rows_sent_sum): the total number of data rows sent by the slow query statement;
-   **Scanned Rows** (Rows_examined_sum): the total number of data rows scanned by the slow query statement;
