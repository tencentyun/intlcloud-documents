## Namespace

Namespace=QCE/LB

## Monitoring Metrics

| Metric Name | Description | Unit | Dimension |
| -------------- | ---------- | ----- | ---- |
| VipOuttraffic | Public network outbound bandwidth | Mbps | EIP |
| VipIntraffic | Public network inbound bandwidth | Mbps | EIP |
| VipOutpkg | Outbound packets | Packets/sec | EIP |
| VipInpkg | Inbound packets | Packets/sec | EIP |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | -------- | --------------------- | ------------------------------------ |
| Instances.N.Dimensions.0.Name | eip | EIP dimension name | Enter a string-type eip dimension name |
| Instances.N.Dimensions.0.Value | eip | A specific EIP | Enter a specific EIP, such as 111.111.111.11 |

## Input Parameters

To query the monitoring data of an EIP in a VPC instance, use the following input parameters:
&Namespace=QCE/LB
&Instances.N.Dimensions.0.Name=eip
&Instances.N.Dimensions.0.Value=<Unique EIP ID>
