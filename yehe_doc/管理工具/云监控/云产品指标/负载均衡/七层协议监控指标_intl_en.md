## Namespace

Namespace=QCE/LOADBALANCE

## Monitoring Metrics

| Parameter | Metric | Unit | Statistical Period |
| ------------------- | ------------------- | ------- | -------------- |
| ClbHttp3xx | 3xx status code returned by CLB | Codes/min | 60, 300, 3600, 86400 |
| ClbHttp404 | 404 status code returned by CLB | Codes/min | 60, 300, 3600, 86400 |
| ClbHttp4xx | 4xx status code returned by CLB | Codes/min | 60, 300, 3600, 86400 |
| ClbHttp502 | 502 status code returned by CLB | Codes/min | 60, 300, 3600, 86400 |
| ClbHttp5xx | 5xx status code returned by CLB | Codes/min | 60, 300, 3600, 86400 |
| ConNum | Active connections | - | 60, 300, 3600, 86400 |
| HttpCode2XX | 2xx status code | Codes/min | 60, 300, 3600, 86400 |
| HttpCode3XX | 3xx status code | Codes/min | 60, 300, 3600, 86400 |
| HttpCode404 | 404 status code | Codes/min | 60, 300, 3600, 86400 |
| HttpCode4XX | 4xx status code | Codes/min | 60, 300, 3600, 86400 |
| HttpCode502 | 502 status code | Codes/min | 60, 300, 3600, 86400 |
| HttpCode5XX | 5xx status code | Codes/min | 60, 300, 3600, 86400 |
| InPkg               | Inbound packets              | Packets/sec   | 60, 300, 3600, 86400 |
| InTraffic           | Inbound bandwidth              | Mbps    | 60, 300, 3600, 86400 |
| NewConn             | New connections          | Connections/min | 60, 300, 3600, 86400 |
| OutPkg              | Outbound packets              | Packets/sec   | 60, 300, 3600, 86400 |
| OutTraffic          | Outbound bandwidth              | Mbps    | 60, 300, 3600, 86400 |
| QPS                 | Requests per second          | -      | 60, 300, 3600, 86400 |
| RequestTimeAverage  | Average request time        | ms    | 60, 300, 3600, 86400 |
| RequestTimeMax      | Maximum request time        | ms    | 60, 300, 3600, 86400 |
| ResponseTimeoutNum  | Timed-out responses        | Responses/min | 60, 300, 3600, 86400 |
| ResponseTimeAverage | Average response time        | ms    | 60, 300, 3600, 86400 |
| ResponseTimeMax     | Maximum response time        | ms    | 60, 300, 3600, 86400 |



> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ---------------- | ---------------------------- | ------------------------------------------ |
| Instances.N.Dimensions.0.name  | vip      | CLB VIP dimension name | Enter a String-type dimension name: vip |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as `111.111.111.11`    |
| Instances.N.Dimensions.1.name  | loadBalancerPort | CLB listener port dimension name | Enter a String-type dimension name: loadBalancerPort |
| Instances.N.Dimensions.1.value | loadBalancerPort | Specific CLB listener port     | Enter a specific port number, such as `80`                   |
| Instances.N.Dimensions.2.name  | protocol | Listener protocol dimension name            | Enter a String-type dimension name: protocol         |
| Instances.N.Dimensions.2.value | protocol | Specific listener protocol                | Enter a specific protocol name, such as `http`            |
| Instances.N.Dimensions.3.name  | vpcId    | VPC ID dimension name       | Enter a String-type dimension name: vpcId                              |
| Instances.N.Dimensions.3.value | vpcId    | Specific CLB VPC ID | Enter a specific VPC ID, such as `vpc-1ywqac83` |
| Instances.N.Dimensions.4.name  | domain   | Domain name dimension name              | Enter a String-type dimension name: domain                             |
| Instances.N.Dimensions.4.value | domain   | Specific domain name                     | Enter a specific domain name, such as `www.cloud.tencent.com`                   |
| Instances.N.Dimensions.5.name  | url      | URL dimension name               | Enter a String-type dimension name: url                                |
| Instances.N.Dimensions.5.value | url      | Specific URL                     | Enter a specific URL, such as `/aaa`                                   |
| Instances.N.Dimensions.6.name  | lanIp            | Real server IP address dimension name             | Enter a String-type dimension name: lanIp                                |
| Instances.N.Dimensions.6.value | lanIp            | Specific real server IP address  | Enter a specific IP address, such as `111.222.111.22`                         |
| Instances.N.Dimensions.7.name  | port             | Real server port dimension name             | Enter a String-type dimension name: port                                 |
| Instances.N.Dimensions.7.value | port             | Specific real server port number | Enter a specific port number, such as `80`                                     |





## Input Parameter Description

Monitoring data can be queried based on the following six combinations of dimensions. The values for input parameters are as follows:

#### 1. Values of input parameters in CLB instance dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address

#### 2. Values of input parameters in CLB listener dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type

#### 3. Values of input parameters in CLB domain name dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type
&Instances.N.Dimensions.3.Name=domain
&Instances.N.Dimensions.3.Value=Domain name

#### 4. Values of input parameters in CLB domain name URL dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type
&Instances.N.Dimensions.3.Name=domain
&Instances.N.Dimensions.3.Value=Domain name
&Instances.N.Dimensions.4.Name=url
&Instances.N.Dimensions.4.Value=URL under domain name

#### 5. Values of input parameters in CLB real server dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=VPC ID of CLB instance
&Instances.N.Dimensions.4.Name=domain
&Instances.N.Dimensions.4.Value=Domain name
&Instances.N.Dimensions.5.Name=url
&Instances.N.Dimensions.5.Value=URL under domain name
&Instances.N.Dimensions.6.Name=lanIp
&Instances.N.Dimensions.6.Value=Real server IP of CLB instance

#### 6. Values of input parameters in CLB real server port dimension

&Namespace: QCE/LOADBALANCE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=loadBalancerPort
&Instances.N.Dimensions.1.Value=Port number
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Protocol type
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=VPC ID of CLB instance
&Instances.N.Dimensions.4.Name=domain
&Instances.N.Dimensions.4.Value=Domain name
&Instances.N.Dimensions.5.Name=url
&Instances.N.Dimensions.5.Value=URL under domain name
&Instances.N.Dimensions.6.Name=lanIp
&Instances.N.Dimensions.6.Value=Real server IP of CLB instance
&Instances.N.Dimensions.7.Name=port
&Instances.N.Dimensions.7.Value=Real server port number of CLB instance
