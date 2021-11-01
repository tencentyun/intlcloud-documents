## Namespace

Namespace=QCE/QAAP

## Monitoring Metrics
| Metric | Description | Unit | Dimension |
| --- | --- | --- | --- |
| Connum | Concurrent connections | Count | channelId |
| Inbandwidth | Inbound bandwidth | Mbps | channelId |
| Outbandwidth | Outbound bandwidth | Mbps | channelId |
| InPackets | Inbound packets | Packets/sec | channelId |
| OutPackets | Outbound packets | Packets/sec | channelId |
| PacketLoss | Packet loss rate | % | channelId |
| Latency | Latency | ms | channelId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | --------- | --------------------- | ---------------------------------------- |
| Instances.N.Dimensions.0.Name | channelId | Dimension name of the acceleration connection ID | Enter a string-type dimension name, such as channelId |
| Instances.N.Dimensions.0.Value | channelId | A specific acceleration connection ID | Enter a specific acceleration connection ID, such as link-abcd1234 |


## Input Parameters

To query the load monitoring data of a GAAP connection, use the following input parameters:

&Namespace=QCE/QAAP
&Instances.N.Dimensions.0.Name=channelId 
&Instances.N.Dimensions.0.Value=<Channel ID>
