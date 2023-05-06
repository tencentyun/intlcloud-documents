## Namespace

Namespace=QCE/POSTGRES

## Monitoring Metrics


<table>
<thead>
<tr>
<th>Parameter</th>
<th>Metric</th>
<th>Description</th>
<th>Unit</th>
<th>Dimension</th>
</tr>
</thead>
<tbody><tr>
<td>Connections</td>
<td>Connections</td>
<td>Historical trend of active connections to the instance</td>
<td> - </td>
<td>resourceId</td>
</tr>
<tr>
<td>Cpu</td>
<td>CPU utilization</td>
<td>Instance CPU utilization. Due to the flexible CPU limit policy adopted during idle time, the CPU utilization may be above 100%</td>
<td>%</td>
<td>resourceId</td>
</tr>
<tr>
<td>HitPercent</td>
<td>Buffer cache hit rate</td>
<td>Data cache hit rate</td>
<td>%</td>
<td>resourceId</td>
</tr>
<tr>
<td>Memory</td>
<td>Memory usage</td>
<td>Available memory space used by the instance</td>
<td>KB</td>
<td>resourceId</td>
</tr>
<tr>
<td>OtherCalls</td>
<td>Other requests</td>
<td>Total number of requests (such as DROP) other than reads and writes accumulated by the minute</td>
<td nowrap="nowrap">Requests/min</td>
<td>resourceId</td>
</tr>
<tr>
<td>Qps</td>
<td>Queries per second</td>
<td>Number of queries per second</td>
<td>Queries/sec</td>
<td>resourceId</td>
</tr>
<tr>
<td>WriteCalls</td>
<td>Write requests</td>
<td>Total number of write requests per minute</td>
<td>Requests/min</td>
<td>resourceId</td>
</tr>
<tr>
<td>ReadCalls</td>
<td>Read requests</td>
<td>Total number of read requests per minute</td>
<td>Requests/min</td>
<td>resourceId</td>
</tr>
<tr>
<td>ReadWriteCalls</td>
<td>Read and write requests</td>
<td>Total number of read and write (CRUD) requests per minute</td>
<td>Requests/min</td>
<td>resourceId</td>
</tr>
<tr>
<td>RemainXid</td>
<td>Remaining XIDs</td>
<td>Number of remaining transaction IDs. Maximum number: 2^32. If this value is below 1000000, we recommend you manually run `vacuum full`</td>
<td> - </td>
<td>resourceId</td>
</tr>
<tr>
<td>SqlRuntimeAvg</td>
<td>Average execution latency</td>
<td>Average execution time of all SQL requests, excluding SQL requests in transactions</td>
<td>Ms</td>
<td>resourceId</td>
</tr>
<tr>
<td>SqlRuntimeMax</td>
<td>Top 10 longest execution latency</td>
<td>Average execution time of the top 10 most time-consuming SQL requests</td>
<td>Ms</td>
<td>resourceId</td>
</tr>
<tr>
<td>SqlRuntimeMin</td>
<td>Top 10 shortest execution latency</td>
<td>Average execution time of the top 10 least time-consuming SQL requests</td>
<td>Ms</td>
<td>resourceId</td>
</tr>
<tr>
<td>Storage</td>
<td>Used storage space</td>
<td>Storage capacity used by the instance</td>
<td>GB</td>
<td>resourceId</td>
</tr>
<tr>
<td>XlogDiff</td>
<td>Primary/Secondary xlog sync delay</td>
<td>Primary/Secondary xlog sync delay sampled once per minute. The smaller, the better</td>
<td>Byte</td>
<td>resourceId</td>
</tr>
<tr>
<td>SlowQueryCnt</td>
<td>Slow queries</td>
<td>Number of queries that take more than the specified time (1s by default) to be executed</td>
<td> - </td>
<td>resourceId</td>
</tr>
<tr>
<td>StorageRate</td>
<td>Storage space utilization</td>
<td>Storage space utilization of the instance</td>
<td>%</td>
<td>resourceId</td>
</tr>
</tbody></table>



> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description          | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name  | resourceId              | `resourceId` dimension name   | Enter a String-type dimension name: resourceId         |
| Instances.N.Dimensions.0.Value | resourceId              | Specific instance `resourceId`       | Enter a specific instance `resourceId`, such as postgres-123456       |


## Input Parameter Description

To query the monitoring data of a TencentDB for PostgreSQL instance, use the following input parameters:
&Namespace=QCE/POSTGRES
&Instances.N.Dimensions.0.Name=resourceId
&Instances.N.Dimensions.0.Value=resourceId 
