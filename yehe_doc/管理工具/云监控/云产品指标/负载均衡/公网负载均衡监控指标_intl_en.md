## Namespace

Namespace=QCE/LB_PUBLIC


## Monitoring Metrics

| Parameter | Metric Name | Unit |
| ---------------- | ----- |---- |
| Connum | Connections | Count |
| NewConn | New connections | Connections/sec |
| Intraffic | Public inbound bandwidth | Mbps |
| Outtraffic | Public outbound bandwidth | Mbps |
| Inpkg | Inbound packets | Packets/sec |
| Outpkg | Outbound packets | Packets/sec |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.


## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.name | vip | Dimension name of the CLB VIP | Enter a string-type dimension name, such as vip |
| Instances.N.Dimensions.0.value | vip | A specific CLB VIP | Enter a specific IP address, such as 111.111.111.11 |
| Instances.N.Dimensions.1.name | loadBalancerPort | Dimension name of the CLB instance port | Enter a string-type dimension name, such as loadBalancerPort |
| Instances.N.Dimensions.1.value | loadBalancerPort | A specific CLB port | Enter a specific port number, such as 80 |
| Instances.N.Dimensions.2.name | protocol | Dimension name of the protocol | Enter a string-type dimension name, such as protocol |
| Instances.N.Dimensions.2.value | protocol | A specific protocol | Enter a specific protocol name, such as http |
| Instances.N.Dimensions.3.name | vpcId | Dimension name of the VPC ID | Enter a string-type dimension name, such as vpcId |
| Instances.N.Dimensions.3.value | vpcId | A specific VPC ID (of the CLB instance) | Enter a specific VPC ID, such as 1111. We recommend that you enter a numeric vpcId. For information on obtaining the numeric vpcId, see [DescribeLoadBalancerListByCertId](https://intl.cloud.tencent.com/document/product/214/33800) |
| Instances.N.Dimensions.4.name | lanIp | Dimension name of the lanIp | Enter a string-type dimension name, such as lanIp |
| Instances.N.Dimensions.4.value | lanIp | A specific IP address of the real server bound to the CLB instance | Enter a specific IP address, such as 111.222.111.22 |
| Instances.N.Dimensions.5.name | port | Dimension name of the port number | Enter a string-type dimension name, such as port |
| Instances.N.Dimensions.5.value | port | A specific port number of the real server bound to the CLB instance | Enter a specific port number, such as 80 |

## Input Parameters

Public network CLB instances support the combinations of the following four dimensions for querying monitoring data. The values for the four types of input parameters are as follows:

#### 1. Values of the input parameters at the public network CLB instance dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>

#### 2. Values of the input parameters at the public network CLB instance port dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>

#### 3 Values of the input parameters at the public network CLB real server dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=<VPC ID of the CLB instance>
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=<IP address of the real server bound to the CLB instance>

#### 4. Values of the input parameters at the public network CLB real server port dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=<IP address>
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=<Port number>
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=<Protocol type>
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=<VPC ID of the CLB instance>
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=<IP address of the real server bound to the CLB instance>
&Instances.N.Dimensions.5.Name=port
&Instances.N.Dimensions.5.Value=<Port number of the real server bound to the CLB instance>
