>? CM will soon stop supporting the old monitoring metrics for TDSQL for MySQL. Please use the [new metrics](https://intl.cloud.tencent.com/document/product/248/40010).

## Namespace
Namespace=QCE/DCDB

## Monitoring Metrics
| Parameter                   | Meaning              | Unit  | Dimension          |
| ---------------------------- | ----------------------- | ----- | ------------- |
| CpuUsageRate                 | CPU usage              | %     | uuid and shardId |
| MemHitRate                   | Cache hit ratio              | %     | uuid and shardld |
| DataDiskUsedRate             | Disk space usage          | %     | uuid and shardId |
| MemAvailable                 | Available memory            | GB    | uuid and shardId |
| DataDiskAvailable | Available disk space | GB | uuid and shardId |
| BinlogUsedDisk | Used binlog disk space | GB | uuid and shardId |
| DiskIops | IO usage | % | uuid and shardId |
| ConnActive | Total connections | Connections/sec | uuid and shardId |
| ConnRunning | Active connections | Connections/sec | uuid and shardId |
| TotalOrigSql | Total SQL statement executions | Executions/sec | uuid and shardId |
| TotalErrorSql | Failed SQL statement executions | Executions/sec | uuid and shardId |
| TotalSuccessSql | Successful SQL statement executions | Executions/sec | uuid and shardId |
| LongQuery | Slow queries | Queries/sec | uuid and shardId |
| TimeRange0 | Queries that take 1-5 ms to execute | Queries/sec | uuid and shardId |
| TimeRange1 | Queries that take 5-20 ms to execute | Queries/sec | uuid and shardId |
| TimeRange2 | Queries that take 20-30 ms to execute | Queries/sec | uuid and shardId |
| TimeRange3 | Queries that take longer than 30 ms to execute | Queries/sec | uuid and shardId |
| RequestTotal | Total queries (QPS) | Queries/sec | uuid and shardId |
| SelectTotal | SELECT queries | Queries/sec | uuid and shardId |
| UpdateTotal | UPDATE queries | Queries/sec | uuid and shardId |
| InsertTotal | INSERT queries | Queries/sec | uuid and shardId |
| ReplaceTotal | REPLACE queries | Queries/sec | uuid and shardId |
| DeleteTotal | DELETE queries | Queries/sec | uuid and shardId |
| MasterSwitchedTotal | Master-slave switchovers | Times/sec | uuid and shardId |
| SlaveDelay | Master-slave synchronization delay | ms | uuid and shardId |
| InnodbBufferPoolReads | InnoDB disk reads | Times/sec | uuid and shardId |
| InnodbBufferPoolReadRequests | InnoDB buffer pool reads | Times/sec | uuid and shardId |
| InnodbBufferPoolReadAhead | InnoDB buffer pool read-aheads | Times/sec | uuid and shardId |
| InnodbRowsDeleted | Rows deleted by InnoDB | Rows/sec | uuid and shardId |
| InnodbRowsInserted | Rows inserted by InnoDB | Rows/sec | uuid and shardId |
| InnodbRowsRead | Rows read by InnoDB | Rows/sec | uuid and shardId |
| InnodbRowsUpdated | Rows updated by InnoDB | Rows/sec | uuid and shardId |

>? The statistical period for the metrics of TDSQL for MySQL can be 60s or 300s. The exact statistical periods supported vary from metric to metric. You can get the periods different metrics support by calling the `DescribeBaseMetrics` API.

## Dimensions and Parameters

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | -------- | ------------------------------------------------------------ | ----------------------------------------- |
| Instances.N.Dimensions.0.Name | uuid | Dimension name for the database instance | Enter a string-type dimension name: `uuid` |
| Instances.N.Dimensions.0.Value | uuid | The instance’s UUID | Enter an instance UUID, e.g., `tdsqlshard-12345678` |
| Instances.N.Dimensions.1.Name | shardId | Dimension name for an instance shard. You can pass in this parameter to query a shard’s monitoring data. If it is not passed in, all monitoring data of the instance is queried. | Enter a string-type dimension name: `shardId`. |
| Instances.N.Dimensions.1.Value | shardId | An instance shard ID | Enter an instance shard ID, e.g., `shard-0mzlzl89`. |

## Input Parameters

**To query the monitoring data of a TencentDB for TDSQL v3 instance, use the following input parameters:**
&Namespace=QCE/DCDB
&Instances.N.Dimensions.0.Name=uuid
&Instances.N.Dimensions.0.Value=Specific instance uuid
