## Namespace

Namespace=QCE/POSTGRES

## Monitoring Metrics


| Parameter | Metric Name | Description | Unit | Dimension |
| --------------------- | ------------ | ---- |---- | --------------------- |
| Connections | Number of connections | Historical trend of an instance’s number of active connections | Count | resourceId |
| Cpu | CPU utilization | CPU utilization of an instance. The CPU utilization may be greater than 100% due to the use of flexible CPU limitation policies during the idle period | % | resourceId |
| HitPercent | Buffer cache hit rate | Data cache hit rate | % | resourceId |
| InFlow | Inbound traffic | Inbound traffic for instance read/write | KB/s | resourceId |
| OutFlow | Outbound traffic | Outbound traffic for instance read/write | KB/s | resourceId |
| Iops | Disk IOPS | Instance IOPS (requests per second) | Times/sec | resourceId |
| Memory | Memory usage | Disk storage space occupied by the instance | KB | resourceId |
| OtherCalls | Number of other requests | Total number of requests other than read and write requests (such as Drop requests), which is accumulated by minute | Times/min | resourceId |
| Qps | Number of queries per second | Number of queries per second | Times/sec | resourceId |
| WriteCalls | Number of write requests | Total number of write requests per minute | Times/min | resourceId |
| ReadCalls | Number of read requests | Total number of read requests per minute | Times/min | resourceId |
| ReadWriteCalls | Number of read and write requests | Total number of read and write requests (including Create/Read/Update/Delete (CRUD) requests) per minute | Times/min | resourceId |
| RemainXid | Number of remaining XIDs | Number of remaining Transaction IDs. There are a maximum of 2^32 Transaction IDs. We recommend that you run "vacuum full" manually if the number of Transaction IDs is less than 1,000,000 | Count | resourceId |
| SqlRuntimeAvg | Average execution latency | Average execution time of all SQL requests, excluding SQL requests in transactions | ms | resourceld |
| SqlRuntimeMax | Top-10 maximum execution latency | Average value of the top-10 maximum execution times for SQL requests | ms | resourceId |
| SqlRuntimeMin | Top-10 minimum execution latency | Average value of the top-10 minimum execution times for SQL requests | ms | resourceId |
| Storage | Used storage space | Storage capacity used for instances | resourceId |
| XlogDiff | Xlog synchronization difference between the Master and the Slave | Sampling per minute. The Xlog synchronization difference between the Master and the Slave reflects the synchronization latency. Therefore, the smaller the Xlog synchronization difference is, the better the performance of the Master/Slave will be | Byte | resourceId |
| SlowQueryCnt | Slow queries | Number of queries with a query time greater than the specified time (1s by default) | Count | resourceId |
| StorageRate | Storage space utilization | Storage space utilization of the instance | % | resourceId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | resourceId | Dimension name of the resourceId | Enter a string-type dimension name, such as resourceId |
| Instances.N.Dimensions.0.Value | resourceId | A specific instance resourceId | Enter a specific instance resourceId, such as postgres-123456 |


## Input Parameters

To query the monitoring data of PostgreSQL, use the following input parameters:
&Namespace=QCE/POSTGRES
&Instances.N.Dimensions.0.Name=resourceId
&Instances.N.Dimensions.0.Value=<Instance resourceId> 
