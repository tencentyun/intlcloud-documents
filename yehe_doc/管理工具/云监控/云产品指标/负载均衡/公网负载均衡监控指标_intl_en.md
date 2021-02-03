## Namespace

Namespace=QCE/LB_PUBLIC

>?This namespace includes monitoring data in the CLB instance and real server dimensions.

## Monitoring Metrics

| Parameter | Metric | Unit | Statistical Period |
| ------------- | ------------------ | ------- | ------------ |
| AccOuttraffic | Public network outbound traffic | MB | 10, 60, 300, 3600 |
| ClbHttp3xx | 3xx status code returned by CLB | Codes/min | 60, 300, 3600 |
| ClbHttp404 | 404 status code returned by CLB | Codes/min | 60, 300, 3600 |
| ClbHttp4xx | 4xx status code returned by CLB | Codes/min | 60, 300, 3600 |
| ClbHttp502 | 502 status code returned by CLB | Codes/min | 60, 300, 3600 |
| ClbHttp5xx | 5xx status code returned by CLB | Codes/min | 60, 300, 3600 |
| ConNum     | Current connections | -    | 60, 300, 3600 |
| Http2xx | 2xx status code | Codes/min | 60, 300, 3600 |
| Http3xx | 3xx status code | Codes/min | 60, 300, 3600 |
| Http404 | 404 status code | Codes/min | 60, 300, 3600 |
| Http4xx | 4xx status code | Codes/min | 60, 300, 3600 |
| Http502 | 502 status code | Codes/min | 60, 300, 3600 |
| Http5xx | 5xx status code | Codes/min | 60, 300, 3600 |
| InactiveConn | Inactive connections | - | 60, 300, 3600 |
| InPkg | Public network inbound packets | Packets/sec | 10, 60, 300, 3600 |
| InTraffic | Public network inbound bandwidth | Mbps | 10, 60, 300, 3600 |
| NewConn    | New connections | Connections/sec | 60, 300, 3600 |
| OutPkg        | Public network outbound packets         | Packets/sec   | 10, 60, 300, 3600  |
| OutTraffic    | Public network outbound bandwidth         | Mbps    | 10, 60, 300, 3600  |
| ReqAvg        | Average request time       | ms    | 60, 300, 3600      |
| ReqMax        | Maximum request time       | ms    | 60, 300, 3600      |
| RspAvg        | Average response time       | ms    | 60, 300, 3600      |
| RspMax        | Maximum response time       | ms    | 60, 300, 3600      |
| RspTimeout    | Timed-out responses       | Responses/min | 60, 300, 3600      |
| SuccReq       | Successful requests   | Requests/min | 60, 300, 3600      |
| TotalReq      | Requests         | Requests/sec      | 60, 300, 3600      |



>?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------------- | ----------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.name  | vip      | CLB VIP dimension name | Enter a String-type dimension name: vip |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as 111.111.111.11    |
| Instances.N.Dimensions.1.name  | loadBalancerPort | CLB listener port dimension name | Enter a String-type dimension name: loadBalancerPort |
| Instances.N.Dimensions.1.value | loadBalancerPort | Specific CLB listener port     | Enter a specific port number, such as 80                   |
| Instances.N.Dimensions.2.name  | protocol | Listener protocol dimension name            | Enter a String-type dimension name: protocol         |
| Instances.N.Dimensions.2.value | protocol | Specific listener protocol                | Enter a specific protocol name, such as http            |
| Instances.N.Dimensions.3.name  | vpcId    | VPC ID dimension name       | Enter a String-type dimension name: vpcId                              |
| Instances.N.Dimensions.3.value | vpcId    | Specific CLB VPC ID | Enter a specific VPC ID, such as `vpc-1ywqac83` |
| Instances.N.Dimensions.4.name  | lanIp            | Real server IP address dimension name             | Enter a String-type dimension name: lanIp                                |
| Instances.N.Dimensions.4.value | lanIp            | Specific real server IP address  | Enter a specific IP address, such as `111.222.111.22`                        |
| Instances.N.Dimensions.5.name  | port             | Real server port dimension name             | Enter a String-type dimension name: port                                 |
| Instances.N.Dimensions.5.value | port             | Specific real server port number | Enter a specific port number, such as `80`                                     |

## Input Parameter Description

Monitoring data of public network CLB can be queried based on the following four combinations of dimensions. The values for input parameters are as follows:

#### 1. Values of input parameters in public network CLB instance dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address

#### 2. Values of input parameters in public network CLB listener dimension

&Namespace: QCE/LB_PUBLIC
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type

#### 3. Values of input parameters in public network CLB real server dimension

&Namespace: QCE/LB_PUBLIC
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

#### 4. Values of input parameters in public network CLB real server port dimension

&Namespace: QCE/LB_PUBLIC
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
