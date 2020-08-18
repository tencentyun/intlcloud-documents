DBbrain allows you to customize the monitoring dashboard and link, compare, and view the monitoring data of multiple instances and metrics.
>?Currently, the monitoring dashboard feature is supported only for TencentDB for MySQL (excluding the Basic Edition).

![](https://main.qcloudimg.com/raw/99e78958c112d300aa91b28c2b1d2d40.png)

## Creating Dashboard
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Intelligent Monitoring** on the left sidebar, and select **Monitoring Dashboard** at the top.
2. Click **Create Dashboard**, enter the dashboard name, select the monitoring metrics for comparison, add an instance, and click **Save**.
![](https://main.qcloudimg.com/raw/6d589e9e2202620ff00a8bf7b14fcf26.png)

## Finding/Editing/Deleting Dashboard
Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Intelligent Monitoring** on the left sidebar, and select **Monitoring Dashboard** at the top.
- Click the dashboard name drop-down list to switch between different dashboards.
- After selecting a dashboard, click **Edit** to modify the monitoring metrics and instance of the current dashboard.
- Click **Delete** to delete the current dashboard.
![](https://main.qcloudimg.com/raw/63a8159d686610a9c3a134fac9265296.png)

## Enabling Chart Interaction
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Intelligent Monitoring** on the left sidebar, and select **Monitoring Dashboard** at the top.
2. Toggle on the "Chart Interaction" switch on the right to link and compare the monitoring views of multiple instances or metrics.
![](https://main.qcloudimg.com/raw/bc292ac34dea3fb835f5f8afea6fbbac.png)

## Switching Between Real-Time/Historical Views
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Intelligent Monitoring** on the left sidebar, and select **Monitoring Dashboard** at the top.
2. Click **Real-Time** or **Historical** to view the corresponding real-time or historical monitoring view.
 - The real-time monitoring view allows you to view the performance metric comparison of the instance over the last 3 minutes and is automatically refreshed by default. Click **Disable refresh** to stop refreshing the monitoring data.
![](https://main.qcloudimg.com/raw/1fbc5d902b3728ddcc3ce739602d08cc.png)
 - In the historical monitoring view, you can select a time period to display the view of monitoring dashboard over the selected time period, and you can switch among the last hour, last 3 hours, last 24 hours, last 7 days, and custom time period.
![](https://main.qcloudimg.com/raw/059c0fa80623570ce7ebdafb0e51e9c5.png)

## Monitoring Metrics
The custom monitoring dashboard in DBbrain currently supports the following 70 monitoring metrics.

| Monitoring Metric                         | Description                  |
| -------------------------------- | ------------------------- |
| cpu_use_rate                     | CPU                       |
| memory_use_rate                  | Memory                      |
| memory_use                       | Memory usage                  |
| volume_rate                      | Disk                      |
| real_capacity                    | Data space                  |
| capacity                         | Occupied disk space              |
| bytes_sent                       | Outbound traffic                  |
| bytes_received                   | Inbound traffic                  |
| qps                              | QPS                       |
| tps                              | TPS                       |
| connection_use_rate              | Connection utilization              |
| max_connections                  | Max connections                |
| threads_connected                | Connected threads        |
| slow_queries                     | Slow queries                  |
| select_scan                      | Full-table scans                |
| select_count                     | Queries                    |
| com_update                       | Updates                    |
| com_delete                       | Deletions                    |
| com_insert                       | Insertions                    |
| com_replace                      | Overwrites                    |
| queries                          | Total requests                  |
| query_rate                       | Query utilization                |
| created_tmp_tables               | Temp tables                |
| table_locks_waited               | Table locks awaited              |
| innodb_cache_hit_rate            | InnoDB cache hit rate        |
| innodb_cache_use_rate            | InnoDB cache utilization        |
| innodb_os_file_reads             | InnoDB disk reads        |
| innodb_os_file_writes            | InnoDB disk writes        |
| innodb_os_fsyncs                 | InnoDB fsync count         |
| innodb_num_open_files            | InnoDB opened tables |
| key_cache_hit_rate               | MyISAM cache hit rate        |
| key_cache_use_rate               | MyISAM cache utilization        |
| com_commit                       | Submissions                    |
| com_rollback                     | Rollbacks                    |
| threads_created                  | Created threads            |
| created_tmp_disk_tables          | Temp disk tables            |
| threads_running                  | Running threads          |
| created_tmp_files                | Temp files              |
| handler_read_rnd_next            | Requests of reading next row            |
| handler_rollback                 | Internal rollbacks                |
| handler_commit                   | Internal submissions                |
| innodb_buffer_pool_pages_free    | InnoDB empty pages            |
| innodb_buffer_pool_pages_total   | Total InnoDB pages            |
| innodb_buffer_pool_read_requests | InnoDB logical reads            |
| innodb_buffer_pool_reads         | InnoDB physical reads            |
| innodb_data_read                 | InnoDB reads            |
| innodb_data_reads                | Total InnoDB reads          |
| innodb_data_written              | InnoDB writes            |
| innodb_data_writes               | Total InnoDB writes          |
| innodb_rows_deleted              | InnoDB rows deleted          |
| innodb_rows_inserted             | InnoDB rows inserted          |
| innodb_rows_updated              | InnoDB rows updated          |
| innodb_rows_read                 | InnoDB rows read          |
| innodb_row_lock_time_avg         | Average InnoDB row lock acquiring time  |
| innodb_row_lock_waits            | InnoDB row lock waits      |
| key_blocks_unused                | Unused blocks in key cache    |
| key_blocks_used                  | Used blocks in key cache      |
| key_read_requests                | Data blocks read by key cache      |
| key_reads                        | Data blocks read by disks        |
| key_write_requests               | Data blocks written into key cache      |
| key_writes                       | Data blocks written into disks        |
| opened_tables                    | Opened tables            |
| table_locks_immediate            | Table locks released immediately          |
| open_files                       | Total opened files              |
| log_capacity                     | Log space                  |
| slave_io_running                 | IO thread status               |
| slave_sql_running                | SQL thread status              |
| master_slave_sync_distance       | Source-replica delay distance             |
| seconds_behind_master            | Source-replica delay time              |
