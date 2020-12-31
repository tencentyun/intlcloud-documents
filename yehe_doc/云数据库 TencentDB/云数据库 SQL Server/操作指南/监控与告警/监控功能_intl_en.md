To make it easier for you to view and stay up to date with how instances work, TencentDB for SQL Server provides a wide variety of performance monitoring metrics and convenient monitoring features (custom view, time comparison, merged monitoring metrics, etc).
>?If the number of tables in a single instance exceeds one million, database monitoring may be affected. Please make sure the number of tables in a single instance is no more than one million.
  
## Supported Instance Types
TencentDB for SQL Server primary instances and read-only replicas can be monitored, and each instance is provided with a separate monitoring view for easy query.


## Viewing Monitoring Information
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance name/ID or **Manage** in the **Operation** column to enter the instance management page.
2. Select the **System Monitoring** tab to view the monitoring information of each metric of the instance.
>?
>- TencentDB for SQL Server monitoring supports a granularity of down to 10 seconds.
>- Currently, you can view monitoring data of TencentDB for SQL Server in the last 180 days.


## Monitoring Metrics
The system monitoring of TencentDB for SQL Server supports 25 common metrics of SQL Server. You can collect statistics of other metrics by configuring the performance counters of SQL Server Management Studio (SSMS).

<span id = "changjian_canshu"></span>
### Common metrics
| Metric | Description (Unit) | Value | Optimization Suggestion |
|:----:|----|:-----:|--------|
| CPU utilization <br>(Total Processor Time) | Actual CPU utilization (%) | max | < 30% Good <br>< 60% Normal <br>> 60% Attention required |
| Number of transactions <br>(Transaction/sec) | Average transactions per second (times/second) | max | Dependent on business needs |
| Number of connections <br>(User Connection) | Average user connections to the database per second (-) | max | Dependent on business needs |
| Number of requests <br>(Batch Requests/sec) | Average requests per second (times/second) | max | Dependent on business needs |
| Number of logins per second <br>(Logins/sec) | Logins per second (times/second) | max | Dependent on business needs |
| Number of logouts per second <br>(Logouts/sec) | Logouts per second (times/second) | max | Dependent on business needs |
| Used storage space <br>(Storage Space) | Sum of space occupied by instance data files and log files (GB) | max | < 30% Good <br>< 60% Normal <br>> 60% Attention required |
| Inbound network traffic <br>(Network Receive Throughput) | Sum of all inbound packets of all connections (MB/s) | max | Dependent on business needs |
| Outbound network traffic <br>(Network Transmit Throughput) | Sum of all outbound packets of all connections (MB/s) | max | Dependent on business needs |
| Disk IOPS <br>(IPOS) | Disk reads/writes (times/second) | max | < 30% Good <br>< 60% Normal <br>> 60% Attention required |
| Number of disk reads <br>(Read IOPS) | Disk reads per second (times/second) | max | Dependent on business needs |
| Number of disk writes <br>(Write IOPS) | Disk writes per second (times/second) | max | Dependent on business needs |
| Memory Usage | Used memory capacity (MB) |max| Dependent on business needs |
| Remaining storage capacity | Sum of remaining capacity of instance data files and log files (GB) | max | < 30% Good <br>< 60% Normal <br>> 60% Attention required |

  
### Performance optimization metrics

| Metric | Description (Unit) | Value | Optimization Suggestion |
|:----:|----|:-----:|--------|
| Slow queries <br>(SlowQuery) | Number of queries running for more than one second (-) | avg | < 1 Good <br>< 10 Normal <br>> 10 Attention required |
| Blocking processes <br>(Processes blocked) | Current number of blocking processes (-) | avg | Dependent on business needs |
| Number of lock requests <br>(Lock Requests/sec) | Average lock requests per second (times/second) | avg | Dependent on business needs|
| Number of user errors <br>(User Error/sec) | Average errors per second (times/second) | avg | 0 Good <br>> 0 Attention required |
| Number of lock waits <br>(Lock waits) | Lock requests requiring caller to wait per second (times/second) | avg | Dependent on business needs |
| Number of SQL compilations <br>(SQL Compilation/sec) | Average SQL compilations per second (times/second) | avg | Dependent on business needs |
| Number of SQL recompilations <br>(SQL Re-Compilation/sec) | Average SQL recompilations per second (times/second) | avg | Dependent on business needs |
| Inbound network traffic <br>(Network Receive Throughput) | Sum of all inbound packets of all connections (MB/s) | avg | Dependent on business needs |
| Outbound network traffic <br>(Network Transmit Throughput) | Sum of all outbound packets of all connections (MB/s) | avg | Dependent on business needs |
| Number of full-table scans by SQL per second <br>(Full Scans/sec) | Disk reads/writes (times/second) | avg | < 30% Good <br>< 60% Normal <br>> 60% Attention required |
| Buffer cache hit rate <br>(Buffer cache hit ratio) | Data cache (memory) hit rate (%) | avg | >= 95% Good <br>>= 90% Normal <br>< 90% Attention required |
| Number of latch waits per second <br>(Latch Waits/sec) | Latch waits per second (times/sec) | avg | Dependent on business needs |
| Average lock wait delay <br>(Average Wait Time) | Average wait time for each lock request that causes a wait (ms) | max | Dependent on business needs |
| Average network IO delay <br>(Network IO waits) | Average network IO delay time (ms) | max | Dependent on business needs |
| Plan cache hit rate <br>(Plan Cache: Cache Hit Ratio) | Hit rate of the execution plan of each SQL (%) | max | >= 95% Good <br>>= 90% Normal <br>< 90% Attention required |



