## Namespace

Namespace=QCE/NAT_GATEWAY

## Monitoring Metrics

| Metric Name | Description | Unit | Dimension |
| ------------ | ----- | ---- | ----------- |
| Outbandwidth | Public network outbound bandwidth | Mbps | natId |
| Inbandwidth | Public network inbound bandwidth | Mbps | natId |
| Outpkg | Outbound packets | Packets/sec | natId |
| Inpkg | Inbound packets | Packets/sec | natId |
| Conns | Connections | Connections/sec | natId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | natId | Dimension name of the NAT gateway ID | Enter a string-type natId dimension name |
| Instances.N.Dimensions.0.Value | natId | A specific NAT gateway ID | Enter a specific `natId`, such as nat-4d545d |

## Input Parameters

To query the monitoring data of a NAT gateway in a VPC instance, use the following input parameters:
&Namespace=QCE/NAT_GATEWAY
&Instances.N.Dimensions.0.Name=natId
&Instances.N.Dimensions.0.Value=<NAT gateway ID>

