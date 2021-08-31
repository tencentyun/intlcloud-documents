## Namespace

Namespace=QCE/CES

## Monitoring Metrics

| Parameter | Metric Name | Calculation Method | Description | Unit | Dimension | Statistical Granularity (Period) |
| ---------------------------------- | -------------------------- | -------------------------------------------------------- | ------------------------------------ | ------- | ----------- | ------------------ |
| Status | Cluster health status | Latest status of the ES cluster in the statistical period | Cluster health status: 0: green, 1: yellow, 2: red | - | uInstanceId | 60 secs and 300 secs |
| DiskUsageAvg | Average disk usage | Average disk usage of each node in the ES cluster in the statistical period | Average disk usage of each node in the ES cluster | % | uInstanceId | 60 secs and 300 secs |
| DiskUsageMax | Maximum disk usage | Maximum disk usage of each node in the ES cluster in the statistical period | Maximum disk usage of each node in the ES cluster | % | uInstanceId | 60 secs and 300 secs |
| JvmMemUsageAvg | Average JVM memory usage | Average JVM memory usage of each node in the ES cluster in the statistical period | Average JVM memory usage of each node in the ES cluster | % | uInstanceId | 60 secs and 300 secs |
| JvmMemUsageMax | Maximum JVM memory usage | Maximum JVM memory usage of each node in the ES cluster in the statistical period | Maximum JVM memory usage of each node in the ES cluster | % | uInstanceId | 60 secs and 300 secs |
| JvmOldMemUsageAvg | Average JVM old memory usage | Average JVM old memory usage of each node in the ES cluster in the statistical period | Average JVM old memory usage of each node in the ES cluster | % | uInstanceId | 60 secs and 300 secs |
| JvmOldMemUsageMax | Maximum JVM old memory usage | Maximum JVM old memory usage of each node in the ES cluster in the statistical period | Maximum JVM old memory usage of each node in the ES cluster | % | uInstanceId | 60 secs and 300 secs |
| CpuUsageAvg | Average CPU utilization | Average CPU utilization of each node in the ES cluster in the statistical period | Average CPU utilization of each node in the ES cluster | % | uInstanceId | 60 secs and 300 secs |
| CpuUsageMax | Maximum CPU utilization | Maximum CPU utilization of each node in the ES cluster in the statistical period | Maximum CPU utilization of each node in the ES cluster | % | uInstanceId | 60 secs and 300 secs |
| CpuLoad1minAvg | Average CPU load of the cluster per minute | Average CPU load per minute of each node in the ES cluster in the statistical period | Average CPU load per minute of each node in the ES cluster | - | uInstanceId | 60 secs and 300 secs |
| CpuLoad1minMax | Maximum CPU load of the cluster per minute | Maximum CPU load per minute of each node in the ES cluster in the statistical period | Maximum CPU load per minute of each node in the ES cluster | - | uInstanceId | 60 secs and 300 secs |
| IndexLatencyAvg | Average write latency | Average write latency of the ES cluster in the statistical period | Average write latency of the ES cluster | ms | uInstanceId | 60 secs and 300 secs |
| IndexLatencyMax | Maximum write latency | Maximum write latency of the ES cluster in the statistical period | Maximum write latency of the ES cluster | ms | uInstanceId | 60 secs and 300 secs |
| SearchLatencyAvg | Average query latency | Average query latency of the ES cluster in the statistical period | Average query latency of the ES cluster | ms | uInstanceId | 60 secs and 300 secs |
| SearchLatencyMax | Maximum query latency | Maximum query latency of the ES cluster in the statistical period | Maximum query latency of the ES cluster | ms | uInstanceId | 60 secs and 300 secs |
| IndexSpeed | Write speed | Average write speed of the ES cluster in the statistical period | Average write speed of the ES cluster | Times/sec | uInstanceId | 60 secs and 300 secs |
| SearchCompletedSpeed | Query speed | Average query speed of the ES cluster in the statistical period | Average query speed of the ES cluster | Times/sec | uInstanceId | 60 secs and 300 secs |
| BulkRejected<br>CompletedPercent | Bulk rejection rate | Percentage of rejected bulk operations to all bulk operations in the ES cluster in the statistical period | Percentage of rejected bulk operations to all bulk operations | % | uInstanceId | 60 secs and 300 secs |
| SearchRejected<br>CompletedPercent | Query rejection rate | Percentage of rejected query operations to all query operations in the ES cluster in the statistical period | Percentage of rejected query operations to all query operations | % | uInstanceId | 60 secs and 300 secs |
| IndexDocs | Total number of documents | Average of the total number of documents in the ES cluster in the statistical period | Total number of documents in the ES cluster | Count | uInstanceId | 60 secs and 300 secs |
| AutoSnapshotStatus | Execution status of the automatic backup task in the ES cluster | Status of the last executed automatic backup task in the ES cluster in the statistical period | Execution status of the automatic backup task in the ES cluster | - | uInstanceId | 300 secs |

>?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ----------- | ------------------- | ----------------------------------- |
| Instances.N.Dimensions.0.Name | uInstanceId | Dimension name of the ES instance ID | Enter a string-type dimension name, such as uInstanceId |
| Instances.N.Dimensions.0.Value | uInstanceId | A specific ES instance ID | Enter a specific instance ID, such as es-example |

## Input Parameters

To query the monitoring data of the Elasticsearch Service, use the following input parameters:
&Namespace=QCE/CES
&Instances.N.Dimensions.0.Name=uInstanceId
&Instances.N.Dimensions.0.Value=Specific ES instance ID
