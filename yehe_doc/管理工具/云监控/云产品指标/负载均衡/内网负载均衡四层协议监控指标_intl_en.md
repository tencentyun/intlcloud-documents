## Namespace

Namespace=QCE/LB_PRIVATE

## Monitoring Metrics

| Parameter | Metric | Unit | Statistical Period |
| ---------- | ---------- | ----- | -------------- |
| ConNum     | Current connections | -    | 60, 300, 3600, 86400 |
| InPkg      | Inbound packets     | Packets/sec | 60, 300, 3600, 86400 |
| InTraffic  | Inbound bandwidth     | Mbps  | 60, 300, 3600, 86400 |
| NewConn    | New connections | Connections/sec | 60, 300, 3600, 86400 |
| OutPkg     | Outbound packets     | Packets/sec | 60, 300, 3600, 86400 |
| OutTraffic | Outbound bandwidth     | Mbps  | 60, 300, 3600, 86400 |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------ |
| Instances.N.Dimensions.0.name  | vip      | CLB VIP dimension name | Enter a String-type dimension name: vip |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as `111.111.111.11`    |
| Instances.N.Dimensions.1.name  | loadBalancerPort | CLB listener port dimension name | Enter a String-type dimension name: loadBalancerPort |
| Instances.N.Dimensions.1.value | loadBalancerPort | Specific CLB listener port     | Enter a specific port number, such as `80`                   |
| Instances.N.Dimensions.2.name  | protocol | Listener protocol dimension name            | Enter a String-type dimension name: protocol         |
| Instances.N.Dimensions.2.value | protocol         | Specific listener protocol                | Enter a specific protocol name, such as `TCP` or `UDP`       |
| Instances.N.Dimensions.3.name  | vpcId    | VPC ID dimension name       | Enter a String-type dimension name: vpcId                              |
| Instances.N.Dimensions.3.value | vpcId    | Specific CLB VPC ID | Enter a specific VPC ID, such as `vpc-1ywqac83` |
| Instances.N.Dimensions.4.name  | lanIp            | Real server IP address dimension name             | Enter a String-type dimension name: lanIp                                |
| Instances.N.Dimensions.4.value | lanIp            | Specific real server IP address  | Enter a specific IP address, such as `111.222.111.22`                         |
| Instances.N.Dimensions.5.name  | port             | Real server port dimension name             | Enter a String-type dimension name: port                                 |
| Instances.N.Dimensions.5.value | port             | Specific real server port number | Enter a specific port number, such as `80`                                     |

## Input Parameter Description

Monitoring data of private network CLB can be queried based on the following four combinations of dimensions. The values for input parameters are as follows:

#### 1. Values of input parameters in private network CLB instance dimension
&Namespace: QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=VPC ID of CLB instance


#### 2. Values of input parameters in private network CLB listener dimension
&Namespace: QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=vpcId
&Instances.N.Dimensions.1.Value=VPC ID of CLB instance
&Instances.N.Dimensions.2.Name=loadBalancerPort
&Instances.N.Dimensions.2.Value=Port number
&Instances.N.Dimensions.3.Name=protocol
&Instances.N.Dimensions.3.Value=Protocol type

#### 3. Values of input parameters in private network CLB real server dimension
&Namespace: QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=VPC ID of real server
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=Real server IP of CLB instance

#### 4. Values of input parameters in private network CLB real server port dimension
&Namespace: QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=VPC ID of CLB instance
&Instances.N.Dimensions.4.Name=lanIp
&Instances.N.Dimensions.4.Value=real server IP of CLB instance
&Instances.N.Dimensions.5.Name=port
&Instances.N.Dimensions.5.Value=Real server port number of CLB instance
