
## Console monitoring

To make it easy for users to view and grasp the running information of the instance, cloud database PostgreSQL provides a wealth of performance monitoring items, and users can log in [PostgreSQL console](https://console.cloud.tencent.com/pgsql) To view it in the **system Monitoring** tab of the corresponding instance management page.

## Monitoring Metrics

|Metric's Chinese name|Metric's English name|Metric's meaning|Metric unit|
|-|-|-|-|
|CPU Utilization|Cpu|Instance CPU utilization. Due to the flexible CPU restriction policy adopted in idle time, the CPU utilization may be greater than 100%.|%|
|Used Storage|Storage|The instance occupies the available space of the disk|GB|
|Disk IOPS|Iops|IOPS of the instance (number of requests per second)|times/sec|
|Inbound Traffic|In_flow|Traffic inputted by reading and writing of an example|KB/ seconds|
|Outbound Traffic|Out_flow|Traffic of example read-write output|KB/ seconds|
|Connections|Connections|Historical trend of active connections of instances|__item(s)|
|Requests|Read_write_calls|Total number of read and write (CRUD) requests per minute|/min|
|Number of read requests|Read_calls|Total number of read requests per minute|/min|
|Write Requests|Write_calls|Total number of write requests per minute|/min|
|Number of other requests|Other_calls|Total number of requests except read and write (for example, Drop), accumulates by minute|/min|
|Buffer Cache Hit Rate|Hit_percent|Data cache hit ratio|%|
|Average Execution Latency|Sql_runtime_avg|Average execution time of all SQL requests, excluding SQL in the transaction|ms|
|Longest TOP10 executive Latency|Sql_runtime_avg|Average SQL of the TOP10 with the longest execution time|ms|
|The shortest TOP10 executive Latency|Sql_runtime_min|The average SQL of the TOP10 with the shortest execution time|ms|
|Number of remaining XID|Remain_xid|Number of remaining Transaction IDs. There are a maximum of 2 ^ 32 Transaction Ids. It is recommended to execute "vacuum full" manually if the number falls below 1000000|__item(s)|
|Synchronization difference between master/slave XLOG|Xlog_diff|(Sample is taken every minute) The synchronization difference between the master XLOG and the slave XLOG. This represents synchronization delay, and lower is better|byte|

## Pg_stat_statements View 

 You can also use the [Pg_stat_statements](https://www.postgresql.org/docs/9.4/pgstatstatements.html) View query pg detailed performance Metric. The pg_stat_statements module provides a method to track the execution statistics of all SQL statements executed by a server, which can be used to count the resource cost of the database and analyze TOP SQL.

```
select * from pg_stat_statements；
```
