To make it easier for you to view and stay up to date with how instances work, TencentDB for MySQL provides a wide variety of performance monitoring metrics and convenient monitoring features (custom view, time comparison, merged monitoring metrics, etc). You can log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and view them in **Instance Monitoring** on the instance management page.
>?
>- You can get instance monitoring metrics by calling the [GetMonitorData API](https://intl.cloud.tencent.com/document/product/248/33881) or using the [TencentDB for MySQL Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/11006) in Cloud Monitor.
>- You can [create dashboards](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=10) for monitoring metrics to analyze monitored data dynamically.
>- If the number of tables in a single instance exceeds one million, database monitoring may be affected. Please control this value appropriately and make sure that it is below one million.

## Types of Instances for Monitoring
TencentDB for MySQL master, read-only, and disaster recovery instances can be monitored, and each instance is provided with a separate monitoring view for easy query.

## Types of Monitoring
Four types of monitoring are available for TencentDB for MySQL: resource monitoring, engine monitoring (general), engine monitoring (extended), and deployment monitoring. You can view the metrics of different monitoring types to gain a quick and accurate understanding of how instances perform and operate.
- **Resource monitoring** provides monitoring data of CPU, memory, disk, and network.
- **Engine monitoring (general)** provides monitoring data of the number of connections, locks, hotspot tables, and slow queries, helping you troubleshoot issues and optimize the performance.
- **Engine monitoring (extended)** provides a wider variety of engine-related monitoring metrics so as to assist you in identifying existing or potential database problems as much as possible.
- **Deployment monitoring** provides monitoring metrics with regard to master-slave delay. It divides into master and slave:
 - Master deployment monitoring: when the monitored instance is a master instance which is not a slave of any instance, replicating relevant monitoring data from the master won't work, and the IO and SQL threads are disabled. Replicating relevant monitoring data can work and the IO and SQL threads can be enabled only when the monitored instance is a disaster recovery or a read-only instance.
 
- Deploy monitoring on the replica: the source instance and disaster recovery instance in High-Availability Edition come in a one-source-one-replica architecture by default. As a result, replicating relevant monitoring data from the replica can work only when the monitored instance is a source or disaster recovery instance. Such data can be used to reflect the delay distance and time between the source or disaster recovery instance and its hidden replica nodes. We recommend that you keep an eye out for the relevant monitoring data of the replica. If the source or disaster recovery instance fails, its monitored hidden replica nodes can be promoted into the source instance quickly.
 
![](https://main.qcloudimg.com/raw/183cebeb93cdeaca2dedeb228ab8f0be.png)

## Monitoring Granularity
TencentDB for MySQL has adopted an adaptive policy for monitoring granularity since August 11, 2018, which means that you cannot select a monitoring granularity as desired for the time being. The adaptive policy is as follows:

| Time Span | Monitoring Granularity | Adaptation Description | Retention Period |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5 seconds | The time span is below 4 hours, and the monitoring granularity is 5 seconds | 1 day |
| (4h, 2d] | 1 minute | The time span is above 4 hours but below 2 days, and the monitoring granularity is 1 minute | 15 days |
| (2d, 10d] | 5 minutes | The time span is above 2 days but below 10 days, and the monitoring granularity is 5 minutes | 31 days |
| (10d, 30d] | 1 hour | The time span is above 10 days but below 30 days, and the monitoring granularity is 1 hour | 62 days |

>?Currently, you can view monitoring data of TencentDB for MySQL in the last 30 days.



## Monitoring Metrics
Cloud Monitor provides the following monitoring metrics for TencentDB for MySQL instances in the instance dimension:

>?For more information on how to use TencentDB monitoring metrics, please see the [GetMonitorData API](https://intl.cloud.tencent.com/document/product/248/11006) in Cloud Monitor.

| Metric Name | Metric | Unit | Description |
|---------|---------|---------|---------|
| Operations/sec | qps | Operations/second | Number of SQL statements executed by the database per second (including insert, select, update, delete, and replace). QPS mainly represents the actual processing capability of the TencentDB instance |
|Transactions executed per second| tps |Transactions/second|Number of transactions executed per second in the database|
| Slow Queries | slow_queries | - | Number of queries that take more than `long_query_time` second(s) to be executed |
| Full Table Scans | select_scan | Scans/second | Number of full-table scans executed per second |
| Queries | select_count | Queries/second | Number of queries executed per second |
| Updates | com_update | Updates/second | Number of updates executed per second |
| Deletions | com_delete | Deletions/second | Number of deletions executed per second |
| Insertions | com_insert | Insertions/second | Number of insertions executed per second |
| Overwrites | com_replace | Overwrites/second | Number of overwrites executed per second |
| Total Requests | queries | Requests/second | All executed SQL statements such as set and show. |
| Opened Connections | threads_connected | - | Number of currently open connections |
| Connection Utilization |connection_use_rate|%| Number of open connections/maximum connections   |
| Query Utilization | query_rate | % | Actual QPS/recommended QPS |
| Used Space Disk | real_capacity | MB | This includes only MySQL's data directories but not logs such as binlog, relaylog, undolog, errorlog, and slowlog |
| Occupied Disk Space | capacity | MB | This includes MySQL's data directories and logs such as binlog, relaylog, undolog, errorlog, and slowlog |
| Sent Data Volume | bytes_sent | MB/s | Number of bytes sent per second |
| Received Data Volume |bytes_received| MB/s | Number of bytes received per second |
| Disk Utilization |volume_rate|%| Used disk space/purchased instance space |
| Query Cache Hit Rate |qcache_hit_rate|%| Query cache hit rate |
| Query Cache Utilization |qcache_use_rate|%| Query cache utilization |
| Table Locks Awaited |table_locks_waited| Locks/second | Number of table locks due to the failure to obtain tables immediately |
| Temp Tables |created_tmp_tables| Tables/second | Number of temp tables created per second. |
| InnoDB Cache Hit Rate |innodb_cache_hit_rate|%| InnoDB cache hit rate |
| InnoDB Cache Utilization |innodb_cache_use_rate|%| cache utilization |
| InnoDB Disk Reads |innodb_os_file_reads| Reads/second | Number of reads to disk files by the InnoDB engine per second |
| InnoDB Disk Writes |innodb_os_file_writes| Writes/second | Number of writes to disk files by the InnoDB engine per second |
| InnoDB fsync Count |innodb_os_fsyncs| Calls/second | Number of calls of the fsync function by the InnoDB engine per second |
| InnoDB Opened Tables |innodb_num_open_files| - | Number of tables currently opened by the InnoDB engine |
| MyISAM Cache Hit Rate |key_cache_hit_rate|%| MyISAM engine cache hit rate |
| MyISAM Cache Utilization |key_cache_use_rate|%| MyISAM engine cache utilization |
| CPU Utilization |cpu_use_rate|%| Overuse of idle resources is permitted. The CPU utilization may exceed 100% |
| MEM Utilization |memory use rate|%| Overuse of idle resources is permitted. The memory utilization may exceed 100% |
| Memory Usage |memory use|MB| Overuse of idle resources is permitted. The actual memory usage may exceed the purchased specification |
| Temp Files |created_tmp_files| Files/second | Number of temp files created per second |
| Opened Tables |opened_tables| - | Number of opened tables |
| Submissions | com_commit | Commits/second | Number of submissions per second |
| Rollbacks |com_rollback| Rollback/second | Number of rollbacks per second |
| Created Threads |threads_created| - | Number of threads created to process connections |
| Running Threads |threads_running| - | Number of active (non-idle) threads |
| Max Connections | max_connections | - | Maximum number of connections |
| Temp Disk Tables | created_tmp_disk_tables| Tables/second | Number of temp disk tables created per second |
| Requests of Reading Next Row | handler_read_rnd_next | Requests/second | Number of requests to read the next row per second |
| Internal Rollbacks |handler_rollback| Rollbacks/second | Number of transaction rollbacks per second |
| Internal Submissions |handler_commit | Commits/second | Number of transaction commits per second |
| InnoDB Empty Pages |innodb_buffer_pool_pages_free| - | Number of empty memory pages in the InnoDB engine |
| Total InnoDB Pages |innodb_buffer_pool_pages_total| - | Total number of memory pages occupied by the InnoDB engine |
| InnoDB Logical Reads |innodb_buffer_pool_read_requests| Reads/second | Number for logical read requests completed by the InnoDB engine per second |
| InnoDB Physical Reads |innodb_buffer_pool_reads| Reads/second | Number for physical read requests completed by the InnoDB engine per second |
| InnoDB Reads |innodb_data_read| Bytes/s | Number of bytes read by the InnoDB engine per second |
| Total InnoDB Reads |innodb_data_reads| Reads/second | Number of data reads completed by the InnoDB engine per second |
| Total InnoDB Writes |innodb_data_writes| Writes/second | Number of data writes completed by the InnoDB engine per second |
| InnoDB Writes |innodb_data_written| Bytes/s | Number of bytes written by the InnoDB engine per second |
| InnoDB Rows Deleted | innodb_rows_deleted | Rows/second | Number of rows deleted in the InnoDB engine per second |
| InnoDB Rows Inserted | innodb_rows_inserted | Rows/second | Number of rows inserted in the InnoDB engine per second |
| InnoDB Rows Updated |innodb_rows_updated| Rows/second | Number of rows updated by the InnoDB engine per second |
| InnoDB Rows Read |innodb_rows_read| Rows/second | Number of rows read by the InnoDB engine per second |
| Average Lock Time of InnoDB's Acquiring Rows |innodb_row_lock_time_avg| Milliseconds | Average time of row lock in the InnoDB engine |
| InnoDB Row Lock Waits |innodb_row_lock_waits| Locks/second | Number of row locks waited by the InnoDB engine per second |
| Unused Blocks in Key Cache |key_blocks_unused| - | Number of unused blocks in the key cache in the MyISAM engine |
| Used Blocks in Key Cache |key_blocks_used| - | Number of used blocks in the key cache in the MyISAM engine |
| Data Blocks Read by Key Cache |key_read_requests| Reads/second | Number of block reads from the key cache by the MyISAM engine per second |
| Data Blocks Read by Disks |key_read| Reads/second | Number of block reads from the disk by the MyISAM engine per second |
| Data Blocks Written into Key Cache |key_write_requests| Writes/second | Number of block writes to the key cache by the MyISAM engine per second |
| Data Blocks Written into Disks |key_write_requests| Writes/second | Number of block writes to the disk by the MyISAM engine per second |
| Master-Slave Delay Distance | master_slave_sync_distance | MB | Master-slave binlog delay |
| Master-Slave Delay Time |	seconds_behind_master|	Seconds | Master-slave delay time |
| IO Thread Status |	slave_io_running|	 Status value (0: yes, 1: no, 2: connecting) | IO thread status |
| SQL Thread Status |	slave_sql_running|	 Status value (0: yes, 1: no) | SQL thread status |
