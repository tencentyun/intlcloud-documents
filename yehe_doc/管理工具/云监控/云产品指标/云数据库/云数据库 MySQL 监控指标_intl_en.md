## Namespace

Namespace=QCE/CDB

## Monitoring Metrics

### Resource monitoring

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ------------- | ------------ | ------------------------------------------------------------ | ----- | ------------------------ | ---------------------------- |
| BytesReceived | Private network inbound traffic | Number of bytes accepted per second | Bytes/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| BytesSent | Private network outbound traffic | Number of bytes sent per second | Bytes/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| Capacity | Used disk space | This includes the MySQL data directories and the binlog/relaylog/undolog/errorlog/slowlog space | MB | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| CpuUseRate | CPU utilization | The CPU capacity can be overused during the idle period, and the CPU utilization may be greater than 100% | % | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| IOPS          | IOPS         | Input and output volume (or number of reads/writes) per second                                 | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| MemoryUse | Memory usage | The memory capacity can be overused during the idle period, and the actual memory usage may be greater than the purchased specifications | % | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| MemoryUseRate | Memory utilization | The memory capacity can be overused during the idle period, and the memory utilization may be greater than 100% | % | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| RealCapacity | Disk usage | This only includes the MySQL data directories and does not include the binlog/relaylog/undolog/errorlog/slowlog space | MB | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| VolumeRate | Disk utilization | Used disk space/purchased instance space | % | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (general) - MyISAM

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| --------------- | ----------------- | ----------------------- | ---- | ------------------------ | ---------------------------- |
| KeyCacheHitRate | MyISAM cache hit rate | Cache hit rate of the MyISAM engine | % | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| KeyCacheUseRate | MyISAM cache utilization | Cache utilization of the MyISAM engine | % | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (general) - InnoDB

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ------------------ | ------------------------------------- | ---------------------------------- | ----- | ------------------------ | ---------------------------- |
| InnodbCacheHitRate | InnoDB cache hit rate | Cache hit rate of the InnoDB engine | % | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbCacheUseRate | InnoDB cache utilization | Cache utilization of the InnoDB engine | % | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbNumOpenFiles | Total InnoDB pages | Number of tables opened in the InnoDB engine currently | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s |
| InnodbOsFileReads | InnoDB disk reads | Number of disk file reads per second by the InnoDB engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbOsFileWrites | InnoDB disk writes | Number of disk file writes per second by the InnoDB engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbOsFsyncs | InnoDB fsync function calls | Number of fsync function calls per second by the InnoDB engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (general) - connection

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ----------------- | -------------- | ------------------------------------------------------------ | ----- | ------------------------ | ---------------------------- |
| ConnectionUseRate | Connection utilization | Number of currently enabled connections/maximum number of connections | % | InstanceId, InstanceType | 5s, 10s, 60s, 300s, 3600s |
| MaxConnections | Maximum connections | Maximum number of connections | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| Qps | Executions per second | Number of SQL statements (including INSERT, SELECT, UPDATE, DELETE, and REPLACE statements) executed in the database per second. The QPS metric reflects the actual processing capability of the TencentDB instances. | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| ThreadsConnected  | Current connections     | Number of currently opened connections                                         | -    | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| Tps               | Transactions executed per second | Number of transactions executed in the database per second                                | Transactions/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (general) - access

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ----------- | ---------- | ------------------------------------------- | ----- | ------------------------ | ---------------------------- |
| ComDelete | Deletions | Number of deletions per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| ComInsert | Insertions | Number of insertions per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| ComReplace | Replacements | Number of replacements per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| ComUpdate | Updates | Number of updates per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| Queries     | Total queries | All executed SQL statements such as set and show      | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| QueryRate   | Query utilization | Actual QPS/recommended QPS           | %     | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| SelectCount | Queries     | Number of queries per second                                  | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| SelectScan  | Full-table scans | Number of full-table scans executed                      | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| SlowQueries | Slow queries   | Number of queries that take more than `long_query_time` second(s) to be executed | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (general) - table

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ---------------- | -------------- | -------------------------- | ----- | ------------------------ | ---------------------------- |
| CreatedTmpTables | Temp tables | Number of created temp tables | Tables/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| TableLocksWaited | Table locks awaited   | Number of table locks due to the failure to get tables immediately | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - Tmp

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| -------------------- | -------------- | ------------------------ | ----- | ------------------------ | ---------------------------- |
| CreatedTmpDiskTables | Disk temp tables | Number of disk temp tables created per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| CreatedTmpTables | Temp files | Number of temp files created per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - key

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ---------------- | ---------------------- | ----------------------------------- | ----- | ------------------------ | ---------------------------- |
| KeyBlocksUnused | Unused blocks in key cache | Number of unused key cache blocks for the MyISAM engine | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| KeyBlocksUsed | Used blocks in key cache | Number of used key cache blocks for the MyISAM engine | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| KeyReadRequests | Data block reads for key cache | Number of key cache block reads per second by the MyISAM engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| KeyReads | Data block reads for disk | Number of disk data block reads per second by the MyISAM engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| KeyWriteRequests | Data block writes for key cache | Number of key cache block writes per second by the MyISAM engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| KeyWrites | Data block writes for disk | Number of disk data block writes per second by the MyISAM engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - InnoDB row

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| -------------------- | ------------------------------- | ------------------------------- | ----- | ------------------------ | ---------------------------- |
| InnodbRowLockTimeAvg | Average InnoDB row lock getting time in ms | Average time of getting a row lock by the InnoDB engine | ms | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbRowLockWaits | InnoDB row lock waits | Number of row lock waits per second by the InnoDB engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbRowsDeleted | Deleted InnoDB rows | Number of rows deleted per second by the InnoDB engine | Rows/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbRowsInserted | Inserted InnoDB rows | Number of rows inserted per second by the InnoDB engine | Rows/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbRowsRead | Read InnoDB rows | Number of rows read per second by the InnoDB engine | Rows/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbRowsUpdated | Updated InnoDB rows | Number of rows updated per second by the InnoDB engine | Rows/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - InnoDB data

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ----------------- | --------------- | --------------------------------------- | ------- | ------------------------ | ---------------------------- |
| InnodbDataRead | Read InnoDB data volume | Number of data bytes read per second by the InnoDB engine | Bytes/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbDataReads | Total read InnoDB data volume | Number of data reads completed per second by the InnoDB engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbDataWrites | Total written InnoDB data volume | Number of data writes completed per second by the InnoDB engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbDataWritten | Written InnoDB data volume | Number of data bytes written per second by the InnoDB engine | Bytes/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - handler

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ------------------ | -------------- | ------------------------ | ----- | ------------------------ | ---------------------------- |
| HandlerCommit | Internal commits | Number of transaction commits per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| HandlerReadRndNext | Next-row read requests | Number of requests for reading the next row per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| HandlerRollback | Internal rollbacks | Number of transaction rollbacks per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - buff

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ---------------------------- | ----------------------- | --------------------------------------- | ----- | ------------------------ | ---------------------------- |
| InnodbBufferPoolPagesFree | InnoDB blank pages | Number of memory blank pages of the InnoDB engine | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s |
| InnodbBufferPoolPagesTotal | Total InnoDB pages | Total number of memory pages occupied by the InnoDB engine | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbBufferPoolReadRequests | InnoDB buffer pool read-aheads | Number of logic read requests completed per second by the InnoDB engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| InnodbBufferPoolReadRequests | InnoDB disk reads | Number of physical read requests completed per second by the InnoDB engine | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - others

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ----------- | ---------- | -------------------- | ----- | ------------------------ | ---------------------------- |
| LogCapacity | Log usage | Log usage of the engine | MB | InstanceId, InstanceType | 5s, 60s, 300s, 3600s |
| OpenFiles | Opened files | Number of files opened by the engine | Files/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - connection

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| -------------- | -------------- | -------------------------- | ---- | ------------------------ | ---------------------------- |
| ThreadsCreated | Created threads | Number of threads created for processing connections | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| ThreadsRunning | Running threads | Number of running (non-idle) threads | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - access

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ----------- | ---------- | ------------ | ----- | ------------------------ | ---------------------------- |
| ComCommit | Commits | Number of commits per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| ComRollback | Rollbacks | Number of rollbacks per second | Times/sec | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Engine monitoring (extended) - table

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ------------------- | ---------------- | ---------------------- | ---- | ------------------------ | ---------------------------- |
| OpenedTables | Opened tables | Number of tables opened by the engine | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| TableLocksImmediate | Table locks released immediately | Number of table locks released immediately by the engine | - | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |

### Deployment monitoring (secondary)

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ----------------------- | ------------ | ---------------- | ----------------------------------- | ------------------------ | ---------------------------- |
| MasterSlaveSyncDistance | Primary/Secondary lag distance | Primary/Secondary binlog lag distance | MB | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| SecondsBehindMaster | Primary/Secondary lag time | Primary/Secondary lag time | s | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| SlaveIoRunning | IO thread status | IO thread running status | Status value (0: Yes, 1: No, 2: Connecting) | InstanceId, InstanceType | 5s, 60s, 300s, 3600s, 86400s |
| SlaveSqlRunning | SQL thread status | SQL thread running status | slave_sql_running | InstanceId, InstanceTyp | 5s, 60s, 300s, 3600s, 86400s |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ------------ | ------------------------------------------------------------ | -------------------------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | Database instance ID name | Enter a String-type dimension name, such as `topicId` |
| Instances.N.Dimensions.0.Value | InstanceId | Specific database ID | Enter a specific instance ID, such as `topic-i4p4k0u0` |
| Instances.N.Dimensions.1.Name | InstanceType | Database instance type | Enter a String-type dimension name, such as `InstanceType` |
| Instances.N.Dimensions.1.Value | InstanceType | Database instance type. Valid values: <br><li>1: pulls the monitoring data of the instance's primary server<br><li>2: pulls the monitoring data of the instance's secondary server<br><li>3: pulls the monitoring data of the read-only instance<br><li>4: pulls the monitoring data of the instance's second secondary server (only applicable to Finance Edition instances) | Enter an instance type. Default value: 1 |

## Input Parameter Description

**To query the monitoring data of a TencentDB for MySQL instance, use the following input parameters:**
&Namespace=QCE/CDB
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=Specific database ID 
&Instances.N.Dimensions.1.Name=InstanceType
&Instances.N.Dimensions.1.Value=Database instance type
