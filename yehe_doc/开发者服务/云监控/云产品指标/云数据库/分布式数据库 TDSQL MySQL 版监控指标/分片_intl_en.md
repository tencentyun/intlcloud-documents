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
<td>CpuUsageRateShard</td>
<td>CPU usage</td>
<td>Shard-level metric, whose value is the CPU usage of the shard’s primary node</td>
<td>%</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDisk<br>AvailableShard</td>
<td>Available data disk space</td>
<td>Shard-level metric, whose value is the available data disk space in the shard’s primary node</td>
<td>GB</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDiskUsed<br>RateShard</td>
<td>Data disk usage</td>
<td>Shard-level metric, whose value is the data disk space usage in the shard’s primary node</td>
<td>%</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DeleteTotalShard</td>
<td>Number of DELETE queries</td>
<td>Shard-level metric, whose value is the number of DELETE queries in the shard’s primary node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>IOUsageRateShard</td>
<td>IO usage</td>
<td>Shard-level metric, whose value is the IO usage of the shard’s primary node</td>
<td>%</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadsShard</td>
<td>Number of InnoDB disk page reads</td>
<td>Shard-level metric, which is the sum of InnoDB disk page reads in the shard’s primary and replica nodes</td>
<td>Times</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadAheadShard</td>
<td>Page read-ahead count of the InnoDB buffer pool</td>
<td>Shard-level metric, which is the sum of page read-aheads in the InnoDB buffer pool in the shard’s primary and replica nodes</td>
<td>Times</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadRequestsShard</td>
<td>Page read count of the InnoDB buffer pool </td>
<td>Shard-level metric, which is the sum of page reads in the InnoDB buffer pool in the shard’s primary and replica nodes</td>
<td>Times</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>DeletedShard</td>
<td>Number of rows deleted by InnoDB</td>
<td>Shard-level metric, whose value is the number of rows deleted by InnoDB in the shard’s primary node</td>
<td>Rows</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>InsertedShard</td>
<td>Number of rows inserted by InnoDB</td>
<td>Shard-level metric, whose value is the number of rows inserted by InnoDB in the shard’s primary node</td>
<td>Rows</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRowsReadShard</td>
<td>Number of rows read by InnoDB</td>
<td>Shard-level metric, which is the sum of rows read by InnoDB in the shard’s primary and replica nodes</td>
<td>Rows</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>UpdatedShard</td>
<td>Number of rows updated by InnoDB</td>
<td>Shard-level metric, whose value is the number of rows updated by InnoDB in the shard’s primary node</td>
<td>Rows</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InsertTotalShard</td>
<td>Number of INSERT queries</td> 
<td>Shard-level metric, whose value is the number of INSERT queries executed in the shard’s primary node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>LongQueryCountShard</td>
<td>Slow queries</td>
<td>Shard-level metric, whose value is the number of slow queries in the shard’s primary node</td>
<td>Queries</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MasterSwitched<br>TotalShard</td>
<td>Number of primary node switchovers</td>
<td>Shard-level metric, which represents the number of times the primary node is switched in the shard</td>
<td>Times</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemAvailableShard</td>
<td>Available memory</td>
<td>Shard-level metric, whose value is the available memory in the shard’s primary node</td>
<td>GB</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemHitRateShard</td>
<td>Cache hit ratio</td>
<td>Shard-level metric, whose value is the cache hit ratio of the shard’s primary node</td>
<td>%</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceSelect<br>TotalShard</td>
<td>Number of REPLACE_SELECT queries</td>
<td>Shard-level metric, whose value is the number of REPLACE_SELECT queries executed in the shard’s primary node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceTotalShard</td>
<td>Number of REPLACE queries</td>
<td>Shard-level metric, whose value is the number of REPLACE queries executed in the shard’s primary node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>RequestTotalShard</td>
<td>Total number of queries</td>
<td>Shard-level metric, which is the total number of queries executed in the shard’s primary node plus the number of SELECT queries executed in the replica nodes</td>
<td>Queries/sec</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SelectTotalShard</td>
<td>Number of SELECT queries</td>
<td>Shard-level metric, which is the sum of SELECT queries executed in the shard’s primary and replica nodes</td>
<td>Queries/sec</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SlaveDelayShard</td>
<td>Primary-replica synchronization delay</td>
<td>Shard-level metric, whose value is the shortest primary-replica synchronization delay among the shard’s replica nodes</td>
<td>Sec</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ThreadsConnected<br>Shard</td>
<td>Number of threads currently connected</td>
<td>Shard-level metric, which is the sum of threads connected in the shard’s primary and replica nodes</td>
<td>Threads</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>UpdateTotalShard</td>
<td>Number of UPDATE queries</td>
<td>Shard-level metric, whose value is the number of UPDATE queries executed in the shard’s primary node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ActiveThread<br>CountShard</td>
<td>Number of active threads</td>
<td>Shard-level metric, which is the sum of active threads in the shard’s primary and replica nodes</td>
<td>Threads</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogDisk<br>AvailableShard</td>
<td>Available binlog disk space</td>
<td>Shard-level metric, whose value is the smallest available binlog disk space among the shard’s primary and replica nodes</td>
<td>GB</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogUsedDiskShard</td>
<td>Used binlog disk space</td>
<td>Shard-level metric, whose value is the binlog disk space used in the shard’s primary node</td>
<td>GB</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnMaxShard</td>
<td>Maximum number of connections</td>
<td>Shard-level metric, whose value is the sum of the maximum number of connections of the shard’s primary and replica nodes</td>
<td>Connections</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnUsageRateShard</td>
<td>Connection usage</td>
<td>Shard-level metric, whose value is the highest connection usage among the shard’s primary and replica nodes</td>
<td>%</td>
<td>InstanceId,<br>ShardId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
</tbody></table>

> ?Statistical periods (period) may vary from metric to metric. You can get the periods different metrics support by calling the `DescribeBaseMetrics` API.

## Dimension and Parameters

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------- | ------------------ | ------------------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | Dimension name of the instance | Enter a string-type dimension name: `InstanceId` |
| Instances.N.Dimensions.0.Value | InstanceId | Instance ID | Enter an instance ID, e.g. `tdsqlshard-9kjauqq1` |
| Instances.N.Dimensions.1.Name | ShardId | Dimension name of the shard | Enter a string-type dimension name: `ShardId`|
| Instances.N.Dimensions.1.Value | ShardId    | Shard ID         | Enter a shard ID, e.g., `shard-i6f4sf12`.     |

## Input Parameters

To query the shard-level monitoring metrics of TDSQL for MySQL, use the following input parameters:

&Namespace=QCE/TDMYSQL
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=Instance ID
&Instances.N.Dimensions.1.Name=ShardId
&Instances.N.Dimensions.1.Value=Shard ID
