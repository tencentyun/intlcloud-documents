## Namespace

Namespace=QCE/TGW_SET

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| --------------- | ---------------- | ------------------------------------------------------------ | ----- | --------- | ---------------------------------------- |
| ConcurConnRatio | Concurrent connection utilization | Utilization of all the TCP connections established from the client to the layer-4 CLB cluster in the statistical period | %     | clusterId | 60, 300, 3600 |
| InpkgRatio      | Public network inbound packet utilization | Utilization of the request packets received by the layer-4 CLB cluster per second             | %     | clusterId | 60, 300, 3600 |
| IntrafficRatio  | Public network inbound bandwidth utilization | Utilization of the bandwidth consumed when the layer-4 CLB cluster is accessed externally                 | %     | clusterId | 60, 300, 3600 |
| NewConnRatio    | New connection utilization   | Utilization of new connections established from the client to CLB in the statistical period | %     | clusterId | 60, 300, 3600 |
| OutpkgRatio     | Public network outbound packet utilization | Utilization of the packets sent by the layer-4 CLB cluster per second                       | %     | clusterId | 60, 300, 3600 |
| OuttrafficRatio | Outbound bandwidth utilization     | Utilization of the bandwidth consumed when the layer-4 CLB cluster accesses externally                   | %     | clusterId | 60, 300, 3600 |
| ConcurConn      | Concurrent connections       | Number of all TCP connections established from the client to the layer-4 CLB cluster in the statistical period | -    | clusterId | 60, 300, 3600 |
| ConNum          | Public network connections       | Number of all TCP connections in the `ESTABLISHED` status from the client to the layer-4 CLB cluster in the statistical period | -    | clusterId | 60, 300, 3600 |
| DropTotalConns  | Dropped connections       | Number of dropped connections from the client to the layer-4 CLB cluster in the statistical period          | Connections/sec | clusterId | 60, 300, 3600 |
| InactiveConn    | Inactive connections | Number of TCP connections from the client to the layer-4 CLB cluster in a status other than `ESTABLISHED` in the statistical period | -    | clusterId | 60, 300, 3600 |
| InPkg           | Public network inbound packets       | Number of request packets received by the layer-4 CLB cluster per second                     | Packets/sec | clusterId | 60, 300, 3600 |
| InTraffic       | Public network inbound bandwidth       | Bandwidth consumed when the layer-4 CLB cluster is accessed externally                       | MB/s  | clusterId | 60, 300, 3600 |
| InDropBits      | Dropped inbound traffic       | Bandwidth dropped when the layer-4 CLB cluster is accessed externally                         | MB/s  | clusterId | 60, 300, 3600 |
| InDropPkts      | Dropped inbound packets   | Number of dropped request packets received by the layer-4 CLB cluster per second             | Packets/sec | clusterId | 60, 300, 3600 |
| NewActiveConn   | New active connections   | Number of new active connections established from the client to the layer-4 CLB cluster in the statistical period | Connections/sec | clusterId | 60, 300, 3600 |
| NewConn         | New connections (CPS)  | Number of new connections established from the client to the layer-4 CLB cluster in the statistical period | Connections/sec | clusterId | 60, 300, 3600 |
| OutPkg          | Public network outbound packets       | Number of packets sent by the layer-4 CLB cluster per second                         | Packets/sec | clusterId | 60, 300, 3600 |
| OutTraffic      | Outbound bandwidth           | Bandwidth consumed when the layer-4 CLB cluster accesses externally                         | MB/s  | clusterId | 60, 300, 3600 |
| OutDropBits     | Dropped outbound traffic       | Bandwidth dropped when the layer-4 CLB cluster accesses externally                           | MB/s  | clusterId | 60, 300, 3600 |
| OutDropPkts     | Dropped outbound packets   | Number of dropped packets sent by the layer-4 CLB cluster per second                | Packets/sec | clusterId | 60, 300, 3600 |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | --------- | ------------------------- | ---------------------------------- |
| Instances.N.Dimensions.0.name  | clusterId | CLB cluster ID dimension name | Enter a String-type dimension name: clusterId |
| Instances.N.Dimensions.0.value | clusterId | Specific CLB cluster ID        | Enter a specific cluster ID, such as `tgw-12345678` |


## Input Parameter Description

**Input parameters for layer-4 CLB cluster:**

&Namespace= QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value=Cluster ID

