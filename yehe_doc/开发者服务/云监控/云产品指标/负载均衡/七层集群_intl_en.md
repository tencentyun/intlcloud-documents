## Namespace

Namespace=QCE/LOADBALANCE

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ------------------ | -------------------- | ------------------------------------------------------------ | ---- | --------- | ----------------------------------------------- |
| ActiveConnRatio    | Active connection utilization       | Utilization of active connections established from the client to the layer-7 CLB cluster in the statistical period | %    | clusterId | 60, 300, 3600        |
| InpkgRatio      | Inbound packet utilization | Utilization of the request packets received by the layer-7 CLB cluster per second             | %     | clusterId | 60, 300, 3600, 86400 |
| IntrafficRatio  | Inbound bandwidth utilization | Utilization of the bandwidth consumed when the layer-7 CLB cluster is accessed externally                 | %     | clusterId | 60, 300, 3600 |
| NewActiveConnRatio | New active connection utilization | Utilization of new connections established from the client to the layer-7 CLB cluster in the statistical period | %     | clusterId | 60, 300, 3600 |
| OutpkgRatio     | Outbound packet utilization | Utilization of the packets sent by the layer-7 CLB cluster per second                       | %     | clusterId | 60, 300, 3600 |
| OuttrafficRatio | Outbound bandwidth utilization     | Utilization of the bandwidth consumed when the layer-7 CLB cluster accesses externally                   | %     | clusterId | 60, 300, 3600 |
| QpsRatio           | QPS utilization            | Utilization of requests of the layer-7 CLB cluster per second                               | %    | clusterId | 60, 300, 3600 |
| Setreqmax          | Maximum request time         | Maximum request time of the layer-7 CLB cluster                                 | ms   | clusterId | 60, 300, 3600, 86400 |
| Setreqavg          | Average request time         | Average request time of the layer-7 CLB cluster                                 | ms   | clusterId | 60, 300, 3600, 86400 |
| Setrspmax          | Maximum response time         | Maximum response time of the layer-7 CLB cluster                                 | ms   | clusterId | 60, 300, 3600, 86400 |
| Setrspavg          | Average response time         | Average response time of the layer-7 CLB cluster                                 | ms   | clusterId | 60, 300, 3600, 86400 |
| Rsptimeout         | Response timeouts         | Number of response timeouts of the layer-7 CLB cluster                                 | -   | clusterId | 60, 300, 3600, 86400 |
| Settotalreq        | Requests per minute         | Number of requests of the layer-7 CLB cluster per minute                                 | -   | clusterId | 60, 300, 3600, 86400 |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.name  | clusterId | CLB cluster ID dimension name | Enter a String-type dimension name: clusterId |
| Instances.N.Dimensions.0.value | clusterId | Specific CLB cluster ID        | Enter a specific cluster ID, such as `tgw-12345678` |


## Input Parameter Description

**Input parameters for layer-7 CLB cluster:**

&Namespace= QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value=Cluster ID
