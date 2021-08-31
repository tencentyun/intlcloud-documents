## Namespace

Namespace=QCE/BWP

## Monitoring Metrics

| Parameter | Metric | Description | Unit | Dimension |
| ---------- | ---------- | ---------------- | ----- | ------------------ |
| InPkg      | Inbound packets     | Inbound packets of bandwidth package | Packets/sec | bandwidthPackageId |
| InTraffic  | Inbound bandwidth     | Inbound bandwidth of bandwidth package | Mbps  | bandwidthPackageId |
| OutPkg     | Outbound packets     |  Outbound packets of bandwidth package | Packets/sec | bandwidthPackageId |
| OutTraffic | Outbound bandwidth     | Outbound bandwidth of bandwidth package | Mbps  | bandwidthPackageId |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ------------------ | ------------------- | ------------------------------------------- |
| Instances.N.Dimensions.0.Name  | bandwidthPackageId | Bandwidth package ID dimension name | Enter a String-type dimension name: bandwidthPackageId |
| Instances.N.Dimensions.0.Value | bandwidthPackageId | Specific bandwidth package ID     | Enter a specific bandwidth package ID, such as `pdcg-4d545d`        |

## Input Parameter Description

**To query the monitoring data of a bandwidth package in a VPC, set the following input parameters:**
&Namespace=QCE/BWP
&Instances.N.Dimensions.0.Name=bandwidthPackageId
&Instances.N.Dimensions.0.Value=unique bandwidth package ID
