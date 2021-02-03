## Namespace

Namespace=QCE/PCX

## Monitoring Metrics

| Parameter | Metric | Description | Unit | Dimension |
| ------------ | ------------ | ---------------------------------------- | ----- | ------------------- |
| InBandwidth  | Network inbound bandwidth   | Inbound bandwidth of peering connection                           | bps   | peeringConnectionId |
| OutBandwidth | Network outbound bandwidth   | Outbound bandwidth of peering connection                           | bps   | peeringConnectionId |
| InPkg        | Inbound packets       | Number of inbound packets of peering connection per second                       | Packets/sec | peeringConnectionId |
| OutPkg       | Outbound packets       | Number of outbound packets of peering connection per second                       | Packets/sec | peeringConnectionId |
| PkgDrop      | Packet loss rate       | Ratio of packets dropped by peering connection due to bandwidth limit to the total packets | %     | peeringConnectionId |
| OutbandRate  | Outbound bandwidth utilization | Outbound bandwidth utilization of peering connection                     | %     | peeringConnectionId |
| InbandRate   | Inbound bandwidth utilization | Inbound bandwidth utilization of peering connection                     | %     | peeringConnectionId |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ------------------- | ------------------------------- | -------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | peeringConnectionId | Peering connection ID dimension name | Enter a String-type dimension name: peeringConnectionId       |
| Instances.N.Dimensions.0.Value | peeringConnectionId | Specific peering connection ID       | Enter a specific peering connection ID, such as `pcx-086ypwc8` |

## Input Parameter Description

**To query the monitoring data of a peering connection in a VPC, set the following input parameters:**
&Namespace=QCE/PCX
&Instances.N.Dimensions.0.Name=peeringConnectionId
&Instances.N.Dimensions.0.Value=peering connection ID
