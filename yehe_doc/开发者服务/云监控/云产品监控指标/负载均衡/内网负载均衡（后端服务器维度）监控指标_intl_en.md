## Namespace

Namespace=QCE/LB_RS_PRIVATE

## Monitoring Metrics

| Parameter | Metric Name | Unit |
| ---------- | ---------- | ---- |
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
| Instances.N.Dimensions.0.Name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name, such as vip |
| Instances.N.Dimensions.0.Value | vip | A specific CLB VIP | Enter a specific IP address, such as 111.111.111.11 |
| Instances.N.Dimensions.1.Name | vpcId | Dimension name of the VPC ID | Enter a string-type dimension name, such as vpcId |
| Instances.N.Dimensions.1.Value | vpcId | A specific VPC ID (of the CLB instance) | Enter a specific VPC ID, such as 1111. We recommend that you enter a numeric vpcId. For information on obtaining the numeric vpcId, see [DescribeLoadBalancerListByCertId](https://intl.cloud.tencent.com/document/product/214/33800) |
| Instances.N.Dimensions.2.Name | loadBalancerPort | Dimension name of the CLB port | Enter a string-type dimension name, such as loadBalancerPort |
| Instances.N.Dimensions.2.Value | loadBalancerPort | A specific CLB port | Enter a specific port number, such as 80 |
| Instances.N.Dimensions.3.Name | protocol | Dimension name of the protocol | Enter a string-type dimension name, such as protocol |
| Instances.N.Dimensions.3.Value | protocol | A specific protocol | Enter a specific protocol name, such as http |
| Instances.N.Dimensions.4.Name | lanIp | Dimension name of the lanIp | Enter a string-type dimension name, such as lanIp |
| Instances.N.Dimensions.4.Value | lanIp | A specific IP address of the real server bound to the CLB instance | Enter a specific IP address, such as 111.111.111.11 |
| Instances.N.Dimensions.5.Name | port | Dimension name of the port number | Enter a string-type dimension name, such as port |
| Instances.N.Dimensions.5.Value | port | A specific port number of the real server bound to the CLB instance | Enter a specific port number, such as 80 |

## Input Parameters

Private network CLB instances (at the real server dimension) support the combination of the following two dimensions for querying monitoring data. The values for the two types of input parameters are as follows:

#### 1. Values of the input parameters at the private network CLB real server dimension

Since the private vip may be repeated, vpcId is also required to uniquely specify a CLB instance:
&Namespace= QCE/LB_RS_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=<VPC ID of the CLB instance>
&Instances.N.Dimensions.2.Name=loadBalancerPort
&Instances.N.Dimensions.2.Value=<Port number>
&Instances.N.Dimensions.3.Name=protocol
&Instances.N.Dimensions.3.Value=<Protocol type>
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=<IP address of the real server bound to the CLB instance>

#### 2. Values of the input parameters at the private network CLB real server port dimension

Since the private vip may be repeated, vpcId is also required to uniquely specify a CLB instance:

&Namespace= QCE/LB_RS_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=<VPC ID of the CLB instance>
&Instances.N.Dimensions.2.Name=loadBalancerPort
&Instances.N.Dimensions.2.Value=<Port number>
&Instances.N.Dimensions.3.Name=protocol
&Instances.N.Dimensions.3.Value=<Protocol type>
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=<IP address of the real server bound to the CLB instance>
&Instances.N.Dimensions.5.Name=port
&Instances.N.Dimensions.5.Value=<Port number of the real server bound to the CLB instance>

