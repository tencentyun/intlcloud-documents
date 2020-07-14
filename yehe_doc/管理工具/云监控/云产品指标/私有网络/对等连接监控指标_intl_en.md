## Namespace

Namespace=QCE/PCX

## Monitoring Metrics

| Metric Name | Description | Unit | Dimension |
| ------------ | ---------- | ----- | ------------------- |
| Inpkg | Inbound packets | Packets/second | peeringConnectionId |
| Inbandwidth | Inbound bandwidth | Mbps | peeringConnectionId |
| Outpkg | Outbound packets | Packets/second | peeringConnectionId |
| Outbandwidth | Outbound bandwidth | Mbps | peeringConnectionId |
| Pkgdrop | Packet loss rate | % | peeringConnectionId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ------------------- | ------------------------------- | -------------------------------------------------- |
| Instances.N.Dimensions.0.Name | peeringConnectionId | Dimension name of the peering connection ID | Enter a string-type peeringConnectionId dimension name |
| Instances.N.Dimensions.0.Value | peeringConnectionId | A specific peering connection ID | Enter a specific peering connection ID, such as pcx-086ypwc8 |

## Input Parameters

To query the monitoring data of a peering connection in a VPC instance, use the following input parameters:
&Namespace=QCE/PCX
&Instances.N.Dimensions.0.Name=peeringConnectionId
&Instances.N.Dimensions.0.Value=<Peering connection ID>
