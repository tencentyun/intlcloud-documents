## Namespace
Namespace= QCE/DCX

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ----- | ---------- | ---- | ------------ | ------------ |
|InBandwidth | Network inbound bandwidth | Bandwidth rate from the access point AR toward the VPC instance, which indicates the inbound bandwidth data collected every one minute or five minutes | Mbps | directConnectConnId |
| OutBandwidth | Newtork outbound bandwidth | Bandwidth rate from the VPC toward the access point AR, which indicates the outbound bandwidth data collected every one minute or five minutes | Mbps | directConnectConnId |
| OutPkg | Outbound packets | Outbound packets for the current dedicated tunnel | Count | directConnectConnId |
| InPkg | Inbound packets | Inbound packets for the current dedicated tunnel | % | directConnectConnId |

>? The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
|---------|---------|---------|---------|
| Instances.N.Dimensions.0.Name | directConnectConnId | Dimension name of the dedicated tunnel ID | Enter a string-type dimension name, such as directConnectConnId |
| Instances.N.Dimensions.0.Value | directConnectConnId | A specific dedicated tunnel ID | Enter a specific dedicated tunnel ID, such as dc-e1h9wqp8 |

## Input Parameters

**To query the monitoring data of a dedicated tunnel, use the following input parameters:**
&Namespace= QCE/DCX
&Instances.N.Dimensions.0.Name=directConnectConnId
&Instances.N.Dimensions.0.Value=<Dedicated tunnel ID> 
