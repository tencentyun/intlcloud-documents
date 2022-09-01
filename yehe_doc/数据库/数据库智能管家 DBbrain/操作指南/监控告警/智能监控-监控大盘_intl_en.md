## Feature Description

DBbrain allows you to customize the monitoring dashboard and link, compare, and view the monitoring data of multiple instances and metrics.

>?Currently, the monitoring dashboard feature is supported for TencentDB for MySQL (excluding basic single-node instances), TDSQL-C for MySQL, self-built MySQL, TencentDB for Redis, and TencentDB for MongoDB.

![](https://main.qcloudimg.com/raw/99e78958c112d300aa91b28c2b1d2d40.png)

## Creating a Dashboard
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Monitoring and Alarming** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Monitoring Dashboard** tab.
2. Click **Create Dashboard**, enter the dashboard name, select the monitoring metrics for comparison, add an instance, and click **Save**.
   ![](https://main.qcloudimg.com/raw/6d589e9e2202620ff00a8bf7b14fcf26.png)

## Finding/Editing/Deleting a Dashboard
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Monitoring and Alarming** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Monitoring Dashboard** tab.

- Click the dashboard name drop-down list to switch between different monitoring dashboards.
- After selecting a dashboard, click **Edit** to modify its monitoring metrics and instance.
- Click **Delete** to delete the current dashboard.
  ![](https://main.qcloudimg.com/raw/63a8159d686610a9c3a134fac9265296.png)

## Viewing Dashboard Details

### Enabling chart interaction
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Monitoring and Alarming** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Monitoring Dashboard** tab.
2. Toggle on **Chart Interaction** on the right to link and compare the monitoring views of multiple instances or metrics.
   When you hover over a data point in any monitoring view, the data at the same time point will be displayed in other monitoring views. Click the data point to pin it for display. To unpin it, click **Deselect the Time Point**.
   ![](https://main.qcloudimg.com/raw/bc292ac34dea3fb835f5f8afea6fbbac.png)

### Switching between one-column and two-column modes
1. Click the button on the right of **Chart Interaction** in the top-right corner to switch.
2. Click the border of a monitoring view to drag it to the desired position.

### Switching between real-time and historical views
Click **Real-Time** or **Historical** to view the real-time or historical monitoring view.
- The real-time monitoring view displays the performance metric comparison of the instance in the last three minutes and is automatically refreshed by default. You can click **Disable refresh** to stop refreshing the monitoring data in real time.
  ![](https://main.qcloudimg.com/raw/1fbc5d902b3728ddcc3ce739602d08cc.png)
- In the historical monitoring view, you can select a time range (**Last hour**, **Last 3 hours**, **Last 24 hours**, **Last 7 days**, or a custom time range) to display the monitoring dashboard in the selected time range.
  ![](https://main.qcloudimg.com/raw/059c0fa80623570ce7ebdafb0e51e9c5.png)

## Monitoring Metrics

### DBbrain (TencentDB for MySQL)

In DBbrain, the custom monitoring dashboard for TencentDB for MySQL currently supports the following monitoring metrics:

| Monitoring Metric | Description |
| -------------------------------- | ------------------------- |
| cpu_use_rate                     | CPU Utilization                       |
| memory_use_rate                  | Memory Utilization                      |
| memory_use                       | Memory Usage                  |
| volume_rate                      | Disk Utilization                |
| real_capacity                    | Used Disk Space              |
| capacity                         | Occupied Disk Space              |
| bytes_sent                       | Outbound Traffic                  |
| bytes_received                   | Inbound Traffic                  |
| qps                              | QPS                       |
| tps                              | TPS                       |
| connection_use_rate              | Connection Utilization              |
| max_connections                  | Max Connections                |
| threads_connected                | Connected Threads        |
| slow_queries                     | Slow Queries                  |
| select_scan                      | Full-Table Scans                |
| select_count                     | Queries                   |
| com_update                       | Updates                    |
| com_delete                       | Deletions                    |
| com_insert                       | Insertions                    |
| com_replace                      | Overwrites                    |
| queries                          | Total Requests                  |
| query_rate                       | Query Utilization                |
| created_tmp_tables               | Temp Tables                |
| table_locks_waited               | Table Locks Awaited              |
| innodb_cache_hit_rate            | InnoDB Cache Hit Rate        |
| innodb_cache_use_rate            | InnoDB Cache Utilization        |
| innodb_os_file_reads             | InnoDB Disk Reads        |
| innodb_os_file_writes            | InnoDB Disk Writes        |
| innodb_os_fsyncs                 | InnoDB fsync Count         |
| innodb_num_open_files            | InnoDB Opened Tables |
| key_cache_hit_rate               | MyISAM Cache Hit Rate        |
| key_cache_use_rate               | MyISAM Cache Utilization        |
| com_commit                       | Submissions                    |
| com_rollback                     | Rollbacks                    |
| threads_created                  | Created Threads            |
| created_tmp_disk_tables          | Temp Disk Tables            |
| threads_running                  | Running Threads          |
| created_tmp_files                | Temp Files              |
| handler_read_rnd_next            | Requests of Reading Next Row            |
| handler_rollback                 | Internal Rollbacks                |
| handler_commit                   | Internal Submissions                |
| innodb_buffer_pool_pages_free    | InnoDB Empty Pages           |
| innodb_buffer_pool_pages_total   |  Total InnoDB Pages       |
| innodb_buffer_pool_read_requests | InnoDB Logical Reads   |
| innodb_buffer_pool_reads         | InnoDB Physical Reads            |
| innodb_data_read                 | InnoDB Reads            |
| innodb_data_reads                | Total InnoDB Reads          |
| innodb_data_written              | InnoDB Writes            |
| innodb_data_writes               | Total InnoDB Writes          |
| innodb_rows_deleted              | InnoDB Rows Deleted          |
| innodb_rows_inserted             |  InnoDB Rows Inserted          |
| innodb_rows_updated              | InnoDB Rows Updated         |
| innodb_rows_read                 | InnoDB Rows Read          |
| innodb_row_lock_time_avg         | Average InnoDB Row Lock Acquiring Time  |
| innodb_row_lock_waits            | InnoDB Row Lock Waits      |
| key_blocks_unused                | Unused Blocks in Key Cache    |
| key_blocks_used                  | Used Blocks in Key Cache      |
| key_read_requests                | Data Blocks Read by Key Cache      |
| key_reads                        | Data Blocks Read by Disks        |
| key_write_requests               | Data Blocks Written into Key Cache      |
| key_writes                       | Data Blocks Written into Disks        |
| opened_tables                    | Opened Tables            |
| table_locks_immediate            | Table Locks Released Immediately          |
| open_files                       | Total Opened Files              |
| log_capacity                     | Log Space                  |
| slave_io_running                 | IO Thread Status               |
| slave_sql_running                | SQL Thread Status              |
| master_slave_sync_distance       | Source-Replica Delay Distance              |
| seconds_behind_master            | Source-Replica Delay Time              |

### DBbrain (TDSQL-C for MySQL)

In DBbrain, the custom monitoring dashboard for TDSQL-C for MySQL currently supports the following monitoring metrics.

| Monitoring Metric | Description |
| --------------------------------- | ------------------------------- |
| cpu_use_rate                     | CPU Utilization                       |
| memory_use_rate                  | Memory Utilization                      |
| memory_use                       | Memory Usage                  |
| volume_rate                       | Storage Utilization                      |
| real_capacity                     | Used Storage Space                    |
| qcache_hits                       | Cache Hits                      |
| qcache_hit_rate                   | Cache Hit Rate                      |
| capacity                          | Total Storage Space                    |
| bytes_sent                       | Outbound Traffic                  |
| bytes_received                   | Inbound Traffic                  |
| queries                           | QPS                             |
| com_commit                        | TPS                             |
| max_connections                  | Max Connections                |
| threads_connected                | Connected Threads        |
| slow_queries                     | Slow Queries                  |
| select_scan                      | Full-Table Scans                |
| select_count                     | Queries                   |
| com_update                       | Updates                    |
| com_delete                       | Deletions                    |
| com_insert                       | Insertions                    |
| com_replace                      | Overwrites                    |
| created_tmp_tables               | Temp Tables                |
| innodb_cache_hit_rate            | InnoDB Cache Hit Rate        |
| innodb_cache_use_rate            | InnoDB Cache Utilization        |
| threads_created                  | Created Threads            |
| threads_running                  | Running Threads          |
| handler_rollback                  | Rolled-Back Transactions per Second             |
| innodb_buffer_pool_read_requests | InnoDB Logical Reads   |
| handler_commit                    | Committed Transactions per Second              |
| innodb_buffer_pool_write_requests | InnoDB Logic Write                   |
| innodb_rows_deleted              | InnoDB Rows Deleted          |
| innodb_rows_updated              | InnoDB Rows Updated         |
| innodb_rows_inserted             |  InnoDB Rows Inserted          |
| innodb_rows_read                 | InnoDB Rows Read          |
| log_capacity                     | Log Space                  |
| replicate_lag                     | Replica Instance Delay in Redo Log Based Replication            |
| replicate_lsn_lag                 | Redo Log LSN Difference between Source and Replica Instances |
| replicate_status                  | Replication Status of Replica Instance                |

### DBbrain (TencentDB for Redis)

In DBbrain, the custom monitoring dashboard for TencentDB for Redis currently supports the following monitoring metrics:

| Monitoring Metric | Description |
| -------------------- | ------------------- |
| cmd_big_value        | Big Value Request       |
| cmd_err              | Execution Error            |
| cmd_hits             | Read Request Hit          |
| cmd_hits_ratio       | Read Request Hit Rate        |
| %cmd_key_count       | Key Requests          |
| cmd_mget             | Mget Requests         |
| cmd_miss             | Read Request Miss         |
| cmd_other            | Other Requests            |
| cmd_read             | Read Request              |
| cmd_slow             | Slow Query              |
| cmd_write            | Write Request              |
| commands             | Total Requests              |
| connections          | Connections              |
| connections_util     | Connection Utilization          |
| %cpu_max_util        | Max Node CPU Utilization |
| %cpu_util            | CPU Utilization          |
| %evicted             | Evicted Keys          |
| expired              | Expired Keys          |
| in_bandwidth_util    | Inbound Traffic Utilization        |
| %in_flow             |  Inbound Traffic              |
| MBit/sin_flow_limit  |  Inbound Traffic Throttling Trigger      |
| keys                 | Total Keys          |
| latency_max          | Max Execution Latency        |
| mslatency_other      | Avg Latency of Other Commands    |
| mslatency_avg        |  Avg Execution Latency        |
| mslatency_read       | Avg Read Latency          |
| mslatency_write      | Avg Write Latency          |
| msmem_max_util       | Max Node MEM Utilization  |
| %mem_used            | Memory Usage          |
| MBmem_util           | Memory Utilization         |
| %out_bandwidth_util  | Outbound Traffic Utilization        |
| %out_flow            | Outbound Traffic             |
| MBit/sout_flow_limit | Outbound Traffic Throttling Trigger      |
| latency_p99          | P99 Execution Latency       |


### DBbrain (self-built MySQL)

In DBbrain, the custom monitoring dashboard for self-built MySQL currently supports the following monitoring metrics:

| Monitoring Metric | Description | Agent Access | Direct Access |
| -------------------------------- | ------------------------- | ---------- | -------- |
| cpu_use_rate                     | CPU Utilization                       | &#10003;   | ×        |
| memory_use_rate                  | Memory Utilization                      | &#10003;   | ×        |
| memory_use                       | Memory Usage                  | &#10003;   | ×        |
| volume_rate                      | Disk Utilization                | &#10003;   | ×        |
| real_capacity                    | Used Disk Space              | &#10003;   | ×        |
| capacity                         |  Occupied Disk Space              | &#10003;   | ×        |
| bytes_sent                       | Outbound Traffic                  | &#10003;   | &#10003; |
| bytes_received                   | Inbound Traffic                  | &#10003;   | &#10003; |
| qps                              | QPS                       | &#10003;   | &#10003; |
| tps                              | TPS                       | &#10003;   | &#10003; |
| connection_use_rate              | Connection Utilization              | &#10003;   | &#10003; |
| max_connections                  | Max Connections                | &#10003;   | &#10003; |
| threads_connected                | Connected Threads        | &#10003;   | &#10003; |
| slow_queries                     | Slow Queries                  | &#10003;   | &#10003; |
| select_scan                      | Full-Table Scans                | &#10003;   | &#10003; |
| select_count                     |  Queries                    | &#10003;   | &#10003; |
| com_update                       | Updates                 | &#10003;   | &#10003; |
| com_delete                       | Deletions                  | &#10003;   | &#10003; |
| com_insert                       | Insertions                | &#10003;   | &#10003; |
| com_replace                      |  Overwrites                    | &#10003;   | &#10003; |
| queries                          | Total Requests                | &#10003;   | &#10003; |
| query_rate                       | Query Utilization                | &#10003;   | &#10003; |
| created_tmp_tables               | Temp Tables                | &#10003;   | &#10003; |
| table_locks_waited               | Table Locks Awaited              | &#10003;   | &#10003; |
| innodb_cache_hit_rate            | InnoDB Cache Hit Rate        | &#10003;   | &#10003; |
| innodb_cache_use_rate            |  InnoDB Cache Utilization        | &#10003;   | &#10003; |
| innodb_os_file_reads             | InnoDB Disk Reads        | &#10003;   | &#10003; |
| innodb_os_file_writes            | InnoDB Disk Writes        | &#10003;   | &#10003; |
| innodb_os_fsyncs                 | InnoDB fsync Count         | &#10003;   | &#10003; |
| innodb_num_open_files            |  InnoDB Opened Tables | &#10003;   | &#10003; |
| key_cache_hit_rate               | MyISAM Cache Hit Rate        | &#10003;   | &#10003; |
| key_cache_use_rate               |  MyISAM Cache Utilization      | &#10003;   | &#10003; |
| com_commit                       |  Submissions                    | &#10003;   | &#10003; |
| com_rollback                     | Rollbacks                   | &#10003;   | &#10003; |
| threads_created                  |  Created Threads            | &#10003;   | &#10003; |
| created_tmp_disk_tables          | Temp Disk Tables            | &#10003;   | &#10003; |
| threads_running                  | Running  Threads          | &#10003;   | &#10003; |
| created_tmp_files                | Temp Files             | &#10003;   | &#10003; |
| handler_read_rnd_next            | Requests of Reading Next Row            | &#10003;   | &#10003; |
| handler_rollback                 | Internal Rollbacks                | &#10003;   | &#10003; |
| handler_commit                   |  Internal Submissions                | &#10003;   | &#10003; |
| innodb_buffer_pool_pages_free    | InnoDB Empty Pages           | &#10003;   | &#10003; |
| innodb_buffer_pool_pages_total   | Total InnoDB Pages          | &#10003;   | &#10003; |
| innodb_buffer_pool_read_requests |  InnoDB Logical Reads            | &#10003;   | &#10003; |
| innodb_buffer_pool_reads         | InnoDB Physical Reads            | &#10003;   | &#10003; |
| innodb_data_read                 | InnoDB Reads            | &#10003;   | &#10003; |
| innodb_data_reads                |  Total InnoDB Reads          | &#10003;   | &#10003; |
| innodb_data_written              |  InnoDB Writes          | &#10003;   | &#10003; |
| innodb_data_writes               | Total InnoDB Writes          | &#10003;   | &#10003; |
| innodb_rows_deleted              |  InnoDB Rows Deleted          | &#10003;   | &#10003; |
| innodb_rows_inserted             |  InnoDB Rows Inserted          | &#10003;   | &#10003; |
| innodb_rows_updated              |  InnoDB Rows Updated         | &#10003;   | &#10003; |
| innodb_rows_read                 | InnoDB Rows Read          | &#10003;   | &#10003; |
| innodb_row_lock_time_avg         | Average InnoDB Row Lock Acquiring Time  | &#10003;   | &#10003; |
| innodb_row_lock_waits            |  InnoDB Row Lock Waits      | &#10003;   | &#10003; |
| key_blocks_unused                |  Unused Blocks in Key Cache    | &#10003;   | &#10003; |
| key_blocks_used                  | Used Blocks in Key Cache     | &#10003;   | &#10003; |
| key_read_requests                | Data Blocks Read by Key Cache     | &#10003;   | &#10003; |
| key_reads                        | Data Blocks Read by Disks        | &#10003;   | &#10003; |
| key_write_requests               |  Data Blocks Written into Key Cache      | &#10003;   | &#10003; |
| key_writes                       | Data Blocks Written into Disks        | &#10003;   | &#10003; |
| opened_tables                    |  Opened Tables           | &#10003;   | &#10003; |
| table_locks_immediate            | Table Locks Released Immediately          | &#10003;   | &#10003; |
| open_files                       | Total Opened Files              | &#10003;   | &#10003; |
| log_capacity                     | Log Space                  | &#10003;   | ×        |

