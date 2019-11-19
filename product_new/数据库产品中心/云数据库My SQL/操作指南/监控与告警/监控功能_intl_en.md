## Performance Monitoring
To make it easier for you to view and stay up to date with how instances work, TencentDB for MySQL provides a wide variety of performance monitoring metrics and convenient monitoring features (custom view, time comparison, merged monitoring metrics, etc). You can log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), and view them in **Instance Monitoring** on the instance management page.


>- You can also view instance monitoring metrics by calling the [TencentCloud for MySQL monitoring data API](https://intl.cloud.tencent.com/document/api/248/11006) in Cloud Monitor.
>- If the number of tables in a single instance exceeds one million, database monitoring may be affected. Please control this value appropriately and make sure that it is below one million.

## Types of Instances for Monitoring
TencentDB for MySQL master, read-only, and disaster recovery instances can be monitored, and each instance is provided with a separate monitoring view for easy query.

## Types of Monitoring
Four types of monitoring are available for TencentDB for MySQL: resource monitoring, engine monitoring (general), engine monitoring (extended), and deployment monitoring. You can view the metrics of different monitoring types to gain a quick and accurate understanding of how instances perform and operate.
- **Resource monitoring** provides monitoring data of CPU, memory, disk, and network.
- **Engine monitoring (general)** provides monitoring data of the number of connections, locks, hotspot tables, and slow queries, helping you troubleshoot issues and optimize the performance.
- **Engine monitoring (extended)** provides a wider variety of engine-related monitoring metrics so as to assist you in identifying existing or potential database problems as much as possible.
- **Deployment monitoring** provides monitoring metrics with regard to master-slave delay.


>- Deploy monitoring on the master: When the monitored instance is a master instance which is not a slave of any instance, replicating relevant monitoring data from the master won't work, and the IO and SQL threads are disabled. Replicating relevant monitoring data can work and the IO and SQL threads can be enabled only when the monitored instance is a disaster recovery or a read-only instance.
> - Deploy monitoring on the slave: The master instance and disaster recovery instance in HA edition come in a one-master-one-slave architecture by default. As a result, replicating relevant monitoring data from the slave can work only when the monitored instance is a master or disaster recovery instance. Such data can be used to reflect the delay distance and time between the master or disaster recovery instance and its hidden slave nodes. You are recommended to keep an eye out for the relevant monitoring data of the slave. If the master or disaster recovery instance fails, its monitored hidden slave nodes can be promoted into the master instance quickly.
> 
> ![](https://main.qcloudimg.com/raw/183cebeb93cdeaca2dedeb228ab8f0be.png)

## Monitoring Granularity
TencentDB for MySQL has adopted an adaptive policy for monitoring granularity since August 11, 2018, which means that you cannot select a monitoring granularity as desired for the time being. In addition, TencentDB for MySQL supports free monitoring at a granularity of 5 seconds. If fees will be charged for monitoring, we will inform you in advance. Below is the adaptive policy:

| Time Span | Monitoring Granularity | Adaptation Description | Retention Period |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5 seconds | The time span is below 4 hours, and the monitoring granularity is 5 seconds | 1 day |
| (4h, 2d] | 1 minute | The time span is above 4 hours but below 2 days, and the monitoring granularity is 1 minute | 15 days |
| (2d, 10d] | 5 minutes | The time span is above 2 days but below 10 days, and the monitoring granularity is 5 minutes | 31 days |
| (10d, 30d] | 1 hour | The time span is above 10 days but below 30 days, and the monitoring granularity is 1 hour | 62 days |

>Currently, you can view monitoring data of TencentDB for MySQL in the past 30 days.


## Monitoring Metrics
Cloud Monitor provides the following monitoring metrics for TencentDB for MySQL instances:

| Metric Name | Metric | Unit | Dimension | Meaning |
|---------|---------|---------|---------|----|
| Queries per second | qps | Queries/second | Instance | The number of SQL statements executed by the database per second (including insert, select, update, delete, and replace). QPS mainly represents the actual processing capability of the TencentDB instance |
| Number of slow queries | slow_queries | - | Instance | Number of queries that take more than long_query_time second(s) to be executed |
| Number of full table scans | select_scan | Scans/second | Instance | Number of full table scans executed per second |
| Number of queries | select_count | Queries/second | Instance | Number of queries executed per second |
| Number of updates | com_update | Updates/second | Instance | Number of updates executed per second |
| Number of deletions | com_delete | Deletions/second | Instance | Number of deletions executed per second |
| Number of insertions | com_insert | Insertions/second | Instance | Number of insertions executed per second |
| Number of replacements | com_replace | Replacements/second | Instance | Number of replacements executed per second |
| Total number of requests | queries | Requests/second | Instance | All executed SQL statements such as set and show. |
| Number of active connections | threads_connected | - | Instance | Number of currently enabled connections |
| Query rate | query_rate | % | Instance | Actual QPS/recommended QPS |
| Used disk capacity | real_capacity | MB | Instance | This includes only MySQL's data directories but not logs such as binlog, relaylog, undolog, errorlog, and slowlog |
| Occupied disk capacity | capacity | MB | Instance | This includes MySQL's data directories and logs such as binlog, relaylog, undolog, errorlog, and slowlog |
| Amount of data sent | bytes_sent | MB/s | Instance | Number of bytes sent per second |
| Amount of data received |bytes_received| MB/s | Instance | Number of bytes received per second |
| Disk utilization |volume_rate|%| Instance | Used disk capacity/purchased instance capacity |
| Query cache hit rate |qcache_hit_rate|%| Instance | Query cache hit rate |
| Query cache utilization |qcache_use_rate|%| Instance | Query cache utilization |
| Number of waited table locks |table_locks_waited| Locks/second | Instance | Number of table locks due to the failure to obtain tables immediately |
| Number of temp tables |created_tmp_tables| Tables/second | Instance | Number of temp tables created per second. |
| InnoDB cache hit rate |innodb_cache_hit_rate|%| Instance | InnoDB engine cache hit rate |
| InnoDB cache utilization |innodb_cache_use_rate|%| Instance | InnoDB engine cache utilization |
| Number of InnoDB disk reads |innodb_os_file_reads| Reads/second | Instance | Number of reads to disk files by the InnoDB engine per second |
| Number of InnoDB disk writes |innodb_os_file_writes| Writes/second | Instance | Number of writes to disk files by the InnoDB engine per second |
| Number of InnoDB fsync calls |innodb_os_fsyncs| Calls/second | Instance | Number of calls of the fsync function by the InnoDB engine per second |
| Number of tables currently opened by InnoDB |innodb_num_open_files| - | Instance | Number of tables currently opened by the InnoDB engine |
| MyISAM cache hit rate |key_cache_hit_rate|%| Instance | MyISAM engine cache hit rate |
| MyISAM cache utilization |key_cache_use_rate|%| Instance | MyISAM engine cache utilization |
| CPU utilization |cpu_use_rate|%| Instance | Overuse is permitted while idle. The CPU utilization may exceed 100% |
| Memory utilization |memory use rate|%| Instance | Overuse is permitted while idle. The memory utilization may exceed 100% |
| Memory usage |memory use|MB| Instance | Overuse is permitted while idle. The actual memory usage may exceed the purchased specification |
| Number of temp files |created_tmp_files| Files/second | Instance | Number of temp files created per second |
| Number of opened tables |opened_tables| - | Instance | Number of opened tables |
| Number of commits | com_commit | Commits/second | Instance | Number of commits per second |
| Number of rollbacks |com_rollback| Rollback/second | Instance| Number of rollbacks per second |
| Number of created threads |threads_created| - | Instance | Number of threads created to process connections |
| Number of running threads |threads_running| - | Instance | Number of active (non-idle) threads |
| Maximum number of connections | max_connections | - | Instance | Maximum number of connections |
| Number of temp disk tables |created_tmp_disk_tables| Tables/second | Instance | Number of temp disk tables created per second |
| Number of requests to read the next row | handler_read_rnd_next | Requests/second | Instance | Number of requests to read the next row per second |
| Number of internal rollbacks |handler_rollback| Rollbacks/second | Instance | Number of transaction rollbacks per second |
| Number of internal commits |handler_commit | Commits/second | Instance | Number of transaction commits per second |
| Number of empty InnoDB pages |innodb_buffer_pool_pages_free| - | Instance | Number of empty memory pages in the InnoDB engine |
| Total number of InnoDB pages |innodb_buffer_pool_pages_total| - | Instance | Total number of memory pages occupied by the InnoDB engine |
| InnoDB logical reads |innodb_buffer_pool_read_requests| Reads/second | Instance | Number for logical read requests completed by the InnoDB engine per second |
| Number of InnoDB physical reads |innodb_buffer_pool_reads| Reads/second | Instance | Number for physical read requests completed by the InnoDB engine per second |
| Amount of data read by InnoDB |innodb_data_read| Bytes/s | Instance | Number of bytes read by the InnoDB engine per second |
| Total number of InnoDB reads |innodb_data_reads| Reads/second | Instance | Number of data reads completed by the InnoDB engine per second |
| Total number of InnoDB writes |innodb_data_writes| Writes/second | Instance | Number of data writes completed by the InnoDB engine per second |
| Amount of data written by InnoDB |innodb_data_written| Bytes/s | Instance | Number of bytes written by the InnoDB engine per second |
| Number of rows deleted by InnoDB | innodb_rows_deleted | Rows/second | Instance | Number of rows deleted by the InnoDB engine per second |
| Number of rows inserted by InnoDB | innodb_rows_inserted | Rows/second | Instance | Number of rows inserted by the InnoDB engine per second |
| Number of rows updated by InnoDB |innodb_rows_updated| Rows/second | Instance | Number of rows updated by the InnoDB engine per second |
| Number of rows read by InnoDB |innodb_rows_read| Rows/second | Instance | Number of rows read by the InnoDB engine per second |
| Average time of row lock in InnoDB |innodb_row_lock_time_avg| Milliseconds | Instance | Average time of row lock in the InnoDB engine |
| Number of row locks waited by InnoDB |innodb_row_lock_waits| Locks/second | Instance | Number of row locks waited by the InnoDB engine per second |
| Number of unused blocks in the key cache |key_blocks_unused| - | Instance | Number of unused blocks in the key cache in the MyISAM engine |
| Number of used blocks in the key cache |key_blocks_used| - | Instance | Number of used blocks in the key cache in the MyISAM engine |
| Number of block reads from the key cache |key_read_requests| Reads/second | Instance | Number of block reads from the key cache by the MyISAM engine per second |
| Number of block reads from the disk |key_read| Reads/second | Instance | Number of block reads from the disk by the MyISAM engine per second |
| Number of block writes to the key cache |key_write_requests| Writes/second | Instance | Number of block writes to the key cache by the MyISAM engine per second |
| Number of block writes to the disk |key_write_requests| Writes/second | Instance | Number of block writes to the disk by the MyISAM engine per second |
| Master-slave delay distance | master_slave_sync_distance | MB | Instance | Master-slave binlog delay |
| Master-slave delay time |	seconds_behind_master|	Seconds |	 Instance |	 Master-slave delay time |
| IO thread status |	slave_io_running|	 Status value (0: yes, 1: no, 2: connecting) |	 Instance | 	IO thread status |
| SQL thread status |	slave_sql_running|	 Status value (0: yes, 1: no) |	 Instance | 	SQL thread status |

For more information on how to use TencentDB monitoring metrics, see the [TencentDB for MySQL APIs](https://intl.cloud.tencent.com/document/product/248/11006) in Cloud Monitor.

