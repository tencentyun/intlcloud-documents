
## Namespace

Namespace=QCE/SQLSERVER

## Monitoring Metrics

### Common metrics

| Parameter | Metric Name | Description | Unit | Dimension |
|---------|---------|---------|---------|---------|
| Cpu | CPU utilization | Percentage of instance CPU usage | % | resourceId |
| Transactions | Number of transactions | Average number of transactions per second | Times/sec | resourceId |
| Connections | Number of connections | Average number of databases connected by users per second | Count | resourceId |
| Requests | Number of requests | Number of requests per second | Times/sec | resourceId |
| Logins | Number of logins | Number of logins per second | Times/sec | resourceId |
| Logouts | Number of logouts | Number of logouts per second | Times/sec | resourceId |
| Storage | Used storage | Sum of storage space consumed by instance database files and log files | GB | resourceId |
| InFlow | Inbound traffic | Sum of inbound packet sizes for all connections | KB/s | resourceId |
| OutFlow | Outbound traffic | Sum of outbound packet sizes for all connections | KB/s | resourceId |
| Iops | Disk IOPS | Disk read/write operations per second | Times/sec | resourceId |
| DiskReads | Number of disk reads | Number of disk reads per second | Times/sec | resourceId |
| DiskWrites | Number of disk writes | Number of disk writes per second | Times/sec | resourceId |
| ServerMemory | Memory usage | Actual memory usage | MB | resourceId |

### Performance optimization metrics

| Parameter | Metric Name | Description | Unit | Dimension |
|---------|---------|---------|---------|---------|
| SlowQueries | Slow queries | Number of slow queries with a running time greater than one second | Count | resourceId |
| BlockedProcesses | Number of blocked processes | Number of currently blocked processes | Count | resourceId |
| LockedRequests | Number of lock requests | Average number of lock requests per second | Times/sec | resourceId |
| UserErrors | Number of user errors | Average number of user errors per second | Times/sec | resourceId |
| SqlCompilations | Number of SQL compilations | Average number of SQL compilations per second | Times/sec | resourceId |
| SqlRecompilations | Number of SQL recompilations | Average number of SQL recompilations per second | Times/sec | resourceId |
| FullScans | Number of full-table scans for SQL per second | Number of full scans without limitations per second | Times/sec | resourceId |
| BufferCacheHitRatio | Buffer cache hit rate | Data cache (memory) hit rate | % | resourceId |
| LatchWaits | Number of latch waits | Number of latch waits per second | Times/sec | resourceId |
| LockWaits | Average latency on a lock wait | Average wait time of each lock request resulting in lock wait | ms | resourceId |
| NetworkIoWaits | I/O wait time | Average network I/O wait time | ms | resourceId |
| PlanCacheHitRatio | Plan cache hit rate | The hit rate of a plan. Each SQL statement has a plan with a hit rate | % | resourceId |
| FreeStorage | Residual capacity of the hard disk | Percentage of the residual capacity of the hard disk | % | resourceId |

>? The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------- | -------------------- | ----------------------------------------------- |
| Instances.N.Dimensions.0.Name | resourceId | Dimension name of the instance resource ID | Enter a string-type dimension name, such as resourceId |
| Instances.N.Dimensions.0.Value | resourceId | A specific instance resource ID | Enter a specific instance resource ID, such as mssql-dh0123456 |

## Input Parameters

To query the monitoring data of TencentDB for SQL Server, use the following input parameters:
&Namespace=QCE/SQLSERVER
&Instances.N.Dimensions.0.Name=resourceId
&Instances.N.Dimensions.0.Value=<Instance resource ID> 

