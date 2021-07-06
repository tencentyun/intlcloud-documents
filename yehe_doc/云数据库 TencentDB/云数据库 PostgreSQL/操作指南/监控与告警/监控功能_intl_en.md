
## Monitoring in Console
To make it easier for you to view and stay up to date with how instances work, TencentDB for PostgreSQL provides a wide variety of performance monitoring metrics. You can log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql) and view them on the **System Monitoring** tab on the corresponding instance management page.

#### Monitoring metrics

| Metric Name | Metric | Unit | Description |
| -------------------------- | ----------------- | ----- | ------------------------------------------------------------ |
| CPU Utilization                  | cpu               | %     | Actual CPU utilization                                              |
| Used Storage Capacity               | storage           | GB    | Used instance space                                         |
| Data File Size               | data_file_size    | GB    | Size of data files                                       |
| WAL File Size               | log_file_size     | GB    | Size of WAL log files                                    |
| Temp File Size               | temp_file_size    | MB    | Size of temporary files                                             |
| Storage Space Utilization             | storage_rate      | %     | Total storage space utilization, which takes into account the temporary, data, and log files and other types of database files |
| Queries per Second                 | qps               | Counts/sec | Average number of executed SQL statements per second                                  |
| Connections                     | connections       | -    | Total number of current connections when metric collection is initiated on the database                     |
| Connections Created in the Last 5 Sec            | new_conn_in5s     | -    | Total number of connections established in the last 5 seconds when metric collection is initiated on the database    |
| Active Connections                 | active_conns      | -    | Number of currently active (non-idle) connections when metric collection is initiated on the database       |
| Idle Connections                 | idle_conns        | -    | Number of idle connections when metric collection is initiated on the database |
| Waiting Sessions                 | waiting           | -    | Number of sessions in waiting status when metric collection is initiated on the database |
| Sessions Waiting for More Than 5 Sec         | long_waiting      | -    | Number of sessions that stay in waiting status for over 5 seconds in a collection period |
| Idle Transactions                 | idle_in_xact      | -    | Number of idle transactions when metric collection is initiated on the database       |
| Transactions Executed for More Than 1 Sec  | long_xact         | -    | Number of transactions with an execution duration longer than 1 second in a collection period                    |
| Transactions Idle for More than 5 Sec        | long_idle_in_xact | -    | Number of transactions that stay in idle status for over 5 seconds in a collection period                    |
| Transactions per Second                 | tps               | Counts/sec | Average number of successfully executed transactions (including rollbacks and commits) per second                   |
| Transactions Committed /Sec                 | xact_commit       | Counts/sec | Average number of committed transactions per second                                         |
| Transactions Rolled Back /Sec                 | xact_rollback     | Counts/sec | Average number of rolled back transactions per second                                         |
| Requests                     | read_write_calls  | -    | Total number of requests in a statistical period                                     |
| Read Requests                   | read_calls        | -    | Number of read requests in a statistical period                                     |
| Write Requests                   | write_calls       | -    | Number of write requests in a statistical period                                     |
| Other Requests                 | other_calls       | -    | Number of other requests (BEGIN, CREATE, Non-DML, DDL, and DQL operations) in a statistical period |
| Buffer Cache Hit Rate           | hit_percent       | %     | Hit rate of execution of all SQL statements in a request period                       |
| Average SQL Execution Time               | sql_runtime_avg   | ms    | Average execution latency of all SQL statements in a statistical period                    |
| Average of Top 10 Longest SQL Execution Time          | sql_runtime_max   | ms    | Average execution latency of the top 10 SQL statements with the longest latency in a statistical period          |
| Average of Top 10 Shortest SQL Execution Time          | sql_runtime_min   | ms    | Average execution latency of the top 10 SQL statements with the shortest latency in a statistical period          |
| Remaining XIDs                | remain_xid        | -    | Number of remaining XIDs of the database with the fewest remaining XIDs when metric collection is initiated on the database. This metric is unavailable for read-only instances |
| Differences Between sent_lsn and replay_lsn | xlog_diff         | Byte  | Difference between the size of the log sent from the primary node to the standby node and the log replayed on the standby node, which mainly reflects the log application speed of the standby node as well as its performance and network transfer speed. This metric is unavailable for read-only instances |                     
| WAL Flush Lag       | xlog_diff_time    | s     | Time difference between the time point when the log is sent from the primary node to the standby node and the time point when the standby node receives the log and flushes it. This metric is unavailable for read-only instances and instances below v10.x |
| Primary-Standby Sync Delay           | slave_apply_delay | s     | Primary-Standby sync delay. For primary instances, this metric can reflect the RTO of failover. For read-only instances, it indicates the time after which the data written to primary instances can be queried on the read-only instances. The metric for read-only instances has the same name |
| Slow Queries                 | slow_query_cnt    | -    | Number of slow queries in a collection period                           |
| SQLs Executed for More Than 1 Sec     | long_query    | -    | Number of SQL statements with execution time over 1 second when metric collection is initiated on the database     |
| 2PC Transactions                  | 2pc               | -    | Number of current 2PC transactions when metric collection is initiated on the database                        |
| 2PC Transactions Uncommitted for More Than 5 Sec    | long_2pc          | -    | Number of current transactions with execution time over 5 seconds when metric collection is initiated on the database    |
| Rows Deleted /Sec             | tup_deleted       | -    | Average number of deleted tupes per second. This metric is unavailable for read-only instances                 |
| Rows Inserted /Sec             | tup_inserted      | -    | Average number of inserted tupes per second. This metric is unavailable for read-only instances                  |
| Rows Updated /Sec             | tup_updated       | -    | Average number of updated tupes per second. This metric is unavailable for read-only instances                |
| Rows Scanned in Index Scans /Sec     | tup_inserted      | -    | Average number of tupes scanned by the index per second                               |
| Rows Scanned in Sequential Scans /Sec         | tup_returned      | -    | Average number of tupes scanned in the full table per second                                   |
| Deadlocks                     | deadlocks         | -    | Total number of deadlocks in a collection period                                 |


## pg_stat_statements Module
You can also use the [pg_stat_statements](https://www.postgresql.org/docs/9.4/pgstatstatements.html) view to query the detailed PostgreSQL performance metrics. This module provides a method for tracking execution statistics of all SQL statements executed by a server, which can be used to count the resource overheads of the database and analyze top SQL statements.

```
select * from pg_stat_statements;
```
