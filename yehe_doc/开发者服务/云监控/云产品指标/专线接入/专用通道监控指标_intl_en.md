## Namespace

Namespace=QCE/DCX

## Monitoring Metrics

| Parameter | Metric | Description | Unit | Dimension |
| ----- | ---------- | ---- | ------------ | ------------ |
| InBandwidth | Network inbound bandwidth   | Inbound bandwidth from the access point AR to the VPC, which is collected once every one or five minutes       | Mbps |directConnectConnId |
|OutBandwidth | Network outbound bandwidth | Outbound bandwidth from the VPC to the access point AR, which is collected once every one or five minutes       | Mbps   | directConnectConnId |
|InPkg| Inbound packets | Number of inbound packets of the current dedicated tunnel      | Packets/sec |directConnectConnId |
|OutPkg| Outbound packets |   Number of outbound packets of the current dedicated tunnel   | Packets/sec |directConnectConnId |

>?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
|---------|---------|---------|---------|
| Instances.N.Dimensions.0.Name	| directConnectConnId	| Dedicated tunnel ID dimension name	| Enter a String-type dimension name: directConnectConnId |
| Instances.N.Dimensions.0.Value| directConnectConnId |Specific dedicated tunnel ID |Enter a specific dedicated tunnel ID, such as `dc-e1h9wqp8` |

## Input Parameter Description

**To query the monitoring data of a dedicated tunnel, set the following input parameters:**
&Namespace=QCE/DCX
&Instances.N.Dimensions.0.Name=directConnectConnId
&Instances.N.Dimensions.0.Value=Dedicated tunnel ID 
