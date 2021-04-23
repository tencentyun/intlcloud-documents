## Namespace

Namespace=QCE/MARIADB

## Monitoring Metrics
<escape>
<table style = "table-layout:fixed;">
<tr>
<th width="20%">Metric</th>
<th width="20%">Meaning</th>
<th width="20%">Description</th>
<th width="8%">Unit</th>
<th width="20%">Dimension</th>
<th width="12%">Statistical Periods</th>
</tr>
<tr>
<td>ActiveThread<br>CountNode</td>
<td>Number of active threads</td>
<td>Number of active threads in the thread pool of the node</td>
<td>Threads</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogDiskAvailableNode</td>
<td>Available binlog disk space</td>
<td>Available binlog disk space in the node</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogUsedDiskNode</td>
<td>Used binlog disk space</td>
<td>Used binlog disk space in the node</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnUsageRateNode</td>
<td>Connection utilization</td>
<td>Connection usage in the node, whose value is ThreadsConnected/ConnMax.</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>CpuUsageRateNode</td>
<td>CPU usage</td>
<td>CPU usage of the node</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDisk<br>AvailableNode</td>
<td>Available data disk space</td>
<td>Available data disk space in the node</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDisk<br>UsedRateNode</td>
<td>Data disk usage</td>
<td>Data disk usage in the node</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DeleteTotalNode</td>
<td>Number of DELETE queries</td>
<td>Number of DELETE queries executed in the node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>IOUsageRateNode</td>
<td>IO usage</td>
<td>IO usage of the node</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBuffer<br>PoolReadsNode</td>
<td>Number of InnoDB disk page reads</td>
<td>Number of InnoDB disk page reads in the node</td>
<td>Times</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadAheadNode</td>
<td>Page read-ahead count of the InnoDB buffer pool</td>
<td>Number of read-aheads in the InnoDB buffer pool of the node</td>
<td>Times</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadRequestsNode</td>
<td>Page read count of the InnoDB buffer pool</td>
<td>Number of page reads in the InnoDB buffer pool of the node</td>
<td>Times</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>DeletedNode</td>
<td>Number of rows deleted by InnoDB</td>
<td>Number of rows deleted by InnoDB in the node</td>
<td>Rows</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>InsertedNode</td>
<td>Number of rows inserted by InnoDB</td>
<td>Number of rows inserted by InnoDB in the node</td>
<td>Rows</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>ReadNode</td>
<td>Number of rows read by InnoDB</td>
<td>Number of rows read by InnoDB in the node</td>
<td>Rows</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>UpdatedNode</td>
<td>Number of rows updated by InnoDB</td>
<td>Number of rows updated by InnoDB in the node</td>
<td>Rows</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InsertTotalNode</td>
<td>Number of INSERT queries</td>
<td>Number of INSERT queries executed in the node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>LongQuery<br>CountNode</td>
<td>Slow queries</td>
<td>Number of slow queries in the node</td>
<td>Queries</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemAvailableNode</td>
<td>Available memory</td>
<td>Available memory in the node</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemHitRateNode</td>
<td>Cache hit ratio</td>
<td>Cache hit ratio in the node</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceSelect<br>TotalNode</td>
<td>Number of REPLACE_SELECT queries</td>
<td>Number of REPLACE_SELECT queries executed in the node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceTotalNode</td>
<td>Number of REPLACE queries</td>
<td>Number of REPLACE queries executed in the node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>RequestTotalNode</td>
<td>Total number of requests</td>
<td>Total number of requests executed in the node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SelectTotalNode</td>
<td>Number of SELECT queries</td>
<td>Number of SELECT queries executed in the node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SlaveDelayNode</td>
<td>Primary-replica synchronization delay</td>
<td>Primary-replica synchronization delay of the node</td>
<td>Sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>UpdateTotalNode</td>
<td>Number of UPDATE queries</td>
<td>Number of UPDATE queries executed in the node</td>
<td>Queries/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>Threads<br>ConnectedNode</td>
<td>Number of threads currently connected</td>
<td>Number of threads currently connected, which is the number of sessions obtained using the SHOW PROCESSLIST statement</td>
<td>Threads</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnMaxNode</td>
<td>Maximum number of connections</td>
<td>Maximum number of connections allowed by the node</td>
<td>Connections</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>IsMaster</td>
<td>Whether the node is a primary database</td>
<td>Whether the node is a primary database</td>
<td>-</td>
<td>InstanceId,<br>NodeId</td>
<td>60s</td>
</tr>
</table>
</escape>

> ?Statistical periods (Period) may vary from metric to metric. You can get the periods different metrics support by calling the `DescribeBaseMetrics` API.

## Dimensions and Parameters
<table>
<thead>
<tr>
<th>Parameter Name</th>
<th>Dimension Name</th>
<th>Dimension Description</th>
<th>Format</th>
</tr>
</thead>
<tbody><tr>
<td>Instances.N.Dimensions.0.Name</td>
<td>InstanceId</td>
<td>Dimension name of the instance</td>
<td>Enter a string-type dimension name: InstanceId.</td>
</tr>
<tr>
<td>Instances.N.Dimensions.0.Value</td>
<td>InstanceId</td>
<td>Instance ID</td>
<td>Enter an instance ID, e.g., tdsql-9kjauqq1.</td>
</tr>
<tr>
<td>Instances.N.Dimensions.0.Name</td>
<td>NodeId</td>
<td>Dimension name of the node</td>
<td>Enter a string-type dimension name: NodeId.</td>
</tr>
<tr>
<td>Instances.N.Dimensions.0.Value</td>
<td>NodeId</td>
<td>Node ID</td>
<td>Enter a node ID, e.g., 877adc0ada3e.</td>
</tr>
</tbody></table>

## Input Parameters

To query the node-level monitoring metrics of TencentDB for MariaDB, use the following input parameters:

&Namespace=QCE/MARIADB
&Instances.N.Dimensions.0.Name= InstanceId
&Instances.N.Dimensions.0.Value=Instance ID
&Instances.N.Dimensions.1.Name=NodeId
&Instances.N.Dimensions.1.Value=Node ID
