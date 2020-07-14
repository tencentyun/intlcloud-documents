## Namespace

Namespace=QCE/BWP

## Monitoring Metrics

| Metric Name | Description | Unit | Dimension |
| ------------ | ----- | ---- | ---------------------- |
| OutTraffic | Public network outbound bandwidth | Mbps | bandwidthPackageId |
| InTraffic | Public network inbound bandwidth | Mbps | bandwidthPackageId |
| Outpkg | Outbound packets | Packets/sec | bandwidthPackageId |
| Inpkg | Inbound packets | Packets/sec | bandwidthPackageId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ------------------ | ------------------- | ------------------------------------------- |
| Instances.N.Dimensions.0.Name | bandwidthPackageId | Dimension name of the bandwidth package ID | Enter a string-type bandwidthPackageId dimension name |
| Instances.N.Dimensions.0.Value | bandwidthPackageId | A specific bandwidth package ID | Enter a specific bandwidth package ID, such as pdcg-4d545d |

## Input Parameters

To query the monitoring data of a bandwidth package in a VPC instance, use the following input parameters:
&Namespace=QCE/BWP
&Instances.N.Dimensions.0.Name=bandwidthPackageId
&Instances.N.Dimensions.0.Value=<Unique bandwidth package ID>
