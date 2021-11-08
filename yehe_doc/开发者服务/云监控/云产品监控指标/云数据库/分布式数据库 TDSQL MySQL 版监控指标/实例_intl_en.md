## Namespace

Namespace=QCE/TDMYSQL

## Monitoring Metrics
<table style = "table-layout:fixed;">
<thead>
<tr>
<th width="20%">Parameter</th>
<th width="20%">Metric</th>
<th width="20%">Description</th>
<th width="8%">Unit</th>
<th width="20%">Dimension</th>
<th width="12%">Statistical Period</th>
</tr>
</thead>
<tbody><tr>
<td>ActiveThreadCount</td>
<td>Active Threads</td>
<td>Instance-Level metric, which is the sum of active threads on source and replica nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogDiskAvailable</td>
<td>Available Binlog Disk Space</td>
<td>Instance-Level metric, which is the sum of the values of `BinlogDiskAvailableShard` in all shards</td>
<td>GB</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>BinlogUsedDisk</td>
<td>Used Binlog Disk Space</td>
<td>Instance-Level metric, which is the sum of binlog disk space used on source nodes in all shards</td>
<td>GB</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnUsageRate</td>
<td>Database Connection Utilization</td>
<td>Instance-Level metric, whose value is the highest database connection utilization of the instance's source and replica nodes in all shards</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>CpuUsageRate</td>
<td>CPU utilization</td>
<td>Instance-Level metric, whose value is the highest CPU utilization of the instance's source nodes in all shards</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDiskAvailable</td>
<td>Available Data Disk Space</td>
<td>Instance-Level metric, which is the sum of the available data disk space on source nodes in all shards</td>
<td>GB</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DataDiskUsedRate</td>
<td>Data Disk Utilization</td>
<td>Instance-Level metric, whose value is the highest data disk utilization of the instance's source nodes in all shards</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>DeleteTotal</td>
<td>DELETE Requests</td>
<td>Instance-Level metric, which is the sum of DELETE requests on the instance's source nodes in all shards</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPoolReads</td>
<td>Logical Reads from InnoDB Disk</td>
<td>Instance-Level metric, which is the sum of logical reads from InnoDB disks on the instance's source and replica nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadAhead</td>
<td>Pages Read into InnoDB Buffer Pool by read-ahead Thread</td>
<td>Instance-Level metric, which is the sum of pages read into InnoDB buffer pools by read-ahead thread on the instance's source and replica nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbBufferPool<br>ReadRequests</td>
<td>Logical Reads from InnoDB Buffer Pool</td>
<td>Instance-Level metric, which is the sum of logical reads from InnoDB buffer pools on the instance's source and replica nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRowsDeleted</td>
<td>Rows Deleted from InnoDB Tables</td>
<td>Instance-Level metric, which is the sum of rows deleted from InnoDB tables on the instance's source nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRowsInserted</td>
<td>Rows Inserted into InnoDB Tables</td>
<td>Instance-Level metric, which is the sum of rows inserted into InnoDB tables on the instance's source nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRowsRead</td>
<td>Rows Read from InnoDB Tables</td>
<td>Instance-Level metric, which is the sum of rows read from InnoDB tables on the instance's source and replica nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InnodbRowsUpdated</td>
<td>Rows Updated to InnoDB Tables</td>
<td>Instance-Level metric, which is the sum of rows updated to InnoDB tables on the instance's source nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>InsertTotal</td>
<td>INSERT Requests</td>
<td>Instance-Level metric, which is the sum of INSERT requests on the instance's source nodes in all shards</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>LongQueryCount</td>
<td>Slow Queries</td>
<td>Instance-Level metric, which is the sum of slow queries on the instance's source nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemAvailable</td>
<td>Available Cache</td>
<td>Instance-Level metric, which is the sum of available cache space on the instance's source nodes in all shards</td>
<td>GB</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MemHitRate</td>
<td>Cache Hit Ratio</td>
<td>Instance-Level metric, whose value is the smallest cache hit ratio of the instance's source nodes in all shards</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceSelectTotal</td>
<td>REPLACE_SELECT Requests</td>
<td>Instance-Level metric, which is the sum of REPLACE-SELECT requests on the instance's source nodes in all shards</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ReplaceTotal</td>
<td>REPLACE Requests</td>
<td>Instance-Level metric, which is the sum of REPLACE requests on the instance's source nodes in all shards</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>RequestTotal</td>
<td>DML Throughput</td>
<td>Instance-Level metric, which is the sum of total number of requests on the instance's all source nodes and the number of SELECT requests on all replica nodes</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SelectTotal</td>
<td>SELECT Requests</td>
<td>Instance-Level metric, which is the sum of SELECT requests on the instance's source and replica nodes in all shards</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SlaveDelay</td>
<td>Replica Node Delay</td>
<td>Instance-Level metric. The replica node delay of each shard is calculated first, and the greatest value is taken as the instance's replica node delay. The replica node delay of a shard is the smallest replica node delay of all replica nodes in the shard</td>
<td>Sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>UpdateTotal</td>
<td>UPDATE Requests</td>
<td>Instance-Level metric, which is the sum of UPDATE requests on the instance's source nodes in all shards</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ThreadsConnected</td>
<td>Open Connections</td>
<td>Instance-Level metric, whose value is the sum of open connections to the instance's source and replica nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ConnMax</td>
<td>Max Connections</td>
<td>Instance-Level metric, which is the sum of maximum connections to the instance's source and replica nodes in all shards</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ClientConnTotal</td>
<td>Total Client Connections</td>
<td>Instance-Level metric, which is the sum of connections to the instance's proxy. This metric represents the actual number of clients connected to the database instance.</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SQLTotal</td>
<td>SQL Throughput</td>
<td>Instance-Level metric, which represents the number of SQL statements sent to the instance</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>ErrorSQLTotal</td>
<td>SQL Error Throughput</td>
<td>Instance-Level metric, which represents the number of SQL statements with execution errors</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>SuccessSQLTotal</td>
<td>SQL Success Throughput</td>
<td>Instance-Level metric, which represents the number of SQL statements executed successfully</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>TimeRange0</td>
<td>DML Latency (below 5 ms)</td>
<td>Instance-Level metric, which represents the number of requests that take less than 5 ms to execute</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>TimeRange1</td>
<td>DML Latency (5-20 ms)</td>
<td>Instance-Level metric, which represents the number of requests that take 5-20 ms to execute</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>TimeRange2</td>
<td>DML Latency (20-30 ms)</td>
<td>Instance-Level metric, which represents the number of requests that take 20-30 ms to execute</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>TimeRange3</td>
<td>DML Latency (over 30 ms)</td>
<td>Instance-Level metric, which represents the number of requests that take more than 30 ms to execute</td>
<td>Counts/sec</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MasterSwitchedTotal</td>
<td>Source-Replica Switches</td>
<td>Instance-Level metric, which represents the number of source-replica switches in the instance</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>IOUsageRate</td>
<td>IO Utilization</td>
<td>Instance-Level metric, whose value is the highest IO utilization of the instance's source nodes in all shards</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<tr>
<td>MaxSlaveCpuUsageRate</td>
<td>Max CPU Utilization of Replica Node</td>
<td>Instance-Level metric, whose value is the highest CPU utilization of all replica nodes</td>
<td>%</td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
<td>ThreadsRunningCount</td>
<td>Total Running Threads</td>
<td>Instance-Level metric, whose value is the sum of Threads_running values of the instance's all nodes. Threads_running is the result of running `show status like 'Threads_running'`</td>
<td> - </td>
<td>InstanceId</td>
<td>60s, 300s, 3600s, 86400s</td>
</tr>
</tbody></table>

> ?Statistical periods (`period`) may vary by metric. You can get the periods different metrics support by calling the [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ---------- | ------------------ | ------------------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | Dimension name of the instance ID | Enter a string-type dimension name: InstanceId |
| Instances.N.Dimensions.0.Value | InstanceId | Specific instance ID | Enter an instance ID, such as tdsqlshard-9kjauqq1 |

## Input Parameter Description

To query the instance-level monitoring metrics of TDSQL for MySQL, use the following input parameters:

&Namespace=QCE/TDMYSQL
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=Instance ID
