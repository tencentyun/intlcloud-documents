## Namespace


Namespace=QCE/DCG


## Monitoring Metrics

| Parameter | Metric | Description | Unit | Dimension |
| ------------ | ---------- | ------------------ | ----- | ---------------------- |
| InBandwidth | Network inbound bandwidth | Network inbound bandwidth of Direct Connect | Mbps | directConnectGatewayId |
| InPkg | Inbound packets | Inbound packets of Direct Connect | Packets/sec | directConnectGatewayId |
| OutBandwidth | Network outbound bandwidth | Network outbound bandwidth of Direct Connect | Mbps | directConnectGatewayId |
| OutPkg | Outbound packets | Outbound packets of Direct Connect | Packets/sec | directConnectGatewayId |
| Rxbytes | Inbound traffic | Inbound traffic of Direct Connect | GB | directConnectGatewayId |
| Txbytes | Outbound traffic | Outbound traffic of Direct Connect | GB | directConnectGatewayId |


> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description          | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | directConnectGatewayId | Direct Connect gateway ID dimension name | Enter a String-type dimension name: directConnectGatewayId |
| Instances.N.Dimensions.0.Value | directConnectGatewayId | Specific Direct Connect gateway ID | Enter a specific Direct Connect gateway ID: dcg-4d545d |

## Input Parameter Description

**To query the monitoring data of a Direct Connect gateway in a VPC, set the following input parameters:**
&Namespace=QCE/DCG
&Instances.N.Dimensions.0.Name=directConnectGatewayId
&Instances.N.Dimensions.0.Value=Direct Connect gateway ID
