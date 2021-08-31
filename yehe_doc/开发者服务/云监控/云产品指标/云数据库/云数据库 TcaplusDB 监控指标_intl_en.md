## Namespace
Namespace=QCE/TCAPLUS

## Monitoring Metrics
| Parameter | Metric | Description | Unit | Dimension |
| ------------- | ----- | ---- | ---- | ---- |
| Avgerror | Average error rate | Average error proportion of table operations | % | TableInstanceId, ClusterId |
| Writelatency | Average write latency | Average data write latency | Microsecond | TableInstanceId, ClusterId |
| Comerror | Common error rate | Error proportion of common table operations | % | TableInstanceId, ClusterId |
| Readlatency | Average read latency | Average data read latency | Microsecond | TableInstanceId, ClusterId |
| Volume | Storage volume | Storage volume used by tables | KB | TableInstanceId, ClusterId |
| Syserror | System error rate | System error proportion | % | TableInstanceId, ClusterId |
| Writecu | Actual write capacity units | Actual write capacity units for tables | Units/sec | TableInstanceId, ClusterId |
| Readcu | Actual read capacity units | Actual read capacity units for tables | Units/sec | TableInstanceId, ClusterId |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | TableInstanceId | Database instance ID dimension name | Enter a string-type dimension name: TableInstanceId |
| Instances.N.Dimensions.0.Value | TableInstanceId | Specific database instance ID | Enter a specific database instance ID, such as `tcaplus-123abc456` |
| Instances.N.Dimensions.1.Name | ClusterId | Cluster ID dimension name | Enter a string-type dimension name: clusterId |
| Instances.N.Dimensions.1.Value | ClusterId | Specific cluster ID | Enter a specific cluster ID, such as `clus-12345` |

## Input Parameter Description

**To query the monitoring data of TcaplusDB, set the following input parameters:**
&Namespace=QCE/TCAPLUS
&Instances.N.Dimensions.0.Name=TableInstanceId
&Instances.N.Dimensions.0.Value=Specific database ID
&Instances.N.Dimensions.1.Name=ClusterId
&Instances.N.Dimensions.1.Value=Specific cluster ID
