## Namespace

Namespace=QCE/VPNGW


## Monitoring Metrics

| Parameter | Metric | Description | Unit | Dimension |
| ---------- | ---------- | --------------------- | ----- | ------- |
| Intraffic  | Public network inbound bandwidth | Inbound bandwidth of VPN gateway per second | Mbps  | vpnGwId |
| Outtraffic | Public network outbound bandwidth | Outbound bandwidth of VPN gateway per second | Mbps  | vpnGwId |
| Inpkg      | Inbound packets     | Inbound packets of VPN gateway per second | Packets/sec | vpnGwId |
| Outpkg     | Outbound packets     | Outbound packets of VPN gateway per second | Packets/sec | vpnGwId |


> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | -------- | --------------------- | ---------------------------------------- |
| Instances.N.Dimensions.0.Name  | vpnGwId  | VPN gateway ID dimension name | Enter a String-type dimension name: vpnGwId         |
| Instances.N.Dimensions.0.Value | vpnGwId  | Specific VPN gateway ID       | Enter a specific VPN gateway ID, such as `vpngw-q7v069tf` |

## Input Parameter Description

To query the monitoring data of a VPN gateway in a VPC, set the following input parameters:
&Namespace=QCE/VPNGW
&Instances.N.Dimensions.0.Name=vpnGwId
&Instances.N.Dimensions.0.Value=VPN gateway ID

