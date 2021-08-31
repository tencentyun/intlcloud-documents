## Namespace

Namespace=QCE/LB

## Monitoring Metrics



| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ------------- | ---------- | ------------------------------------------------------------ | ----- | ---- | ----------------------------------------------- |
| VConnum       | Connections   | Number of all TCP connections in the `ESTABLISHED` status from the client to CLB in the statistical period | -    | vip  | 60, 300, 3600, 86400 |
| VNewConn      | New connections | Average number of new connections established from the client to CLB in the statistical period | -    | vip  | 60, 300, 3600, 86400 |
| VInpkg        | Public network inbound packets | Number of request packets received by CLB per second                             | Packets/sec | vip  | 60, 300, 3600, 86400 |
| VIntraffic    | Public network inbound bandwidth | Bandwidth consumed when CLB is accessed externally                               | Mbps  | vip  | 60, 300, 3600, 86400 |
| VOutpkg       | Public network outbound packets | Number of packets sent by CLB per second                                 | Packets/sec | vip  | 60, 300, 3600, 86400 |
| VOuttraffic   | Public network outbound bandwidth | Bandwidth consumed when CLB accesses externally                                 | Mbps  | vip  | 60, 300, 3600, 86400 |
| AccOuttraffic | Public network outbound traffic | Traffic consumed when CLB accesses externally                                 | MB    | vip  | 60, 300, 3600, 86400 |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

## Overview of Parameters in Each Dimension

| Parameter  | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.name  | vip      | CLB VIP dimension name | Enter a String-type dimension name: vip |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as `111.111.111.11`    |

## Input Parameter Description

**Input parameters for CLB - CLB instance:**

&Namespace=QCE/LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address



