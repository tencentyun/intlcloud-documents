## Namespace

Namespace=QCE/CDB

## Monitored Metrics

### Resource monitoring

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ------------- | ------------ | ------------------------------------------------------------ | ----- | ------------------------ | ---------------------------- |
| BytesReceived | Private network inbound traffic | Number of bytes received per second | B/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| BytesSent | Private network outbound traffic | Number of bytes sent per second | B/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| Capacity | Disk usage | Including the space taken up by the MySQL data directory and logs (binlog, relaylog, undolog, errorlog, and slowlog) | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| CpuUseRate    | CPU usage   | May be greater than 100% as you are allowed to use idle CPU resources that you have not purchased                         | %     | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| IOPS          | Input/output operations per second         | Input and output operations (or number of reads/writes) per second                                 | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| MemoryUse | Memory usage | May be greater than the purchased memory as you are allowed to use idle memory you have not purchased | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| MemoryUseRate | Memory utilization | May be greater than 100% as you are allowed to use idle memory you have not purchased | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| RealCapacity | Disk usage | The space taken up by the MySQL data directory, not including that by logs (binlog, relaylog, undolog, errorlog, or slowlog) | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| VolumeRate | Disk utilization | Used disk space/purchased instance space | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - MyISAM

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| --------------- | ----------------- | ----------------------- | ---- | -------------------------------- | ---------------------------- |
| KeyCacheHitRate | MyISAM cache hit rate | Cache hit rate of the MyISAM engine | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyCacheUseRate | MyISAM cache utilization | Cache utilization of the MyISAM engine | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - InnoDB

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ------------------ | ------------------------------------- | ---------------------------------- | ----- | -------------------------------- | ---------------------------- |
| InnodbCacheHitRate | InnoDB cache hit rate | Cache hit rate of the InnoDB engine | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbCacheUseRate | InnoDB cache utilization | Cache utilization of the InnoDB engine | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbNumOpenFiles | Total number of tables currently opened in the InnoDB engine        | Number of tables currently opened in the InnoDB engine | Table(s)    | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s |
| InnodbOsFileReads | Number of InnoDB disk reads                     | Number of times disk files are read per second by the InnoDB engine    | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbOsFileWrites | Number of InnoDB disk writes | Number of times disk files are written per second by the InnoDB engine | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbOsFsyncs     | Number of fsync calls by Innodb                       | Number of times the fsync function is called per second by the InnoDB engine | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - connection

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ----------------- | -------------- | ------------------------------------------------------------ | ----- | -------------------------------- | ---------------------------- |
| ConnectionUseRate | Connection utilization   | Number of current connections/maximum number of connections allowed | %     | InstanceId, InstanceType (optional) | 5s, 10s, 60s, 300s, 3,600s |
| MaxConnections | Maximum number of connections | Maximum number of connections allowed | Connection(s)    | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| QPS | Number of queries processed per second | Number of SQL queries processed (including the execution of the INSERT, SELECT, UPDATE, DELETE, and REPLACE statements) in the database per second. It is a metric of the actual processing capability of TencentDB instances | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ThreadsConnected  | Current connections     | Number of current connections    | Connection(s)    | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| Tps               | Transactions per second | Number of transactions performed in the database per second                                | Transaction(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - access

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ----------- | ---------- | ------------------------------------------- | ----- | -------------------------------- | ---------------------------- |
| ComDelete | Number of deletions | Number of deletions per second | Deletion(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ComInsert | Number of insertions | Number of insertions per second | Insertion(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ComReplace | Number of replacements | Number of replacements per second | Replacement(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ComUpdate | Number of updates | Number of updates per second | Update(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| Queries | Total query number | All SQL statements executed, including SET, SHOW, etc.      | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| QueryRate | Query ratio | Actual number of queries processed per second (QPS)/Recommended QPS           | % | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SelectCount | Number of times the SELECT statement is executed | Number of times the SELECT statement is executed per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SelectScan | Number of full-table scans | Number of full-table scans performed                      | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SlowQueries | Number of slow queries | Number of queries that take more than long_query_time seconds to execute | Query(ies) | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (general) - table

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ---------------- | -------------- | -------------------------- | ----- | -------------------------------- | ---------------------------- |
| CreatedTmpTables | Number of temporary tables | Number of temporary tables created           | Table(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| TableLocksWaited | Number of table lock waits | Number of table locks that cannot be obtained immediately | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - Tmp

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| -------------------- | -------------- | ------------------------ | ----- | -------------------------------- | ---------------------------- |
| CreatedTmpDiskTables | Number of temporary disk tables | Number of temporary disk tables created per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| CreatedTmpFiles | Number of temporary files | Number of temporary files created per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - key

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ---------------- | ---------------------- | ----------------------------------- | ----- | -------------------------------- | ---------------------------- |
| KeyBlocksUnused | Number of unused blocks in the key cache | Number of unused blocks in the MyISAM key cache | Block(s)| InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyBlocksUsed | Number of used blocks in the key cache | Number of used blocks in the MyISAM key cache     | Block(s)    | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyReadRequests | Number of data block reads from the key cache | Number of times the MyISAM engine reads data blocks from the key cache | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyReads | Number of data block reads from the hard disk | Number of times the MyISAM engine reads data blocks from the hard disk per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyWriteRequests | Number of data block writes into the key cache   | Number of times the MyISAM engine writes data blocks into the key cache     | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| KeyWrites | Number of data block writes into the hard disk | Number of times the MyISAM engine writes data blocks into the hard disk per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - InnoDB row

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| -------------------- | ------------------------------- | ------------------------------- | ----- | ------------------------ | ---------------------------- |
| InnodbRowLockTimeAvg | Average time of locking a InnoDB row | Average time the InnoDB engine spends locking a row | ms | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowLockWaits | Number of InnoDB row lock waits | Number of times the InnoDB engine waits to lock a row per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowsDeleted | Number of deleted InnoDB rows | Number of rows deleted by the InnoDB engine per second | Row(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowsInserted | Number of inserted InnoDB rows | Number of rows inserted per second by the InnoDB engine | Row(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowsRead | Number of read InnoDB rows | Number of rows read per second by the InnoDB engine | Row(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbRowsUpdated | Number of updated InnoDB rows | Number of rows updated per second by the InnoDB engine | Row(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - InnoDB data

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ----------------- | --------------- | --------------------------------------- | ------- | -------------------------------- | ---------------------------- |
| InnodbDataReads | Volume of InnoDB data read | Number of bytes read per second by the InnoDB engine | B/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbDataReads | Number of InnoDB data reads | Number of data reads handled by the InnoDB engine | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbDataWrites | Total number of InnoDB data writes | Number of data writes processed per second by the InnoDB engine     | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbDataWritten | Volume of written InnoDB data | Number of data bytes written per second by the InnoDB engine | B/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - handler

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ------------------ | -------------- | ------------------------ | ----- | -------------------------------- | ---------------------------- |
| HandlerCommit | Number of internal commits | Number of transaction commits per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| HandlerReadRndNext | Number of read-next-row requests | Number of requests to read the next row per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| HandlerRollback | Number of internal rollbacks | Number of transaction rollbacks per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - buffer

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ---------------------------- | ----------------------- | --------------------------------------- | ----- | -------------------------------- | ---------------------------- |
| InnodbBufferPoolPagesFree    | Number of InnoDB blank pages            | Number of blank pages in the InnoDB buffer pool                 | Page(s) | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s |
| InnodbBufferPoolPagesTotal   | Total number of InnoDB pages          | Total number of memory pages taken up by the InnoDB engine | Page(s) | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbBufferPoolReadRequests | Number of times pages are pre-fetched into the InnoDB buffer pool | Number of logic read requests processed per second by the InnoDB engine | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| InnodbBufferPoolReads | Number of InnoDB physical reads | Number of physical read requests processed per second by the InnoDB engine | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - others

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ----------- | ---------- | -------------------- | ----- | -------------------------------- | ---------------------------- |
| LogCapacity | Log usage | Current log usage by the engine | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s        |
| OpenFiles | Number of opened files | Number of files opened by the engine | File(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - connection

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| -------------- | -------------- | -------------------------- | ---- | -------------------------------- | ---------------------------- |
| ThreadsCreated | Number of created threads | Number of threads created to process connections | Thread(s)| InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ThreadsRunning | Number of running threads | Number of running (non-idle) threads | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - access

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ----------- | ---------- | ------------ | ----- | -------------------------------- | ---------------------------- |
| ComCommit | Number of commits | Number of commits per second | Time(s)/sec | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| ComRollback | Number of rollbacks | Number of rollbacks per second | Time(s)/sec | InstanceId, InstanceType (optional) |5s, 60s, 300s, 3,600s, 86,400s |

### Engine (extended) - table

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ------------------- | ---------------- | ---------------------- | ---- | -------------------------------- | ---------------------------- |
| OpenedTables | Number of opened tables | Number of tables opened by the engine | Table(s) | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| TableLocksImmediate | Number of table locks released immediately | Number of table locks released immediately by the engine | Lock(s) | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |

### Deployment (replica)

| Metric    | Description   | Note                                                     | Unit  | Dimension                     | Monitoring Granularity                     |
| ----------------------- | ------------ | ---------------- | ----------------------------------- | -------------------------------- | ---------------------------- |
| MasterSlaveSyncDistance | Source-Replica delay (in MB) | Binlog difference between the source and replica | MB | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SecondsBehindMaster | Source-Replica delay (in seconds) | Synchronization delay in time between the source and replica | Seconds | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SlaveIoRunning          | IO thread status | IO thread status | Values: 0: Yes; 1: No; 2: Connecting | InstanceId, InstanceType (optional) | 5s, 60s, 300s, 3,600s, 86,400s |
| SlaveSqlRunning | SQL thread status | SQL thread status | Values: 0: Yes; 1: No   | InstanceId, InstanceTyp | 5s, 60s, 300s, 3,600s, 86,400s |

> ? Monitoring periods (`period`) may vary from metric to metric. You can get the periods different metrics support by calling the [`DescribeBaseMetrics`](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Dimension and Parameters

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | -------------------- | ------------------------------------------------------------ | -------------------------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | Database instance name                                         | Enter a string-type dimension name, e.g., `InstanceId`  |
| Instances.N.Dimensions.0.Value | InstanceId | Database ID                                              | Enter an instance ID, e.g., `cdb-ebul6659` |
| Instances.N.Dimensions.1.Name | InstanceType (optional) | Database instance type                                               | Enter a string-type dimension name, e.g., `InstanceType` |
| Instances.N.Dimensions.1.Value | InstanceType (optional) | Database instance type. Valid values: <br><li>1 (default): pulls monitored data from the instance's source node<br><li>2: pulls monitored data from the instance's replica node (only supported for single-node and two-node instances)<br><li>3: pulls monitored data from the read-only instance (the value of `InstanceId` must be a read-only instance ID; otherwise, the default value of 1 will be used)<br><li>4: pulls monitored data from the instance's second replica node (applicable only to Finance Edition instances) | Enter an instance type (optional). Default value: 1 |

> ? `InstanceType` description:
>
> - If the `InstanceId` value is a source instance ID, only `InstanceType` supports pulling the monitoring data of the source (value: 1), replica (value: 2), and second replica (value: 3).
> - If the `InstanceId` value is a source instance ID, the `InstanceType` value is 2 (replica), and the source instance has three nodes (one source and two replicas), then the monitoring data of one monitored node will be missing, as pulling replica monitoring data is supported only for single-node and two-node instances.
> - To pull the monitoring data of a read-only instance, pass in its ID as `InstanceId`.



## Input Parameters

**To query the monitored data of TencentDB for MySQL, use the following input parameters:**

&Namespace=QCE/CDB
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=Specific database ID 
&Instances.N.Dimensions.1.Name=InstanceType
&Instances.N.Dimensions.1.Value=Database instance type
