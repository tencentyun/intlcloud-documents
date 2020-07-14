## Namespace
Namespace=QCE/TCAPLUS

## Monitoring Metrics
| Parameter | Metric Name | Description | Unit | Dimension |
| ------------- | ----- | ---- | ---- | ---- |
| Avgerror | Average error rate | Average error proportion of table operations | % | TableInstanceId and ClusterId |
| WriteLatency | Average write latency | Error proportion of common table operations | ms | TableInstanceId and ClusterId |
| Comerror | Common error rate | Actually read capacity units for tables | % | TableInstanceId and ClusterId |
| ReadLatency | Average read latency | Average data read latency | ms | TableInstanceId and ClusterId |
| Volume | Storage volume | System error proportion | KB | TableInstanceId and ClusterId |
| Syserror | System error rate | Storage capacity occupied by tables | % | TableInstanceId and ClusterId |
| Writecu | Actual write capacity units | Average write data latency | Units/sec | TableInstanceId and ClusterId |
| Readcu | Actual read capacity units | Actual write capacity units for tables | Units/sec | TableInstanceId and ClusterId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | TableInstanceId | Dimension name of the database instance ID | Enter a string-type dimension name, such as TableInstanceId |
| Instances.N.Dimensions.0.Value | TableInstanceId | A specific database instance ID | Enter a specific database instance ID, such as tcaplus-123abc456 |
| Instances.N.Dimensions.1.Name | ClusterId | Dimension name of the cluster ID | Enter a string-type dimension name, such as clusterId |
| Instances.N.Dimensions.1.Value | ClusterId | A specific cluster ID | Enter a specific cluster ID, such as clus-12345 |

## Input Parameters

To query the monitoring data of TcaplusDB, use the following input parameters:
&Namespace=QCE/TCAPLUS
&Instances.N.Dimensions.0.Name=TableInstanceId
&Instances.N.Dimensions.0.Value=<Specific database ID>
&Instances.N.Dimensions.1.Name=ClusterId
&Instances.N.Dimensions.1.Value=<Specific cluster ID>
