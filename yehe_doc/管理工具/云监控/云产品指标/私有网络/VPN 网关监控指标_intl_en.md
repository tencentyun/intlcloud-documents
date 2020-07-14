## Namespace

Namespace=QCE/VPNGW


## Monitoring Metrics

| Metric Name | Description | Unit | Dimension |
| ------------ | ---------- | ----- | ------- |
| Outbandwidth | Public network outbound bandwidth | Mbps | vpnGwId |
| Inbandwidth | Public network inbound bandwidth | Mbps | vpnGwId |
| Outpkg | Outbound packets | Packets/sec | vpnGwId |
| Inpkg | Inbound packets | Packets/sec | vpnGwId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | -------- | --------------------- | ---------------------------------------- |
| Instances.N.Dimensions.0.Name | vpnGwId | Dimension name of the VPN gateway ID | Enter a string-type vpnGwId dimension name |
| Instances.N.Dimensions.0.Value | vpnGwId | A specific VPN gateway ID | Enter a specific VPN gateway ID, such as vpngw-q7v069tf |

## Input Parameters

To query the monitoring data of a VPN gateway in a VPC instance, use the following input parameters:
&Namespace=QCE/VPNGW
&Instances.N.Dimensions.0.Name=vpnGwId
&Instances.N.Dimensions.0.Value=<VPN gateway ID>

