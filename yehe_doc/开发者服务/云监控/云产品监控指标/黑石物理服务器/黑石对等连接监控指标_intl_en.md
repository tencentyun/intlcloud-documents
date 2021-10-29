## Namespace

Namespace=QCE/BM_PCX



## Monitoring Metrics

| Metric | Description | Unit | Dimension |
| :----------- | :--------- | :---- | :------------------ |
| OutBandwidth | Public network outbound bandwidth | Mbps | peeringConnectionId |
| InBandwidth | Public network inbound bandwidth | Mbps | peeringConnectionId |
| OutPkg | Public network outbound packets | Packets/sec | peeringConnectionId |
| InPkg | Public network inbound packets | Packets/sec | peeringConnectionId |

> ? The statistical granularity (`period`) may vary by metrics. You can obtain the `period` supported by each metric by calling the [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API.

## Overview of parameters in each dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ------------------- | ---------------------------- | ------------------------------------------- |
| Instances.N.Dimensions.0.Name | peeringConnectionId | Dimension name of the unique ID of the BM peering connection | Enter a string-type dimension name, such as peeringConnectionId |
| Instances.N.Dimensions.0.Value | peeringConnectionId | Unique ID of the BM peering connection | Enter a specific ID of the BM peering connection, such as pcx-test |

## Input Parameters

To query the monitoring data of BM peering connection, configure input parameters as follows:

&Namespace=QCE/BM_PCX
&Instances.N.Dimensions.0.Name=peeringConnectionId
&Instances.N.Dimensions.0.Value=<Unique ID of the BM peering connection>
