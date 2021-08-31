To make it easier for you to view and stay up to date with how instances work, TencentDB for SQL Server provides a wide variety of performance monitoring metrics and convenient monitoring features (custom view, time comparison, merged monitoring metrics, etc).
>?If the number of tables in a single instance exceeds one million, database monitoring may be affected. Please make sure that the number of tables in a single instance is below one million.
  
## Types of Instances for Monitoring
TencentDB for SQL Server primary and read-only instances can be monitored, and each instance is provided with a separate monitoring view for easy query.

## Viewing Monitoring Information
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. Select the **System Monitoring** tab to view the monitoring information of each metric of the instance.
>?
>- TencentDB for SQL Server monitoring supports a granularity of down to 10 seconds.
>- Currently, you can view monitoring data of TencentDB for SQL Server in the last 180 days.

## Monitoring Metrics
The system monitoring of TencentDB for SQL Server supports 25 common metrics of SQL Server. You can collect statistics of other metrics by configuring the performance counters of SQL Server Management Studio (SSMS).

### [Common metrics](id:changjian_canshu)
| Metric | Description (Unit) | Value |
|:----:|----|:-----:|
| Total Processor Time | Actual CPU utilization (%) | max | 
| Transactions/sec | Average transactions per second (counts/second) | max |
| User Connections | Average user connections to the database per second (-) | max |
| Batch Requests/sec | Average requests per second (counts/second) | max |
| Logins/sec | Number of logins per second (counts/second) | max |
| Logouts/sec | Number of logouts per second (counts/second) | max |
| Used Storage Space<br>(Storage Space) | Sum of space occupied by instance database files and log files (GB) | max | 
| Inbound Traffic<br>(Network Receive Throughput) | Sum of all inbound packets of all connections (MB/s) | max |
| Outbound Traffic<br>(Network Transmit Throughput) | Sum of all outbound packets of all connections (MB/s) | max |
| Disk IOPS<br>(IPOS) | Disk reads/writes (counts/second) | max |
| Disk Reads<br>(Read IOPS) | Disk reads per second (counts/second) | max |
| Disk Writes<br>(Write IOPS) | Disk writes per second (counts/second) | max |
| Memory Usage | Used memory capacity (MB) | max |
| Free Storage | Percentage of the remaining free storage (%). Calculation formula: (Purchased storage - Used storage) / Purchased storage x 100% | max | 
  
### Performance optimization metrics

| Metric | Description (Unit) | Value |
|:----:|----|:-----:|
| Slow Queries<br>(SlowQuery) | Number of queries running for more than one second (-) | avg | 
| Processes Blocked | Number of currently blocked processes (-) | avg |
| Lock Requests/sec | Average lock requests per second (counts/second) | avg |
| User Errors<br>(User Error/sec) | Average errors per second (counts/second) | avg |
| Lock Waits | Lock requests requiring the caller to wait per second (counts/second) | avg |
| SQL Compilations/sec | Average SQL compilations per second (counts/second) | avg |
| SQL Re-Compilations/sec | Average SQL recompilations per second (counts/second) | avg |
| Inbound Traffic<br>(Network Receive Throughput) | Sum of all inbound packets of all connections (MB/s) | avg |
| Outbound Traffic<br>(Network Transmit Throughput) | Sum of all outbound packets of all connections (MB/s) | avg |
| Full Scans/sec | Number of full scans per second (counts/second) | avg |
| Buffer Cache Hit Ratio | Data cache (memory) hit ratio (%) | avg |
| Latch Waits/sec | Number of latch requests that could not be granted immediately (counts/sec) | avg |
| Average Wait Time | Average amount of wait time for each lock request that resulted in a wait (ms) | max |
| Network IO Waits | Average network IO delay time (ms) | max |
| Plan Cache: Cache Hit Ratio | Hit ratio of the execution plan of each SQL (%) | max |

