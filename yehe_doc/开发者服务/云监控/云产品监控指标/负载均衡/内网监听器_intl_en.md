## Namespace

Namespace=QCE/LB_PRIVATE

## Monitoring Metrics

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ------------- | ---------- | --------------------------------------------- | ----- | -------------------------- | ------------------------------- |
| PvvConnum       | Public network connections | Number of connections from the client to the CLB private network listener in the statistical period                | -   | vip, vpcId, Port, protocol | 60, 300, 3600, 86400 |
| PvvNewConn    | Current connections | Number of current connections from the client to the CLB private network listener           | -    | vip, vpcId, Port, protocol | 60, 300, 3600, 86400 |
| PvvInpkg        | Inbound packets     | Number of request packets received by the CLB private network listener per second                   | -   | vip, vpcId, Port, protocol  | 60, 300, 3600, 86400 |
| PvvIntraffic    | Inbound bandwidth     | Bandwidth consumed when the CLB private network listener is accessed externally                     | bps  | vip, vpcId, Port, protocol | 60, 300, 3600, 86400 |
| PvvOutpkg       | Outbound packets     | Number of packets sent by the CLB private network listener per second                       | Packets/sec   | vip, vpcId, Port, protocol | 60, 300, 3600, 86400 |
| PvvOuttraffic   | Outbound bandwidth     | Bandwidth consumed when the CLB private network listener accesses externally                       | bps  | vip, vpcId, Port, protocol | 60, 300, 3600, 86400 |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

## Overview of Parameters in Each Dimension

| Parameter | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.name  | vip      | CLB VIP dimension name | Enter a String-type dimension name: vip |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as `111.111.111.11`    |
| Instances.N.Dimensions.1.name  | vpcId    | VPC ID dimension name       | Enter a String-type dimension name: vpcId                              |
| Instances.N.Dimensions.1.value | vpcId    | Specific CLB VPC ID | Enter a specific VPC ID, such as `1012345`. You should enter a numerical `vpcId`. For more information on how to get a `NumericalvpcId`, please see [DescribeLoadBalancerListByCertId](https://intl.cloud.tencent.com/document/product/214/33800) |
| Instances.N.Dimensions.2.name  | Port | CLB port dimension name  | Enter a String-type dimension name: Port                    |
| Instances.N.Dimensions.2.value | Port | Specific CLB port number    | Enter a specific port number, such as `80`                  |
| Instances.N.Dimensions.3.name  | protocol | Protocol dimension name            | Enter a String-type dimension name: protocol         |
| Instances.N.Dimensions.3.value | protocol | Specific protocol                | Enter a specific protocol name, such as `http`            |


## Input Parameter Description

**Input parameters for CLB private network listener:**

&Namespace= QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=VPC ID of CLB instance
&Instances.N.Dimensions.2.Name=Port
&Instances.N.Dimensions.2.Value=Port number
&Instances.N.Dimensions.3.Name=protocol
&Instances.N.Dimensions.3.Value=Protocol type

