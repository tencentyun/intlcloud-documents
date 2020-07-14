## Namespace

Namespace=QCE/CDB

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ---------------------------- | ---------------------------------------- | ------------------------------------------------------------ | ------- | ------------------------ |
| CPUUseRate | CPU utilization | The CPU capacity can be overused during the idle period, and the CPU utilization may be greater than 100% | % | InstanceId and InstanceType |
| MemoryUseRate | Memory utilization | The memory capacity can be overused during the idle period, and the memory usage may be greater than 100% | % | InstanceId and InstanceType |
| MemoryUse | Memory usage | The memory capacity can be overused during the idle period, and the actual memory usage may be greater than the purchased specifications | MB | InstanceId and InstanceType |
| VolumeRate | Disk utilization | Used disk space/purchased instance space | % | InstanceId and InstanceType |
| RealCapacity | Disk usage (only including the usage of the data space) | Only includes the MySQL data directories and does not include the binlog/relaylog/undolog/errorlog/slowlog space | MB | InstanceId and InstanceType |
| Capacity | Disk used space (not including the usage of data and log space) | Includes the MySQL data directories and the binlog/relaylog/undolog/errorlog/slowlog space | MB | InstanceId and InstanceType |
| BytesSent | Private outbound traffic | Private outbound traffic per second | Byte/sec | InstanceId and InstanceType |
| BytesReceived | Private inbound traffic | Private inbound traffic per second | Byte/sec | InstanceId and InstanceType |
| QPS | Number of executions per second | Number of SQL statements (including insert, select, update, delete, and replace statements) executed in the database per second. The QPS metric reflects the actual processing capability of the TencentDB for Redis instances. | Times/sec | InstanceId and InstanceType |
| TPS | Number of transactions executed per second | Number of transactions executed in the database per second | Times/sec | InstanceId and InstanceType |
| MaxConnections | Maximum number of connections | Maximum number of connections in the database | Count | InstanceId and InstanceType |
| ThreadsConnected | Number of currently enabled thread connections | Number of currently enabled thread connections | Count | InstanceId and InstanceType |
| ConnectionUseRate | Connection utilization | Number of currently enabled connections/Maximum number of connections | % | InstanceId and InstanceType |
| SlowQueries | Number of slow queries | Number of queries with an execution time greater than long_query_time seconds | Times/min | InstanceId and InstanceType |
| SelectScan | Number of full-table scans | Number of queries used for executing full-table scans | Times/sec | InstanceId and InstanceType |
| SelectCount | Number of queries | Number of queries per second | Times/sec | InstanceId and InstanceType |
| ComUpdate | Number of updates | Number of updates per second | Times/sec | InstanceId and InstanceType |
| ComDelete | Number of deletions | Number of deletions per second | Times/sec | InstanceId and InstanceType |
| ComInsert | Number of insertions | Number of insertions per second | Times/sec | InstanceId and InstanceType |
| ComReplace | Number of replacements | Number of replacements per second | Times/sec | InstanceId and InstanceType |
| Queries | Total requests | All executed SQL statements, including but not limited to set and show statements | Times/sec | InstanceId and InstanceType |
| QueryRate | Query utilization | QPS; that is, the number of executions per second/recommended operations per second | % | InstanceId and InstanceType |
| CreatedTmpTables | Number of temporary tables | Number of created temporary tables | Times/sec | InstanceId and InstanceType |
| TableLocksWaited | Number of table lock waits | Number of table locks that cannot be obtained immediately | Times/sec | InstanceId and InstanceType |
| InnodbCacheUseRate | InnoDB cache utilization | Cache utilization of the InnoDB engine | % | InstanceId and InstanceType |
| InnodbCacheHitRate | InnoDB cache hit rate | Cache hit ratio of the InnoDB engine | % | InstanceId and InstanceType |
| InnodbOsFileReads | Number of InnoDB disk reads | Number of disk file reads per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbOsFileWrites | Number of InnoDB disk writes | Number of disk file writes per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbOsFsyncs | Number of InnoDB fsync functions | Number of fsync function calls per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbNumOpenFiles | Number of tables opened in the InnoDB engine currently | Number of tables opened in the InnoDB engine currently | Count | InstanceId and InstanceType |
| KeyCacheUseRate | MyISAM cache utilization | Cache utilization of the MyISAM engine | % | InstanceId and InstanceType |
| KeyCacheHitRate | MyISAM cache hit rate | Cache hit rate of the MyISAM engine | % | InstanceId and InstanceType |
| ComCommit | Number of commits | Number of commits per second | Times/sec | InstanceId and InstanceType |
| ComRollback | Number of rollbacks | Number of rollbacks per second | Times/sec | InstanceId and InstanceType |
| ThreadsCreated | Number of created threads | Number of threads created for processing connections | Count | InstanceId and InstanceType |
| ThreadsRunning | Number of running threads | Number of running (non-idle) threads | InstanceId and InstanceType |
| CreatedTmpDiskTables | Number of temporary disk tables | Number of temporary disk tables created per second | Times/sec | InstanceId and InstanceType |
| CreatedTmpFiles | Number of temporary files | Number of temporary files created per second | Times/sec | InstanceId and InstanceType |
| HandlerReadRndNext | Number of next-row read requests | Number of requests for reading the next row per second | Times/sec | InstanceId and InstanceType |
| HandlerRollback | Number of internal rollbacks | Number of transaction rollbacks per second | Times/sec | InstanceId and InstanceType |
| HandlerCommit | Number of internal commits | Number of transaction commits per second | Times/sec | InstanceId and InstanceType |
| InnodbBufferPoolPagesFree | Number of InnoDB blank pages | Number of memory blank pages of the InnoDB engine | Count | InstanceId and InstanceType |
| InnodbBufferPoolPagesTotal | Total number of InnoDB pages | Total number of memory pages occupied by the InnoDB engine | Count | InstanceId and InstanceType |
| InnodbBufferPoolReadRequests | InnoDB logic reads | Number of logic read requests completed per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbBufferPoolReads | InnoDB physical reads | Number of physical read requests completed per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbDataReads | Total volume of read InnoDB data | Number of data reads completed per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbDataRead | Volume of read InnoDB data | Number of data bytes read per second for the InnoDB engine | Bytes/sec | InstanceId and InstanceType |
| InnodbDataWrites | Total volume of written InnoDB data | Number of data writes completed per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbDataWritten | Volume of written InnoDB data | Number of data bytes written per second for the InnoDB engine | Bytes/sec | InstanceId and InstanceType |
| InnodbRowsDeleted | Number of deleted InnoDB rows | Number of rows deleted per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbRowsInserted | Number of inserted InnoDB rows | Number of rows inserted per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbRowsUpdated | Number of updated InnoDB rows | Number of rows updated per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbRowsRead | Number of read InnoDB rows | Number of rows read per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| InnodbRowLockTimeAvg | Average time of obtaining a InnoDB row lock | Average time of obtaining a row lock for the InnoDB engine | ms | InstanceId and InstanceType |
| InnodbRowLockWaits | Number of InnoDB row lock waits | Number of row lock waits per second for the InnoDB engine | Times/sec | InstanceId and InstanceType |
| KeyBlocksUnused | Number of unused blocks in the key cache | Number of unused key cache blocks for the MyISAM engine | Count | InstanceId and InstanceType |
| KeyBlocksUsed | Number of used blocks in the key cache | Number of used key cache blocks for the MyISAM engine | Count | InstanceId and InstanceType |
| KeyReadRequests | Number of data block reads for the key cache | Number of key cache block reads per second for the MyISAM engine | Times/sec | InstanceId and InstanceType |
| KeyReads | Number of data block reads for the hard disk | Number of hard-disk data block reads per second for the MyISAM engine | Times/sec | InstanceId and InstanceType |
| KeyWriteRequests | Number of data block writes for the key cache | Number of key cache block writes per second for the MyISAM engine | Times/sec | InstanceId and InstanceType |
| KeyWrites | Number of data block writes for the hard disk | Number of hard-disk data block writes per second for the MyISAM engine | Times/sec | InstanceId and InstanceType |
| OpenedTables | Number of opened tables | Number of tables opened in the database currently | Count | InstanceId and InstanceType |
| TableLocksImmediate | Number of table locks released immediately | Number of table locks released immediately | Count | InstanceId and InstanceType |
| OpenFiles | Total number of opened files | Total number of files opened in the database currently | Count | InstanceId and InstanceType |
| LogCapacity | Log usage | Current log usage of the database | MB | InstanceId and InstanceType |
| SlaveIoRunning | State of the I/O thread | State of the I/O thread in the Slave | Count | InstanceId and InstanceType |
| SlaveSqlRunning | State of the SQL thread | State of the SQL thread in the Slave | Count | InstanceId and InstanceType |
| MasterSlaveSyncDistance | Latency distance between the Master and the Slave | Binlog difference between the Master and the Slave | MB | InstanceId and InstanceType |
| SecondsBehindMaster | Latency time between the Master and the Slave | Latency time between the Master and the Slave | MB | InstanceId and InstanceType |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ------------ | ------------------------------------------------------------ | ---------------------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | Database instance ID | Enter a string-type dimension name, such as topicId |
| Instances.N.Dimensions.0.Value | InstanceId | A specific database ID | Enter a specific instance ID, such as topic-i4p4k0u0 |
| Instances.N.Dimensions.1.Name | InstanceType | Database instance type | Enter a string-type dimension name, such as InstanceType |
  | Instances.N.Dimensions.1.Value | InstanceType | Database instance type. The default value is 1: <br><li>if the default value of `InstanceType` is set to 1, it means to obtain the monitoring data of the Master. <br><li>To obtain the `SlaveIoRunning`, `SlaveSqlRunning`, `MasterSlaveSyncDistance`, or `SecondsBehindMaster` monitoring data of the Slave, set the value of `InstanceType` to 2. | Enter an instance type. The default value is 1. |
	
	
	
## Input Parameters

To query the monitoring data of TencentDB for MySQL, use the following input parameters:
&Namespace=QCE/CDB
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=<Specific database ID> 
