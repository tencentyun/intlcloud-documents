## Namespace

Namespace=QCE/LB

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| --------------- | ---------- | ------------------------------------------------------------ | ---- | -------------------- | ----------------------------------------------- |
| PvvConnum       | Public network connections | Number of connections from the client to the CLB public network listener in the statistical period                | -   | vip, vport, protocol | 60, 300, 3600, 86400 |
| PvvInpkg        | Inbound packets     | Number of request packets received by the CLB public network listener per second                   | -   | vip, vport, protocol | 60, 300, 3600, 86400 |
| PvvIntraffic    | Inbound bandwidth     | Bandwidth consumed when the CLB public network listener is accessed externally                     | bps  | vip, vport, protocol | 60, 300, 3600, 86400 |
| PvvNewConn      | New connections | Average number of new connections established from the client to the CLB public network listener in the statistical period | -   | vip, vport, protocol | 60, 300, 3600, 86400 |
| PvvOutpkg       | Outbound packets     | Number of packets sent by the CLB public network listener per second                       | -   | vip, vport, protocol | 60, 300, 3600, 86400 |
| PvvOuttraffic   | Outbound bandwidth     | Bandwidth consumed when the CLB public network listener accesses externally                       | bps  | vip, vport, protocol | 60, 300, 3600, 86400 |
| PvvInactiveConn | Inactive connections | Number of TCP connections from the client to the CLB public network listener in a status other than `ESTABLISHED` in the statistical period   | vip, vport, protocol | 60, 300, 3600, 86400 |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| :----------------------------- | :------- | :---------------------- | :---------------------------------------- |
| Instances.N.Dimensions.0.name  | vip      | CLB VIP dimension name | Enter a String-type dimension name: vip |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as `111.111.111.11`    |
| Instances.N.Dimensions.1.name  | vport    | CLB port dimension name  | Enter a String-type dimension name: loadBalancerPort |
| Instances.N.Dimensions.1.value | vport    | Specific CLB port number    | Enter a specific port number, such as `80`                  |
| Instances.N.Dimensions.2.name  | protocol | Protocol dimension name            | Enter a String-type dimension name: protocol         |
| Instances.N.Dimensions.2.value | protocol | Specific protocol                | Enter a specific protocol name, such as `http`            |


## Input Parameter Description

**To query the monitoring data of a CLB public network listener, set the following input parameters:**
&Namespace=QCE/LB
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=vport
&Instances.N.Dimensions.1.Value=Specific port number of CLB instance
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Specific protocol



