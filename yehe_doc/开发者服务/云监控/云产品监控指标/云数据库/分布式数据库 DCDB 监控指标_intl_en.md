## Namespace
Namespace=QCE/DCDB

## Monitoring Metrics
| Parameter | Metric Name | Unit | Dimension |
| ---------------------------- | ----------------------- | ----- | ------------- |
| CpuUsageRate | CPU utilization | % | uuid and shardId |
| MemHitRate | Cache hit rate | % | uuid and shardld |
| DataDiskUsedRate | Disk space utilization | % | uuid and shardId |
| MemAvailable | Free cache space | GB | uuid and shardId |
| DataDiskAvailable | Free disk space | GB | uuid and shardId |
| BinlogUsedDisk | Used disk space for binlogs | GB | uuid and shardId |
| DiskIops | IO utilization | % | uuid and shardId |
| ConnActive | Total connections | Times/sec | uuid and shardId |
| ConnRunning | Active connections | Times/sec | uuid and shardId |
| TotalOrigSql | Total SQL statement executions | Times/sec | uuid and shardId |
| TotalErrorSql | Failed SQL statement executions | Times/sec | uuid and shardId |
| TotalSuccessSql | Successful SQL statement executions | Times/sec | uuid and shardId |
| LongQuery | Slow queries | Times/sec | uuid and shardId |
| TimeRange0 | Requests consuming 1-5 ms | Times/sec | uuid and shardId |
| TimeRange1 | Requests consuming 5-20 ms | Times/sec | uuid and shardId |
| TimeRange2 | Requests consuming 20-30 ms | Times/sec | uuid and shardId |
| TimeRange3 | Requests consuming over 30 ms | Times/sec | uuid and shardId |
| RequestTotal | Total requests (QPS) | Times/sec | uuid and shardId |
| SelectTotal | Queries | Times/sec | uuid and shardId |
| UpdateTotal | Updates | Times/sec | uuid and shardId |
| InsertTotal | Insertions | Times/sec | uuid and shardId |
| ReplaceTotal | Replacements | Times/sec | uuid and shardId |
| DeleteTotal | Deletions | Times/sec | uuid and shardId |
| MasterSwitchedTotal | Master/Slave switchovers | Times/sec | uuid and shardId |
| SlaveDelay | Master/Slave latency | ms | uuid and shardId |
| InnodbBufferPoolReads | InnoDB disk reads | Times/sec | uuid and shardId |
| InnodbBufferPoolReadRequests | InnoDB buffer pool reads | Times/sec | uuid and shardId |
| InnodbBufferPoolReadAhead | InnoDB buffer pool pre-reads | Times/sec | uuid and shardId |
| InnodbRowsDeleted | Deleted InnoDB rows | Times/sec | uuid and shardId |
| InnodbRowsInserted | Inserted InnoDB rows | Times/sec | uuid and shardId |
| InnodbRowsRead | Read InnoDB rows | Times/sec | uuid and shardId |
| InnodbRowsUpdated | Updated InnoDB rows | Times/sec | uuid and shardId |

>? The statistical granularity (`period`) for all metrics of distributed databases is either 60 or 300 seconds and varies by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | -------- | ------------------------------------------------------------ | ----------------------------------------- |
| Instances.N.Dimensions.0.Name | uuid | Dimension name of the database instance uuid | Enter a string-type dimension name, such as uuid |
| Instances.N.Dimensions.0.Value | uuid | A specific instance uuid | Enter a specific instance uuid, such as tdsqlshard-12345678 |
| Instances.N.Dimensions.1.Name | shardId | Dimension name of the instance shard ID. To query shard monitoring data, pass in this parameter. If this parameter is not passed in, the overall instance monitoring data will be queried instead | Enter a string-type dimension name, such as shardId |
| Instances.N.Dimensions.1.Value | shardId | A specific instance shard ID | Enter a specific instance shard ID, such as shard-0mzlzl89 |

## Input Parameters

**To query the monitoring data of a TDSQL for MySQL v3 instance, use the following input parameters:**
&Namespace=QCE/DCDB
&Instances.N.Dimensions.0.Name=uuid
&Instances.N.Dimensions.0.Value=<Specific instance uuid>
