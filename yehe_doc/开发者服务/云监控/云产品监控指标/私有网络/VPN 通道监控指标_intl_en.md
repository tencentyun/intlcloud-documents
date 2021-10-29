## Namespace

Namespace=QCE/VPNX

## Monitoring Metrics

| Metric Name | Description | Unit | Dimension |
| ------------ | ---------- | ------ | --------- |
| Outbandwidth | Public network outbound bandwidth | Mbps | vpnConnId |
| Inbandwidth | Public network inbound bandwidth | Mbps | vpnConnId |
| Outpkg | Outbound packets | Packets/sec | vpnConnId |
| Inpkg | Inbound packets | Packets/sec | vpnConnId |
| Pkgdrop | Packet loss rate | % | vpnConnId |
| Delay | Latency | Seconds | vpnConnId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.


## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | --------- | -------------------- | ---------------------------------------- |
| Instances.N.Dimensions.0.Name | vpnConnId | Dimension name of the VPN tunnel ID | Enter a string-type vpnConnId dimension name |
| Instances.N.Dimensions.0.Value | vpnConnId | A specific VPN tunnel ID | Enter a specific VPN connection ID, such as vpnx-12345678 |

## Input Parameters

To query the monitoring data of a VPN tunnel in a VPC instance, use the following input parameters:
&Namespace=QCE/VPNX
&Instances.N.Dimensions.0.Name=vpnConnId
&Instances.N.Dimensions.0.Value=<VPN tunnel ID>
