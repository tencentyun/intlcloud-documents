## Namespace

Namespace=QCE/CDB

## Monitoring Metrics

### Resources

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ------------- | ------------ | ------------------------------------------------------------ | ----- | ------------------------ | ---------------------------- |
| BytesReceived | Private network inbound traffic | Number of bytes received per second | B/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| BytesSent | Private network outbound traffic | Number of bytes sent per second | B/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| Capacity | Disk usage | Including the space taken up by the MySQL data directory and logs (binlog, relaylog, undolog, errorlog, and slowlog) | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| CPUUseRate    | CPU usage   | If overuse of idle resources is permitted, the CPU utilization may exceed 100%.                         | %     | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| IOPS          | Input/output operations per second         | Input and output operations (or number of reads/writes) per second                                 | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| MemoryUse | Memory usage | If overuse of idle resources is permitted, the memory utilization may exceed 100%. | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| MemoryUseRate | Memory utilization | If overuse of idle resources is permitted, the memory utilization may exceed 100%. | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| RealCapacity | Data usage | The space taken up by the MySQL data directory, excluding that by logs (binlog, relaylog, undolog, errorlog, or slowlog) | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| VolumeRate | Disk utilization | Used disk space / purchased instance space | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - MyISAM

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| --------------- | ----------------- | ----------------------- | ---- | -------------------------------- | ---------------------------- |
| KeyCacheHitRate | MyISAM cache hit rate | Cache hit rate of the MyISAM engine | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyCacheUseRate | MyISAM cache utilization | Cache utilization of the MyISAM engine | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - InnoDB

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ------------------ | ------------------------------------- | ---------------------------------- | ----- | -------------------------------- | ---------------------------- |
| InnodbCacheHitRate | InnoDB cache hit rate | Cache hit ratio of the InnoDB engine | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbCacheUseRate | InnoDB cache utilization | Cache utilization of the InnoDB engine | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbNumOpenFiles | Number of tables opened in the InnoDB engine currently | Number of tables opened in the InnoDB engine currently | Table(s) | InstanceId and InstanceType (optional) | 5s、60s、300s、3600s         |
| InnodbOsFileReads | Number of InnoDB disk reads                     | Number of times disk files are read per second by the InnoDB engine    | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbOsFileWrites | Number of InnoDB disk writes | Number of times disk files are written per second by the InnoDB engine | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbOsFsyncs     | Number of fsync calls by InnoDB                       | Number of times the fsync function is called per second by the InnoDB engine | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - connection

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ----------------- | -------------- | ------------------------------------------------------------ | ----- | -------------------------------- | ---------------------------- |
| ConnectionUseRate | Connection utilization   | Number of current connections/maximum number of connections allowed | %     | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s |
| MaxConnections | Maximum number of connections | Maximum number of connections allowed | Connection(s)    | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| QPS | Number of queries processed per second | Number of SQL queries processed (including the execution of the INSERT, SELECT, UPDATE, DELETE, and REPLACE statements) in the database per second. It is a metric of the actual processing capability of TencentDB instances. | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ThreadsConnected  | Current connections     | Number of current connections    | Connection(s)    | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| TPS               | Transactions per second | Number of transactions performed in the database per second                                | Transaction(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - access

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ----------- | ---------- | ------------------------------------------- | ----- | -------------------------------- | ---------------------------- |
| ComDelete | Number of deletions | Number of deletions per second | Deletion(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ComInsert | Number of insertions | Number of insertions per second | Insertion(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ComReplace | Number of replacements | Number of replacements per second | Replacement(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ComUpdate | Number of updates | Number of updates per second | Update(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| Queries | Total number of queries | All SQL statements executed, including SET and SHOW      | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| QueryRate | Query rate | Actual QPS / recommended QPS           | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SelectCount | Number of times the SELECT statement is executed | Number of times the SELECT statement is executed per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SelectScan | Number of full-table scans | Number of full-table scans performed                      | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SlowQueries | Number of slow queries | Number of queries that take more than `long_query_time` to execute | Query/Queries | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - table

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ---------------- | -------------- | -------------------------- | ----- | -------------------------------- | ---------------------------- |
| CreatedTmpTables | Number of temp tables | Number of temp tables created           | Table(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| TableLocksWaited | Number of table lock waits | Number of table locks that cannot be obtained immediately | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - Tmp

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| -------------------- | -------------- | ------------------------ | ----- | -------------------------------- | ---------------------------- |
| CreatedTmpDiskTables | Number of temp disk tables | Number of temp disk tables created per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| CreatedTmpFiles | Number of temporary files | Number of temporary files created per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - key

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ---------------- | ---------------------- | ----------------------------------- | ----- | -------------------------------- | ---------------------------- |
| KeyBlocksUnused | Number of unused blocks in the key cache | Number of unused blocks in the MyISAM key cache | Block(s)| InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyBlocksUsed | Number of used blocks in the key cache | Number of used blocks in the MyISAM key cache     | Block(s)    | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyReadRequests | Number of data block reads from the key cache | Number of times the MyISAM engine reads data blocks from the key cache | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyReads | Number of data block reads from the hard disk | Number of times the MyISAM engine reads data blocks from the hard disk per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyWriteRequests | Number of data block writes into the key cache   | Number of times the MyISAM engine writes data blocks into the key cache     | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyWrites | Number of data block writes into the hard disk | Number of times the MyISAM engine writes data blocks into the hard disk per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - InnoDB row

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| -------------------- | ------------------------------- | ------------------------------- | ----- | ------------------------ | ---------------------------- |
| InnodbRowLockTimeAvg | Average time of locking a InnoDB row | Average time the InnoDB engine spends locking a row | ms | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowLockWaits | Number of InnoDB row lock waits | Number of times the InnoDB engine waits to lock a row per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowsDeleted | Number of rows deleted from InnoDB | Number of rows deleted from the InnoDB engine per second | Row(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowsInserted | Number of rows inserted into InnoDB | Number of rows inserted into the InnoDB engine per second | Row(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowsRead | Number of InnoDB row reads | Number of rows read by the InnoDB engine per second | Row(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowsUpdated | Number of updated InnoDB rows | Number of rows updated by the InnoDB engine per second | Row(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - InnoDB data

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ----------------- | --------------- | --------------------------------------- | ------- | -------------------------------- | ---------------------------- |
| InnodbDataReads | Size of data read by InnoDB | Size of data read by the InnoDB engine per second in bytes | B/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbDataReads | Total number of InnoDB data reads | Number of data reads handled by the InnoDB engine per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbDataWrites | Total number of InnoDB data writes | Number of data writes processed by the InnoDB engine per second     | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbDataWritten | Size of data written to InnoDB | Size of data written to the InnoDB engine per second in bytes | B/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine monitoring (extended) - handler

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ------------------ | -------------- | ------------------------ | ----- | -------------------------------- | ---------------------------- |
| HandlerCommit | Number of internal commits | Number of transaction commits per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| HandlerReadRndNext | Number of read-next-row requests | Number of requests to read the next row per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| HandlerRollback | Number of internal rollbacks | Number of transaction rollbacks per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - buffer

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ---------------------------- | ----------------------- | --------------------------------------- | ----- | -------------------------------- | ---------------------------- |
| InnodbBufferPoolPagesFree    | Number of InnoDB blank pages            | Number of blank pages in the InnoDB buffer pool                 | Page(s) | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s |
| InnodbBufferPoolPagesTotal   | Total number of InnoDB pages          | Total number of memory pages taken up by the InnoDB engine | Page(s) | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbBufferPoolReadRequests | Number of times pages are pre-fetched into the InnoDB buffer pool | Number of logic read requests processed by the InnoDB engine per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbBufferPoolReads | Number of InnoDB physical reads | Number of physical read requests processed by the InnoDB engine per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - others

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ----------- | ---------- | -------------------- | ----- | -------------------------------- | ---------------------------- |
| LogCapacity | Log usage | Size of logs used by the engine | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s        |
| OpenFiles | Number of opened files | Number of files opened by the engine | File(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - connection

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| -------------- | -------------- | -------------------------- | ---- | -------------------------------- | ---------------------------- |
| ThreadsCreated | Number of created threads | Number of threads created to process connections | Thread(s)| InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ThreadsRunning | Number of running threads | Number of running (non-idle) threads | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - access

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ----------- | ---------- | ------------ | ----- | -------------------------------- | ---------------------------- |
| ComCommit | Number of commits | Number of commits per second | Times/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ComRollback | Number of rollbacks | Number of rollbacks per second | Times/sec | InstanceId, InstanceType (optional) |5s, 60s, 300s, 3,600s, 86,400s |

### Engine monitoring (extended) - table

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ------------------- | ---------------- | ---------------------- | ---- | -------------------------------- | ---------------------------- |
| OpenedTables | Number of opened tables | Number of tables opened by the engine | Table(s) | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| TableLocksImmediate | Number of table locks released immediately | Number of table locks released immediately by the engine | Lock(s) | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Deployment (replica)

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ----------------------- | ------------ | ---------------- | ----------------------------------- | -------------------------------- | ---------------------------- |
| MasterSlaveSyncDistance | Source-replica delay in size | Source-replica binlog delay in size | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SecondsBehindMaster | Source-replica delay in time | Source-replica delay in time | Sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SlaveIoRunning          | IO thread status | IO thread status | Values: 0: Yes; 1: No; 2: Connecting | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SlaveSqlRunning | SQL thread status | SQL thread status | Values: 0: Yes; 1: No; 2: Connecting   | InstanceId, InstanceTyp (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

> ?Statistical periods (`period`) may vary by metric. You can get the statistical periods for different metrics by calling the [`DescribeBaseMetrics`](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Dimensions and Parameters

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | -------------------- | ------------------------------------------------------------ | -------------------------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | Database instance name                                         | Enter a string-type dimension name, such as `InstanceId` |
| Instances.N.Dimensions.0.Value | InstanceId | Database ID                                              | Enter an instance ID, such as `cdb-ebul6659` |
| Instances.N.Dimensions.1.Name | InstanceType (optional) | Database instance type                                               | Enter a string-type dimension name, such as `InstanceType` |
| Instances.N.Dimensions.1.Value | InstanceType (optional) | Database instance type. Valid values: <br><li>1 (default): Pulls monitoring data from the source <br><li>2: Pulls monitoring data from the replica (single-node and dual-node instance supported only) <br><li>3: Pulls monitoring data from a read-only instance (the ID of the read-only instance must be passed in as `InstanceId`; otherwise, the value `1` will be used for the database instance type by default) <br><li>4: Pulls monitoring data from the second replica (applicable only to Finance Edition) | Enter an instance type (optional). Default value: 1 |

> ? `InstanceType` description:
>
> - If the `InstanceId` value is a source instance ID, only `InstanceType` supports pulling the monitoring data of the source (value: 1), replica (value: 2), read-only instance (value: 3), and second replica (value: 4).
> - If the `InstanceId` value is a source instance ID, the `InstanceType` value is 2 (replica), and the source instance has three nodes (one source and two replicas), then the monitoring data of one monitored node will be missing, as pulling replica monitoring data is supported only for single-node and two-node instances.
> - To pull the monitoring data of a read-only instance, pass in its ID as `InstanceId`.



## Input Parameters

**To query the monitored data of TencentDB for MySQL, use the following input parameters:**

&Namespace=QCE/CDB
&Instances.N.Dimensions.0.Name=`InstanceId`
&Instances.N.Dimensions.0.Value= Specific database ID 
&Instances.N.Dimensions.1.Name=`InstanceType`
&Instances.N.Dimensions.1.Value=Database instance type
