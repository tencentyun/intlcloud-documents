To make it easier for you to view and stay up to date with how instances work, TencentDB for MySQL provides a wide variety of performance monitoring metrics and convenient monitoring features (custom view, time comparison, merged monitoring metrics, etc). You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), and view them in **Instance Monitoring** on the instance management page.
>?
>- You can get instance monitoring metrics by calling the [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/39306) API or using the TencentDB for MySQL [monitoring metrics](https://intl.cloud.tencent.com/zh/document/product/248/11006) in Cloud Monitor.
>- You can [create dashboards](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=10) for monitoring metrics to analyze monitored data dynamically.
>- If the number of tables in a single instance exceeds one million, database monitoring may be affected. Please control this value appropriately and make sure that it is below one million.

## Types of Instances for Monitoring
TencentDB for MySQL source instances, read-only replicas, and disaster recovery instances can be monitored, and each instance is provided with a separate monitoring view for easy query.

## Types of Monitoring
Four types of monitoring are available for TencentDB for MySQL: resource monitoring, engine monitoring (general), engine monitoring (extended), and deployment monitoring. You can view the metrics of different monitoring types to gain a quick and accurate understanding of how instances perform and operate.
- **Resource monitoring** provides monitoring data of CPU, memory, disk, and network.
- **Engine monitoring (general)** provides monitoring data of the number of connections, locks, hotspot tables, and slow queries, helping you troubleshoot issues and optimize the performance.
- **Engine monitoring (extended)** provides a wider variety of engine-related monitoring metrics so as to assist you in identifying existing or potential database problems as much as possible.
- **Deployment monitoring** provides monitoring metrics with regard to source-replica delay. It divides into source monitoring and replica monitoring:
 - Deploy monitoring on the source: when the monitored instance is a source instance which is not a replica of any instance, replication-related monitoring data is invalid for the source, and the IO and SQL threads are disabled. Replication-related monitoring data is valid and the IO and SQL threads can be enabled only when the monitored instance is a disaster recovery or a read-only replica.

 - Deploy monitoring on the replica: the two-node or three-node source instance and disaster recovery instance come in a source/replica architecture by default. As a result, replication-related monitoring data is valid for the replica only when the monitored instance is a source or disaster recovery instance. Such monitoring data can reflect the replication delay distance and time between the source or disaster recovery instance and its hidden replica nodes. You are recommended to keep an eye out for such monitoring data of the replica. If the source or disaster recovery instance fails, its monitored hidden replica nodes can be promoted into the source instance quickly.

![](https://main.qcloudimg.com/raw/183cebeb93cdeaca2dedeb228ab8f0be.png)

## Monitoring Granularity
TencentDB for MySQL has adopted an adaptive policy for monitoring granularity since August 11, 2018, which means that you cannot select a monitoring granularity as desired for the time being. The adaptive policy is as follows:

| Time Span | Monitoring Granularity | Adaptation Description | Retention Period |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5 seconds | The time span is below 4 hours, and the monitoring granularity is 5 seconds | 1 day |
| (4h, 2d] | 1 minute | The time span is above 4 hours but below 2 days, and the monitoring granularity is 1 minute | 15 days |
| (2d, 10d] | 5 minutes | The time span is above 2 days but below 10 days, and the monitoring granularity is 5 minutes | 31 days |
| (10d, 30d] | 1 hour | The time span is above 10 days but below 30 days, and the monitoring granularity is 1 hour | 62 days |

>?Currently, you can view monitoring data of TencentDB for MySQL in the past 30 days.

## Monitored Metrics
Cloud Monitor provides the following monitoring metrics for TencentDB for MySQL instances in the instance dimension:

For more information on how to use TencentDB monitoring metrics, please see the [TencentDB for MySQL APIs](https://intl.cloud.tencent.com/zh/document/product/248/11006) in Cloud Monitor.

| Metric Name | Parameter | Unit | Description |
|---------|---------|---------|---------|
| Queries per Second | qps | Counts/second | Number of SQL statements (INSERT, SELECT, UPDATE, DELETE, and REPLACE) executed by the database per second. This metric mainly represents the actual processing capability of the TencentDB instance. |
| Transactions per Second | tps | Counts/second | The number of transactions executed per second in the database |
| Slow Queries | slow_queries | - | The number of queries that take more than `long_query_time` second(s) to be executed |
| Full Table Scans | select_scan | Counts/second | The number of full-table scans executed per second |
| SELECT Queries | select_count | Counts/second | The number of SELECT statements executed per second |
| UPDATE Queries | com_update | Counts/second | Number of UPDATE statements executed per second |
| DELETE Queries | com_delete | Counts/second | The number of DELETE statements executed per second |
| INSERT Queries | com_insert | Counts/second | The number of INSERT statements executed per second |
| REPLACE Queries | com_replace | Counts/second | The number of REPLACE statements executed per second |
| Total Queries | queries | Counts/second | All executed SQL statements such as SET and SHOW. |
| Open Connections | threads_connected | - | The number of currently open connections |
| Connection Utilization | connection_use_rate | % | The number of open connections/the maximum number of connections   |
| Query Utilization | query_rate | % | Actual QPS/recommended QPS |
| Used Disk Space | capacity | MB | This includes MySQL's data directories and logs such as binlog, relaylog, undolog, errorlog, and slowlog. |
| Disk Space Used by Data | real_capacity | MB | This includes only MySQL's data directories. |
| Disk Space Used by Logs | disk_log_used  | MB | This includes only MySQL's logs such as binlog, relaylog, undolog, errorlog, and slowlog. |
| Disk Space Used by Temp Files | disk_tmp_used | MB | This includes only MySQL's temp files. |
| Private Outbound Traffic | bytes_sent       | Bytes/second | Bytes sent per second |
| Private Inbound Traffic | bytes_received | Bytes/second | Bytes received per second |
| Disk Utilization | volume_rate | % | Used disk capacity/purchased instance capacity |
| Query Cache Hit Rate | qcache_hit_rate | % | Query cache hit rate |
| Query Cache Utilization | qcache_use_rate | % | Query cache utilization |
| Table Lock Waits |table_locks_waited| Counts/second | The number of times that a request for a table lock could not be granted immediately and a wait was needed |
| Temp Tables | created_tmp_tables | Counts/second | The number of internal temporary tables created by the server while executing statements |
| InnoDB cache hit rate | innodb_cache_hit_rate | % | InnoDB engine cache hit rate |
| InnoDB cache utilization | innodb_cache_use_rate | % | InnoDB engine cache utilization |
| InnoDB Disk Reads |innodb_os_file_reads| Counts/second | The total number of file reads performed by read threads within InnoDB. |
| InnoDB Disk Writes | innodb_os_file_writes | Counts/second | The total number of file writes performed by write threads within InnoDB. |
| InnoDB fsync() Calls | innodb_os_fsyncs | Counts/second | The number of calls of the fsync function by InnoDB per second |
| InnoDB Opened Files | innodb_num_open_files | - | The number of files InnoDB currently holds open |
| MyISAM Cache Hit Rate | key_cache_hit_rate | % | MyISAM engine cache hit rate |
| MyISAM Cache Utilization | key_cache_use_rate | % | MyISAM engine cache utilization |
| CPU Utilization | cpu_use_rate | % | If overuse of idle resources is permitted, the CPU utilization may exceed 100%. |
| Memory Utilization | memory use rate | % | If overuse of idle resources is permitted, the memory utilization may exceed 100%. |
| Used Memory | memory_use | MB | If overuse of idle resources is permitted, the used memory may exceed the purchased specification. |
| Temp Files | created_tmp_files | Counts/second | The number of temp files created per second |
| Open Tables | opened_tables     | -      | Instance-level metric |
| COMMIT Statements | com_commit | Counts/second | The number of COMMIT statements executed |
| ROLLBACK Statements |com_rollback| Counts/second | The number of ROLLBACK statements executed |
| Created Threads | threads_created | - | The number of threads created to handle connections |
| Running Threads | threads_running | - | The number of threads that are not sleeping |
| Max. Connections | max_connections | - | The maximum number of connections |
| Temp Disk Tables | created_tmp_disk_tables | Counts/second | The number of internal on-disk temporary tables created by the server while executing statements |
| Requests to Read Next Row | handler_read_rnd_next | Counts/second | The number of requests to read the next row in the data file. |
| Internal ROLLBACK Statements | handler_rollback | Counts/second | The number of requests for a storage engine to perform a rollback operation |
| Internal COMMIT Statements | handler_commit | Counts/second | The number of internal COMMIT statements executed |
| InnoDB Free Pages | innodb_buffer_pool_pages_free | - | The number of free pages in the InnoDB buffer pool |
| Total InnoDB Pages | innodb_buffer_pool_pages_total | - | The total size of the InnoDB buffer pool in pages |
| InnoDB Logical Reads |innodb_buffer_pool_read_requests| Counts/second | The number of logical read requests |
| InnoDB Physical Reads | innodb_buffer_pool_reads | Counts/second | The number of logical reads that InnoDB could not satisfy from the buffer pool, and had to read directly from disk |
| Data Read in InnoDB | innodb_data_read | Bytes/second | The amount of data read per second |
| Total InnoDB Reads |innodb_data_reads| Counts/second | The total number of data reads per second |
| Total InnoDB Writes |innodb_data_writes| Counts/second | The total number of data writes per second |
| Data Written in InnoDB | innodb_data_written | Bytes/second | The amount of data written per second |
| InnoDB Rows Deleted | innodb_rows_deleted | Counts/second | The number of rows deleted from InnoDB tables |
| InnoDB Rows Inserted | innodb_rows_inserted | Counts/second | The number of rows inserted into InnoDB tables |
| InnoDB Rows Updated | innodb_rows_updated | Counts/second | The number of rows updated in InnoDB tables |
| InnoDB Rows Read | innodb_rows_read | Counts/second | The number of rows read from InnoDB tables |
| Avg. Time to Acquire an InnoDB Row Lock | innodb_row_lock_time_avg | Milliseconds | The average time to acquire a row lock for InnoDB tables |
| InnoDB Row Lock Waits | innodb_row_lock_waits | Counts/second | The number of times operations on InnoDB tables had to wait for a row lock |
| Unused Blocks in Key Cache | key_blocks_unused | - | The number of unused blocks in the MyISAM key cache  |
| Used Blocks in Key Cache | key_blocks_used | - | The number of used blocks in the MyISAM key cache |
| Blocks Read from Key Cache | key_read_requests| Counts/second | The number of requests to read a key block from the MyISAM key cache |
| Blocks Read from Disk | key_reads | Counts/second | The number of physical reads of a key block from disk into the MyISAM key cache |
| Blocks Written into Key Cache | key_write_requests | Counts/second | The number of requests to write a key block to the MyISAM key cache. |
| Blocks Written into Disk | key_writes | Counts/second | The number of physical writes of a key block from the MyISAM key cache to disk. |
| Source-Replica Delay (in MB) | master_slave_sync_distance | MB | The amount of data by which the replica has lagged behind the source |
| Source-Replica Delay (in Seconds) |seconds_behind_master|Seconds  | The amount of time by which the replica has lagged behind the source |
| IO Thread Status | slave_io_running | Status value (0: yes, 1: no, 2: connecting) | IO thread status |
| SQL Thread Status | slave_sql_running | Status value (0: yes, 1: no) | SQLA thread status |

