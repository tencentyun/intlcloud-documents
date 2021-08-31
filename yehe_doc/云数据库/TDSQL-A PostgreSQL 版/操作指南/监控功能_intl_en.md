This document describes how to view and export the monitoring data of a TDSQL-A for PostgreSQL instance in the console.

## Viewing Monitoring Data
1. Log in to the [TDSQL-A for PostgreSQL](https://console.cloud.tencent.com/tdsqla/tdapg) console and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **System Management** tab and select a time to view the monitoring data and load.
![](https://main.qcloudimg.com/raw/5cac2c87a258388ccee34671fabf63e9.png)
  - On the **System Management** tab, click **Restart Node** and select GTM, CN, or DN nodes.
>!Node restart is a high-risk operation that makes the instance unavailable. Please evaluate its impact on your business before proceeding.
>
![](https://main.qcloudimg.com/raw/eb4a503acae02d5402863e2968c96059.png)
  - View alarming and monitoring data at different time granularities. For example, you can click **Last 24 hours** to view the monitoring data for the last 24 hours.
![](https://main.qcloudimg.com/raw/0d8d92034b28ae05f0e34a19ae3625a0.png)
  - Click **Export Data** on the right and select the monitoring data to be exported.
![](https://main.qcloudimg.com/raw/497991ba14059266519f13368b3ea9b2.png)

## Monitoring Metrics
Cloud Monitor provides the following monitoring metrics for TDSQL-A for PostgreSQL instances in the instance dimension:

| **Metric** | **Parameter** | **Unit** | **Description** |
| -------------------- | --------------------- | -------- | ------------------------------------------------------------ |
| CPU Utilization | cpu_used_pct | % | Maximum value of CPU utilization of CN, DN, and GTM of the instance |
| Memory Utilization | mem_used_pct | % | Maximum value of memory utilization of CN, DN, and GTM of the instance |
| IO Throughput | iops | Counts/s | Throughput of primary and standby CN and DN disks of the instance |
| Cache Hit Rate | cache_hit_pct | % | Data cache hit rate |
| Connections | connections | - | Number of active connections of the instance |
| Average of Top 10 Shortest SQL Execution Time | sql_runtime_min | ms | Average value of the top 10 SQL statements with the shortest execution time |
| Average of Top 10 Longest SQL Execution Time | sql_runtime_max | ms | Average value of the top 10 SQL statements with the longest execution time |
| Average SQL Execution Time | sql_runtime_avg | ms | Average execution time of all SQL requests, excluding requests in transactions |
| Total Requests | total_requests | - | Sum of requests of all primary and standby CN and DN nodes per minute |
| User Requests | user_requests | - | Sum of business requests of all primary and standby CN and DN nodes per minute (excluding system requests) |
| Read Requests | read_requests | - | Total number of read requests per minute |
| UPDATE Requests | update_requests | - | Total number of update requests per minute |
| INSERT Requests | insert_requests | - | Total number of insertion requests per minute |
| DELETE Requests | delete_requests | - | Total number of deletion requests per minute |
| Write Requests | write_requests | - | Total number of write requests per minute |
| Other Requests | other_requests | - | Total number of requests other than reads and writes per minute |
| Failed Requests | error_requests | - | Sum of all failed requests recorded in the instance per minute |
| Prepared Transactions for Two-Phase Commit | two_phase_commit_trxs | - | Sum of transactions prepared 10 minutes ago of all primary and standby CN and DN nodes in the instance |
| Capacity Utilization | capacity_used_pct | % | Capacity utilization of the instance |
| Capacity Usage | capacity_usage | GBytes | Used capacity of the instance |
| Remaining XIDs | xid_remain | - | Minimum value of the remaining XIDs on all CNs and DNs of the instance |
| XLog Sync Lag Between Primary and Standby | xlog_diff | Bytes | Primary-Standby XLog sync delay. The smaller, the better |
| Primary-Standby Switches | master_switch | - | Sum of switches of all primary and standby nodes in the instance per minute |


