## Namespace
Namespace=QCE/QAAP 

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension |
| --- | --- | --- | --- | --- |
| ListenerRsStatus | Status of the origin server under the listener | Health of the origin server under the listener (0: unhealthy, 1: healthy) | N/A | channelId, listenerId, and originServerInfo |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the period supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | -------------------- | ----------------------------------------- |
| Instances.N.Dimensions.0.Name | channelId | Dimension name of the acceleration connection ID | Enter a string-type dimension name, such as channelId |
| Instances.N.Dimensions.0.Value | channelId | A specific acceleration connection ID | Enter a specific acceleration connection ID, such as link-abcd1234 |
| Instances.N.Dimensions.1.Name | listenerId | Dimension name of the listener ID | Enter a string-type dimension name, such as listenerId |
| Instances.N.Dimensions.1.Value | listenerId | A specific listener ID | Enter a specific listener ID, such as listener-1234abcd |
| Instances.N.Dimensions.2.Name | originServerInfo | Dimension name of the origin server information | Enter a string-type dimension name, such as originServerInfo |
| Instances.N.Dimensions.2.Value | originServerInfo | IP address or domain name of the origin server | Enter the IP address or domain name of the origin server, such as www.cloud.tencent.com |

## Input Parameters

To query the health monitoring data of a GAAP origin server, use the following input parameters:

&Namespace=QCE/QAAP
&Instances.N.Dimensions.0.Name=channelId 
&Instances.N.Dimensions.0.Value=<Channel ID>





