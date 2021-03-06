## Namespace

Namespace=QCE/TDMYSQL

## Monitoring Metrics
<table style = "table-layout:fixed;">
<thead>
<tr>
<th width="20%">Metric</th>
<th width="20%">Meaning</th>
<th width="20%">Description</th>
<th width="8%">Unit</th>
<th width="20%">Dimension</th>
<th width="12%">Statistical Periods</th>
</tr>
</thead>
<tbody><tr>
<td>ActiveThreadCount</td>
<td>Number of active threads</td>
<td>Instance-level metric, which is the sum of active threads in all the shards’ primary and replica nodes</td>
<td>Threads</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogDiskAvailable</td>
<td>Available binlog disk space</td>
<td>Instance-level metric, which is the sum of the value of `BinlogDiskAvailableShard` in all the shards</td>
<td>GB</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogUsedDisk</td>
<td>Used binlog disk space</td>
<td>Instance-level metric, whose value is the sum of binlog disk space used in all the shards’ primary nodes</td>
<td>GB</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnUsageRate</td>
<td>Connection usage</td>
<td>Instance-level metric, whose value is the highest connection usage among all the shards’ primary and replica nodes</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>CpuUsageRate</td>
<td>CPU usage</td>
<td>Instance-level metric, whose value is the highest CPU usage in all the shards’ primary nodes</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDiskAvailable</td>
<td>Available data disk space</td>
<td>Instance-level metric, which is the sum of the available data disk space in all the shards’ primary nodes</td>
<td>GB</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDiskUsedRate</td>
<td>Data disk usage</td>
<td>Instance-level metric, whose value is the highest data disk usage in all the shards’ primary nodes</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DeleteTotal</td>
<td>Number of DELETE queries</td>
<td>Instance-level metric, which is the sum of DELETE queries executed in all the shards’ primary nodes</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPoolReads</td>
<td>Number of InnoDB disk page reads</td>
<td>Instance-level metric, which is the sum of InnoDB disk page reads in all the shards’ primary and replica nodes</td>
<td>Times</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadAhead</td>
<td>Page read-ahead count of the InnoDB buffer pool</td>
<td>Instance-level metric, which is the sum of page read-aheads in the InnoDB buffer pool in all the shards’ primary and replica nodes</td>
<td>Times</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadRequests</td>
<td>Page read count of the InnoDB buffer pool </td>
<td>Instance-level metric, which is the sum of page reads in the InnoDB buffer pool in the instance's primary and replica nodes</td>
<td>Times</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRowsDeleted</td>
<td>Number of rows deleted by InnoDB</td>
<td>Instance-level metric, which is the sum of rows deleted by InnoDB in all the shards’ primary nodes</td>
<td>Rows</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRowsInserted</td>
<td>Number of rows inserted by InnoDB</td>
<td>Instance-level metric, which is the sum of rows inserted by InnoDB in all the shards’ primary nodes</td>
<td>Rows</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRowsRead</td>
<td>Number of rows read by InnoDB</td>
<td>Instance-level metric, which is the sum of rows read by InnoDB in all the shards’ primary and replica nodes</td>
<td>Rows</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRowsUpdated</td>
<td>Number of rows updated by InnoDB</td>
<td>Instance-level metric, which is the sum of rows updated by InnoDB in all the shards’ primary nodes</td>
<td>Rows</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InsertTotal</td>
<td>Number of INSERT queries</td>
<td>Instance-level metric, which is the sum of INSERT queries executed in all the shards’ primary nodes</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>LongQueryCount</td>
<td>Slow queries</td>
<td>Instance-level metric, which is the sum of slow queries executed in all the shards’ primary nodes</td>
<td>Queries</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemAvailable</td>
<td>Available memory</td>
<td>Instance-level metric, which is the sum of available memory in all the shards’ primary nodes</td>
<td>GB</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemHitRate</td>
<td>Cache hit ratio</td>
<td>Instance-level metric, whose value is the lowest cache hit ratio in all the shards’ primary nodes</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceSelectTotal</td>
<td>Number of REPLACE_SELECT queries</td>
<td>Instance-level metric, which is the sum of REPLACE-SELECT queries executed in all the shards’ primary nodes</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceTotal</td>
<td>Number of REPLACE queries</td>
<td>Instance-level metric, which is the sum of REPLACE queries executed in all the shards’ primary nodes</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>RequestTotal</td>
<td>Total requests</td>
<td>Instance-level metric, which is the total number of queries executed in the instance's primary node plus the number of SELECT queries executed in the replica nodes</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SelectTotal</td>
<td>Number of SELECT queries</td>
<td>Instance-level metric, which is the sum of SELECT queries executed in all the shards’ primary and replica nodes</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SlaveDelay</td>
<td>Primary-replica synchronization delay</td>
<td>Instance-level metric. Instance-level synchronization delay is the delay of whichever shard has the longest delay, and shard-level synchronization delay is the shortest delay among the shard’s all replica nodes.</td>
<td>Sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>UpdateTotal</td>
<td>Number of UPDATE queries</td>
<td>Instance-level metric, which is the sum of UPDATE queries executed in all the shards’ primary nodes</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ThreadsConnected</td>
<td>Number of threads currently connected</td>
<td>Instance-level metric, which is the sum of threads currently connected in all the shards’ primary and replica nodes</td>
<td>Threads</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnMax</td>
<td>Maximum connections</td>
<td>Instance-level metric, which is the sum of the maximum number of connections of all the shards’ primary and replica nodes</td>
<td>Connections</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ClientConnTotal</td>
<td>Number of client connections</td>
<td>Instance-level metric, which is the sum of connections in the instance’s proxy. This metric represents the actual number of clients connected to the database instance.</td>
<td>Connections</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SQLTotal</td>
<td>Total number of SQL queries</td>
<td>Instance-level metric, which represents the number of SQL queries sent to the instance</td>
<td>Queries</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ErrorSQLTotal</td>
<td>SQL error count</td>
<td>Instance-level metric, which represents the number of queries with execution errors</td>
<td>Queries</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SuccessSQLTotal</td>
<td>Number of successful SQL queries</td>
<td>Instance-level metric, which represents the number of SQL queries executed successfully</td>
<td>Queries</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>TimeRange0</td>
<td>Number of queries that take shorter than 5 ms to execute</td>
<td>Instance-level metric, which represents the number of queries that take shorter than 5 ms to execute</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>TimeRange1</td>
<td>Number of queries that take 5-20 ms to execute</td>
<td>Instance-level metric, which represents the number of queries that take 5-20 ms to execute</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>TimeRange2</td>
<td>Number of queries that take 20-30 ms to execute</td>
<td>Instance-level metric, which represents the number of queries that take 20-30 ms to execute</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>TimeRange3</td>
<td>Number of queries that take longer than 30 ms to execute</td>
<td>Instance-level metric, which represents the number of queries that take longer than 30 ms to execute</td>
<td>Queries/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MasterSwitchedTotal</td>
<td>Number of primary node switchovers</td>
<td>Instance-level metric, which represents the number of times the primary node is switched</td>
<td>Times</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>IOUsageRate</td>
<td>IO usage</td>
<td>Instance-level metric, whose value is the highest IO usage in all the shards’ primary nodes</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
</tbody></table>

> ?Statistical periods (period) may vary from metric to metric. You can get the periods different metrics support by calling the `DescribeBaseMetrics` API.

## Dimensions and Parameters

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------- | ------------------ | ------------------------------------- |
| Instances.N.Dimensions.0.Name | instanceId | Dimension name of the instance ID | Enter a string-type dimension name: `InstanceId`  |
| Instances.N.Dimensions.0.Value | InstanceId | Instance ID | Enter an instance ID, e.g. `tdsqlshard-9kjauqq1` |

## Input Parameters

To query the instance-level monitoring metrics of TDSQL for MySQL, use the following input parameters:

&Namespace=QCE/TDMYSQL
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=ID of the instance
