DBbrain allows you to customize the monitoring dashboard and link, compare, and view the monitoring data of multiple instances and metrics.
>?Currently, the monitoring dashboard is supported only for TencentDB for MySQL (excluding the basic single-node instance).

![](https://main.qcloudimg.com/raw/99e78958c112d300aa91b28c2b1d2d40.png)

## Creating a Dashboard
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis), select **Monitoring & Alarm** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database type at the top and select the **Monitoring Dashboard** tab.
2. Click **Create Dashboard**, enter the dashboard name, select the monitoring metrics for comparison, add an instance, and click **Save**.
![](https://main.qcloudimg.com/raw/6d589e9e2202620ff00a8bf7b14fcf26.png)

## Finding/Editing/Deleting a Dashboard
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis), select **Monitoring & Alarm** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database type at the top and select the **Monitoring Dashboard** tab.
- Click the dashboard name drop-down list to switch between different monitoring dashboards.
- After selecting a dashboard, click **Edit** to modify the monitoring metrics and instance of the current dashboard.
- Click **Delete** to delete the current dashboard.
![](https://main.qcloudimg.com/raw/63a8159d686610a9c3a134fac9265296.png)

## Enabling Chart Interaction
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis), select **Monitoring & Alarm** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database type at the top and select the **Monitoring Dashboard** tab.
2. Toggle on the **Chart Interaction** switch on the right to link and compare the monitoring views of multiple instances or metrics.
![](https://main.qcloudimg.com/raw/bc292ac34dea3fb835f5f8afea6fbbac.png)

## Switching Between Real-Time/Historical Views
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis), select **Monitoring & Alarm** > **Intelligent Monitoring** on the left sidebar. On the displayed page, select a database type at the top and select the **Monitoring Dashboard** tab.
2. Click **Real-Time** or **Historical** to view the corresponding real-time or historical monitoring view.
 - The real-time monitoring view allows you to view the performance metric comparison of the instance over the last 3 minutes and is automatically refreshed by default. Click **Disable refresh** to stop refreshing the monitoring data.
![](https://main.qcloudimg.com/raw/1fbc5d902b3728ddcc3ce739602d08cc.png)
 - In the historical monitoring view, you can select a time period to display the view of monitoring dashboard over the selected time period, and you can switch among the last hour, last 3 hours, last 24 hours, last 7 days, and custom time period.
![](https://main.qcloudimg.com/raw/059c0fa80623570ce7ebdafb0e51e9c5.png)

## Monitored Metrics
### DBbrain (TencentDB for MySQL)
In DBbrain, the custom monitoring dashboard for TencentDB for MySQL currently supports the following monitoring metrics.

| Monitoring Metric | Description |
| -------------------------------- | ------------------------- |
| cpu_use_rate | CPU utilization |
| memory_use_rate | Memory utilization |
| memory_use | Memory usage |
| volume_rate | Disk utilization |
| real_capacity | Disk usage |
| capacity | Total disk capacity |
| bytes_sent | Outbound traffic |
| bytes_received | Inbound traffic |
| qps | QPS |
| tps | TPS |
| connection_use_rate | Connection utilization |
| max_connections | The maximum number of connections |
| threads_connected | Connected threads |
| slow_queries | The number of slow queries |
| select_scan | The number of full-table scans |
| select_count | The number of queries |
| com_update | The number of updates |
| com_delete | The number of deletions |
| com_insert | The number of insertions |
| com_replace | The number of overwrites |
| queries | The number of total requests |
| query_rate | Query utilization |
| created_tmp_tables | The number of temp tables |
| table_locks_waited | The number of table lock waits |
| innodb_cache_hit_rate | InnoDB cache hit rate |
| innodb_cache_use_rate | InnoDB cache utilization |
| innodb_os_file_reads | The number of InnoDB disk reads |
| innodb_os_file_writes | The number of InnoDB disk writes |
| innodb_os_fsyncs | The number of InnoDB fsync operations |
| innodb_num_open_files | The number of tables InnoDB currently holds open |
| key_cache_hit_rate | MyISAM cache hit rate |
| key_cache_use_rate | MyISAM cache utilization |
| com_commit | The number of commits |
| com_rollback | The number of rollbacks |
| threads_created | The number of created threads |
| created_tmp_disk_tables | The number of temp tables created on the disk |
| threads_running | Running threads |
| created_tmp_files | The number of temp files |
| handler_read_rnd_next | The number of requests to read the next row |
| handler_rollback | The number of internal rollbacks |
| handler_commit | The number of internal commits |
| innodb_buffer_pool_pages_free | The number of empty pages in InnoDB |
| innodb_buffer_pool_pages_total | The total number of pages in InnoDB |
| innodb_buffer_pool_read_requests | The number of InnoDB logical reads |
| innodb_buffer_pool_reads | The number of InnoDB physical reads |
| innodb_data_read | The number of InnoDB reads |
| innodb_data_reads | The total number of InnoDB reads |
| innodb_data_written | The number of InnoDB writes |
| innodb_data_writes | The total number of InnoDB writes |
| innodb_rows_deleted | The number of InnoDB row deletions |
| innodb_rows_inserted | The number of InnoDB row insertions |
| innodb_rows_updated | The number of InnoDB row updates |
| innodb_rows_read | The number of InnoDB row reads |
| innodb_row_lock_time_avg | InnoDB average row lock acquisition time |
| innodb_row_lock_waits | The number of InnoDB row lock waits |
| key_blocks_unused | The number of unused blocks in key cache |
| key_blocks_used | The number of used blocks in key cache |
| key_read_requests | The number of block reads of key cache |
| key_reads | The number of block reads of the disk |
| key_write_requests | The number of block writes to the key cache |
| key_writes | The number of block writes to the disk |
| opened_tables | The number of opened tables |
| table_locks_immediate | The number of table locks released immediately |
| open_files | Total number of opened files |
| log_capacity | Log space |
| slave_io_running | IO thread status |
| slave_sql_running | SQL thread status |
| master_slave_sync_distance | Master-slave delay distance |
| seconds_behind_master | Master-slave delay time |

