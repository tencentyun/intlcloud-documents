## Namespace

Namespace=QCE/LB_PRIVATE

## Monitoring Metrics

| Parameter | Metric Name | Unit |
| ---------------- | ----- | ---- |
| Connum | Current connections | Count |
| NewConn | New connections | Connections/sec |
| Intraffic | Inbound traffic | Mbps |
| Outtraffic | Outbound traffic | Mbps |
| Inpkg | Inbound packets | Packets/sec |
| Outpkg | Outbound packets | Packets/sec |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name, such as vip |
| Instances.N.Dimensions.0.value | vip | A specific CLB VIP | Enter a specific IP address, such as 111.111.111.11 |
| Instances.N.Dimensions.1.name | vpcId | Dimension name of the VPC ID | Enter a string-type dimension name, such as vpcId |
| Instances.N.Dimensions.1.value | vpcId | A specific VPC ID (of the CLB instance) | Enter a specific VPC ID, such as 1012345. We recommend that you enter a numeric vpcId. For information on obtaining the numeric vpcId, see [DescribeLoadBalancerListByCertId](https://intl.cloud.tencent.com/document/product/214/33800) |
| Instances.N.Dimensions.2.name | loadBalancerPort | Dimension name of the CLB instance port | Enter a string-type dimension name, such as loadBalancerPort |
| Instances.N.Dimensions.2.value | loadBalancerPort | A specific CLB port number | Enter a specific port number, such as 80 |
| Instances.N.Dimensions.3.name | protocol | Dimension name of the protocol | Enter a string-type dimension name, such as protocol |
| Instances.N.Dimensions.3.value | protocol | A specific protocol | Enter a specific protocol name, such as http |


## Input Parameters

Private network CLB instances support the combination of the following two dimensions for querying monitoring data. The values for the two types of input parameters are as follows:

#### 1. Values of the input parameters at the private network CLB instance dimension

&Namespace=QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=<VPC ID of the CLB instance>

#### 2. Values of the input parameters at the private network CLB instance port dimension

&Namespace=QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=<VPC ID of the CLB instance>
&Instances.N.Dimensions.2.Name=loadBalancerPort
&Instances.N.Dimensions.2.Value=<Port number> 
&Instances.N.Dimensions.3.Name=protocol
&Instances.N.Dimensions.3.Value=<Protocol type>
