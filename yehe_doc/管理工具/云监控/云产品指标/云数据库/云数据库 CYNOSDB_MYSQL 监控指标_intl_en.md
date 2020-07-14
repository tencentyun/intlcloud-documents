
## Namespace

Namespace=QCE/CYNOSDB_MYSQL

## Monitoring Metrics

| Parameter | Metric Name | Unit | Dimension |
| ----------------------------- | -------------- | ------ | ------ |
| BytesReceived | Private inbound traffic | MB/% | InstanceId |
| BytesSent | Private outbound traffic | MB/% | Instanceld |
| ComDelete | Deletions | Times/sec | InstanceId |
| ComInsert | Insertions | Times/sec | InstanceId |
| CountSelect | Queries | Times/sec | InstanceId |
| ComUpdate | Updates | Times/sec | InstanceId |
| CpuUsageRate | CPU utilization | % | InstanceId |
| DbConnections | Number of connections | Count | InstanceId |
| MemoryUse | Memory usage | MB | InstanceId |
| Qps | Number of requests | Times/sec | InstanceId |
| StorageUsage | Storage usage | GB | InstanceId |
| Tps | Transactions per second | Times/sec | InstanceId |
| CacheHitRate | Cache hit rate | % | InstanceId |
| CacheHits | Cache hits | Times | InstanceId |
| DataVolumeUsage | Data tablespace usage | GB | Instanceld |
| DataVolumeAllocate | Allocated data tablespace capacity | GB | InstanceId |
| MaxConnections | Maximum number of connections | Times | InstanceId |
| UndoVolumeAllocate | Allocated undo tablespace capacity | GB | InstanceId |
| UndoVolumeUsage | Usage of the undo tablespace | GB | Instanceld |
| TmpVolumeAllocate | Allocated temporary tablespace capacity | GB | Instanceld |
| TmpVolumeUsage | Temporary tablespace usage | GB | Instanceld |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | InstanceId | Dimension name of the database instance ID | Enter a string-type dimension name, such as InstanceId |
| Instances.N.Dimensions.0.Value | InstanceId | A specific database instance ID | Enter a specific database instance ID, such as cynosdbmysql-ins-12ab34cd |

## Input Parameters

To query the monitoring data of TencentDB for CynosDB, use the following input parameters:
&Namespace=QCE/CYNOSDB_MYSQL
&Instances.N.Dimensions.0.Name=InstanceId
&Instances.N.Dimensions.0.Value=<Specific CynosDB instance ID> 

