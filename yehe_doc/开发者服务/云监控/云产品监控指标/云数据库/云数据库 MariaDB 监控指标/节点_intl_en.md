## Namespace

Namespace=QCE/MARIADB

## Monitoring Metrics
<escape>
<table style = "table-layout:fixed;">
<tr>
<th width="20%">Parameter</th>
<th width="20%">Metric</th>
<th width="20%">Description</th>
<th width="8%">Unit</th>
<th width="20%">Dimension</th>
<th width="12%">Statistical Period</th>
</tr>
<tr>
<td>ActiveThread<br>CountNode</td>
<td>Active Threads</td>
<td>Number of active threads in the thread pool on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogDiskAvailableNode</td>
<td>Available Binlog Disk Space</td>
<td>Available binlog disk space on the database node</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogUsedDiskNode</td>
<td>Used Binlog Disk Space</td>
<td>Used binlog disk space on the database node</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnUsageRateNode</td>
<td>Database Connection Utilization</td>
<td>Connection utilization on the database node, whose value is ThreadsConnected/ConnMax.</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>CpuUsageRateNode</td>
<td>CPU utilization</td>
<td>Node CPU utilization</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDisk<br>AvailableNode</td>
<td>Available Data Disk Space</td>
<td>Available data disk space on the database node</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDisk<br>UsedRateNode</td>
<td>Data Disk Utilization</td>
<td>Data disk utilization on the database node</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DeleteTotalNode</td>
<td>DELETE Requests</td>
<td>Number of DELETE requests on the database node</td>
<td>Counts/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>IOUsageRateNode</td>
<td>IO Utilization</td>
<td>IO utilization of the database node</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBuffer<br>PoolReadsNode</td>
<td>Logical Reads from InnoDB Disk</td>
<td>Number of logical reads from InnoDB disk on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadAheadNode</td>
<td>Pages Read into InnoDB Buffer Pool by read-ahead Thread</td>
<td>Number of pages read into InnoDB buffer pool by read-ahead thread on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadRequestsNode</td>
<td>Logical Reads from InnoDB Buffer Pool</td>
<td>Number of logical reads from InnoDB buffer pool on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>DeletedNode</td>
<td>Rows Deleted from InnoDB Tables</td>
<td>Number of rows deleted from InnoDB tables on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>InsertedNode</td>
<td>Rows Inserted into InnoDB Tables</td>
<td>Number of rows inserted into InnoDB tables on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>ReadNode</td>
<td>Rows Read from InnoDB Tables</td>
<td>Number of rows read from InnoDB on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRows<br>UpdatedNode</td>
<td>Rows Updated to InnoDB Tables</td>
<td>Number of rows updated to InnoDB Tables on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InsertTotalNode</td>
<td>INSERT Requests</td>
<td>Number of INSERT requests on the database node</td>
<td>Counts/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>LongQuery<br>CountNode</td>
<td>Slow Queries</td>
<td>Number of slow queries on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemAvailableNode</td>
<td>Available Cache Space</td>
<td>Available cache space on the database node</td>
<td>GB</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemHitRateNode</td>
<td>Buffer Cache Hit Ratio</td>
<td>Buffer cache hit ratio on the database node</td>
<td>%</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceSelect<br>TotalNode</td>
<td>REPLACE_SELECT Requests</td>
<td>Number of REPLACE_SELECT requests on the database node</td>
<td>Counts/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceTotalNode</td>
<td>REPLACE Requests</td>
<td>Number of REPLACE requests on the database node</td>
<td>Counts/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>RequestTotalNode</td>
<td>DML Throughput</td>
<td>Total number of requests on the database node</td>
<td>Counts/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SelectTotalNode</td>
<td>SELECT Requests</td>
<td>Number of SELECT requests on the database node</td>
<td>Counts/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SlaveDelayNode</td>
<td>Replica Node Delay</td>
<td>Replica node delay on the database node</td>
<td>Sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>UpdateTotalNode</td>
<td>UPDATE Requests</td>
<td>Number of UPDATE requests on the database node</td>
<td>Counts/sec</td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>Threads<br>ConnectedNode</td>
<td>Open Connections</td>
<td>Number of connections to the database node, which is the number of sessions obtained using the SHOW PROCESSLIST statement</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnMaxNode</td>
<td>Max Connections</td>
<td>Maximum number of connections to the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>IsMaster</td>
<td>Whether to Be Primary Node</td>
<td>Whether the database node is a primary database node</td>
<td>-</td>
<td>InstanceId,<br>NodeId</td>
<td>60s</td>
</tr>
<tr>
<td>ThreadsRunningCountNode</td>
<td>Running Threads</td>
<td>Value of Threads_running on the database node</td>
<td> - </td>
<td>InstanceId,<br>NodeId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
</table>
</escape>

> ?Statistical periods (`period`) may vary by metric. You can get the periods different metrics support by calling the [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Overview of Parameters in Each Dimension
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Dimension Name</th>
<th>Dimension Description</th>
<th>Format</th>
</tr>
</thead>
<tbody><tr>
<td>Instances.N.Dimensions.0.Name</td>
<td>InstanceId</td>
<td>Dimension name of the instance ID</td>
<td>Enter a string-type dimension name: InstanceId</td>
</tr>
<tr>
<td>Instances.N.Dimensions.0.Value</td>
<td>InstanceId</td>
<td>Specific instance ID</td>
<td>Enter a specific instance ID, such as tdsql-9kjauqq1</td>
</tr>
<tr>
<td>Instances.N.Dimensions.0.Name</td>
<td>NodeId</td>
<td>Dimension name of the node ID</td>
<td>Enter a string-type dimension name: NodeId.</td>
</tr>
<tr>
<td>Instances.N.Dimensions.0.Value</td>
<td>NodeId</td>
<td>Specific node ID</td>
<td>Enter a specific node ID, such as 877adc0ada3e</td>
</tr>
</tbody></table>

## Input Parameter Description

To query the node-level monitoring metrics of TencentDB for MariaDB, use the following input parameters:

&Namespace=QCE/MARIADB
&Instances.N.Dimensions.0.Name= InstanceId
&Instances.N.Dimensions.0.Value=Instance ID
&Instances.N.Dimensions.1.Name=NodeId
&Instances.N.Dimensions.1.Value=Specific node ID
