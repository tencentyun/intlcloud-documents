## Namespace


Namespace=QCE/DCG


## Monitoring Metrics

| Metric Name | Description | Unit | Dimension |
| ------------ | ---------- | ----- | ---------------------- |
| Outbandwidth | Public network outbound bandwidth | Mbps | directConnectGatewayId |
| Inbandwidth | Public network inbound bandwidth | Mbps | directConnectGatewayId |
| Outpkg | Outbound packets | Packets/sec | directConnectGatewayId |
| Inpkg | Inbound packets | Packets/sec | directConnectGatewayId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | directConnectGatewayId | Dimension name of the direct connect gateway ID | Enter a string-type directConnectGatewayId dimension name |
| Instances.N.Dimensions.0.Value | directConnectGatewayId | A specific ID of the direct connect gateway | Enter a specific direct connect gateway ID, such as dcg-4d545d |

## Input Parameters

To query the monitoring data of a direct connect gateway in a VPC instance, use the following input parameters:
&Namespace=QCE/DCG
&Instances.N.Dimensions.0.Name=directConnectGatewayId
&Instances.N.Dimensions.0.Value=<Direct connect gateway ID>
