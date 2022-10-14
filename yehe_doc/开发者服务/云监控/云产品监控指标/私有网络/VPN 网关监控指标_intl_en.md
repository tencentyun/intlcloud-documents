## Namespace

Namespace = QCE/VPNGW


## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ---------- | ---------- | --------------------- | ----- | ------- |
| InBandwidth  | Public network inbound bandwidth | The average inbound traffic of the VPN gateway per second   | Mbps  | vpnGwId |
| OutBandwidth  | Public network outbound bandwidth | The average outbound traffic of the VPN gateway per second   | Mbps  | vpnGwId |
| Inpkg      | Inbound packets     | The average number of inbound packets of the VPN gateway per second | Count/sec | vpnGwId |
| Outpkg      | Outbound packets     | The average number of outbound packets of the VPN gateway per second | Count/sec | vpnGwId |
| VpnBandwidthUsageRate    | VPN bandwidth utilization     |  The VPN bandwidth utilization  | %| vpnGwId |


> ?Statistical periods (`period`) may vary by metric. You can get the statistical periods for different metrics by calling the [`DescribeBaseMetrics`](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Dimensions and Parameters

| Parameter | Dimension | Description | Format |
| ------------------------------ | -------- | --------------------- | ---------------------------------------- |
| Instances.N.Dimensions.0.Name  | vpnGwId  | Dimension name of the VPN gateway ID | enter a string-type dimension name: vpnGwId         |
| Instances.N.Dimensions.0.Value | vpnGwId  | Specific VPN gateway ID       | Enter a specific VPN gateway ID, such as `vpngw-q7v069tf` |

## Input Parameters

To query the monitoring data of a VPN gateway in VPC, use the following input parameters:
&Namespace=QCE/VPNGW
&Instances.N.Dimensions.0.Name=vpnGwId
&Instances.N.Dimensions.0.Value=VPN gateway ID

