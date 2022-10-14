
## Namespace

Namespace = QCE/VPNX

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ------------ | ------------- | ----------------------- | ----- | --------- |
| OutBandwidth | VPN tunnel outbound bandwidth | The average outbound traffic of the VPN tunnel per second   | Mbps  | vpnConnId |
| InBandwidth  | VPN tunnel inbound bandwidth | The average inbound traffic of the VPN tunnel per second   | Mbps  | vpnConnId |
| InPkg        | VPN tunnel inbound packets | The average number of inbound packets of the VPN tunnel per second   | Count/sec | vpnConnId |
| OutPkg       | VPN tunnel outbound packets | The average number of outbound packets of the VPN tunnel per second   | Count/sec | vpnConnId |
| PkgDrop      | VPN tunnel packet loss | The percentage of lost VPN detection packets per minute | %     | vpnConnId |
| Delay        | VPN tunnel delay   | The average VPN detection delay per minute | ms    | vpnConnId |

> ?Statistical periods (`period`) may vary by metric. You can get the statistical periods for different metrics by calling the [`DescribeBaseMetrics`](https://intl.cloud.tencent.com/document/product/248/33882) API.


## Dimensions and Parameters

| Parameter | Dimension | Description | Format |
| ------------------------------ | --------- | -------------------- | ---------------------------------------- |
| Instances.N.Dimensions.0.Name  | vpnConnId | Dimension name of the VPN tunnel ID | Enter a string-type dimension name: vpnConnId       |
| Instances.N.Dimensions.0.Value | vpnConnId | Specific VPN tunnel ID       | Enter a specific VPN tunnel ID, such as `vpnx-12345678` |

## Input Parameters

**To query the monitoring data of a VPN tunnel in a VPC, use the following input parameters:**
&Namespace=QCE/VPNX
&Instances.N.Dimensions.0.Name=vpnConnId
&Instances.N.Dimensions.0.Value=VPN tunnel ID

