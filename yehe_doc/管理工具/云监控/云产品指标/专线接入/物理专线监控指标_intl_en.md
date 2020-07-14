## Namespace
Namespace=QCE/DC

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| ----- | ----------- | ---- |---- |---- |
| OutBandwidth | Network outbound bandwidth | Average outbound traffic per second for a connection | Mbps | directConnectConnId |
| InBandwidth | Network inbound bandwidth | Average inbound traffic per second for a connection | Mbps | directConnectConnId |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
|---------|---------|---------|---------|
| Instances.N.Dimensions.0.Name | directConnectConnId | Dimension name of the dedicated tunnel ID | Enter a string-type input parameter dimension name, such as directConnectConnId |
| Instances.N.Dimensions.0.Value | directConnectConnId | A specific connection ID | Enter a specific ID for a connection, such as dc-e1h9wqp8 |

## Parameters

To query the monitoring data of a dedicated tunnel, use the following input parameters:
&Namespace= QCE/DCX
&Instances.N.Dimensions.0.Name=directConnectConnId
&Instances.N.Dimensions.0.Value=<Dedicated tunnel ID> 
