Cloud Monitor provides the following monitoring metrics for TencentDB (MySQL) instances:

| Metric | Description | Unit | Dimension |
| -------------------------------- | ---------------------------------------- | ----------------------------------- | ----------- |
| cpu_user_ate | CPU utilization | % | uInstanceId |
| memory_use_rate | Memory utilization | % | uInstanceId |
| memory_use | Memory usage | MB | uInstanceId |
| volume_rate | Disk utilization | % | uInstanceId |
| real_capacity | Used disk capacity (only includes data capacity usage) | MB | uInstanceId |
| capacity | Used disk capacity (includes data and log capacity usage) | MB | uInstanceId |
| bytes_sent | Private network outbound traffic | Bytes/second | uInstanceId |
| bytes_received | Private network inbound traffic | Bytes/second | uInstanceId |
| qps | Operations per second | Number of times/second | uInstanceId |
| tps | Transactions per second | Number of times/second | uInstanceId |
| max_connections | Maximum number of connections | Count | uInstanceId |
| threads_connected | Current connections | Count | uInstanceId |
| connection_use_rate | Connection utilization | % | uInstanceId |
| slow_queries | Slow queries | Number of times/minute | uInstanceId |
| select_scan | Full-table scans | Number of times/second | uInstanceId |
| select_count | Queries | Number of times/second | uInstanceId |
| com_update | Updates | Number of times/second | uInstanceId |
| com_delete | Deletions | Number of times/second | uInstanceId |
| com_insert | Insertions | Number of times/second | uInstanceId |
| com_replace | Overwrites | Number of times/second | uInstanceId |
| queries | Total requests | Number of times/second | uInstanceId |
| query_rate | Query utilization | % | uInstanceId |
| created_tmp_tables | Temporary tables | Number of times/second | uInstanceId |
| table_locks_waited | Table lock waits | Number of times/second | uInstanceId |
| innodb_cache_use_rate | InnoDB cache utilization | % | uInstanceId |
| innodb_cache_hit_rate | InnoDB cache hit rate | % | uInstanceId |
| innodb_os_file_reads | InnoDB disk reads | Number of times/second | uInstanceId |
| innodb_os_file_writes | InnoDB disk writes | Number of times/second | uInstanceId |
| innodb_os_fsyncs | InnoDB fsync count | Number of times/second | uInstanceId |
| innodb_num_open_files | Currently opened InnoDB tables | Count | uInstanceId |
| key_cache_use_rate | MyISAM cache utilization | % | uInstanceId |
| key_cache_hit_rate | MyISAM cache hit rate | % | uInstanceId |
| com_commit | Submissions | Number of times/second | uInstanceId |
| com_rollback | Rollbacks | Number of times/second | uInstanceId |
| threads_created | Threads created | Count | uInstanceId |
| threads_running | Running threads | Count | uInstanceId |
| created_tmp_disk_tables | Temporary disk tables | Number of times/second | uInstanceId |
| created_tmp_files | Temporary files | Number of times/second | uInstanceId |
| handler_read_rnd_next | Next-row read requests | Number of times/second | uInstanceId |
| handler_rollback | Internal rollbacks | Number of times/second | uInstanceId |
| handler_commit | Internal submissions | Number of times/second | uInstanceId |
| innodb_buffer_pool_pages_free | InnoDB empty pages | Count | uInstanceId |
| innodb_buffer_pool_pages_total | InnoDB total pages | Count | uInstanceId |
| innodb_buffer_pool_read_requests | InnoDB logical reads | Number of times/second | uInstanceId |
| innodb_buffer_pool_reads | InnoDB physical reads | Number of times/second | uInstanceId |
| innodb_data_reads | InnoDB total reads | Number of times/second | uInstanceId |
| innodb_data_read | InnoDB reads | Bytes/second | uInstanceId |
| innodb_data_writes | InnoDB total writes | Number of times/second | uInstanceId |
| innodb_data_written | InnoDB writes | Bytes/second | uInstanceId |
| innodb_rows_deleted | InnoDB row deletions | Number of times/second | uInstanceId |
| innodb_rowsinserted | InnoDB row insertions | Number of times/second | uInstanceId |
| innodb_rows_updated | InnoDB row updates | Number of times/second | uInstanceId |
| innodb_rows_read | InnoDB row reads | Number of times/second | uInstanceId |
| innodb_row_lock_time_avg | InnoDB average row lock acquisition time | Milliseconds | uInstanceId |
| innodb_row_lock_waits | InnoDB row lock waits | Number of times/second | uInstanceId |
| key_blocks_unused | Unused blocks in the key cache | Count | uInstanceId |
| key_blocks_used | Used blocks in the key cache | Count | uInstanceId |
| key_read_requests | Data block reads by the key cache | Number of times/second | uInstanceId |
| key_reads | Data block reads by disks | Number of times/second | uInstanceId |
| key_write_requests | Data block writes to the key cache | Number of times/second | uInstanceId |
| key_writes | Data block writes to disks | Number of times/second | uInstanceId |
| opened_tables | Opened tables | Count | uInstanceId |
| table_locksimmediate | Table locks released immediately | Count | uInstanceId |
| open_files | Total opened files | Count | uInstanceId |
| log_capacity | Log usage | MB | uInstanceId |
| slaveio_running | I/O thread status | Status values (0: Yes, 1: No, 2: Connecting) | uInstanceId |
| slavesql_running | SQL thread status | Status values (0: Yes, 1: No) | uInstanceId |
| master_slavesync_distance | Master-slave delay distance | MB | uInstanceId |
| seconds_behind_master | Master-slave delay time | Seconds | uInstanceId |


