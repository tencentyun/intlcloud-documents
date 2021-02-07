## Namespace

Namespace=QCE/LOADBALANCE



## Monitoring Metrics

| Parameter | Metric | Description | Unit | Dimension | Statistical Period |
| ------------------- | ------------ | ------------ | ----- | ---------------------------------------- | -------- |
| QPS                 | Requests per second   | Number of requests per second   | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| ResponseTimeoutNum  | Timed-out responses | Number of timed-out responses | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| ResponseTimeAverage | Average response time | Average response time | ms    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| ResponseTimeMax     | Maximum response time | Maximum response time | ms    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| ConNum             | Active connections   | Number of active connections   | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| NewConn             | New connections   | Number of new connections   | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| InPkg               | Inbound packets       | Number of inbound packets       | Packets/sec | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| OutPkg               | Outbound packets       | Number of outbound packets       | Packets/sec | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| InTraffic           | Inbound bandwidth       | Inbound bandwidth       | Mbps  | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| OutTraffic          | Outbound bandwidth       | Outbound bandwidth       | Mbps  | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| HttpCode2XX         | 2xx status codes   | Number of 2xx status codes   | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| HttpCode3XX         | 3xx status codes   | Number of 3xx status codes   | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| HttpCode4XX         | 4xx status codes   | Number of 4xx status codes   | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| HttpCode5XX         | 5xx status codes   | Number of 5xx status codes   | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| HttpCode404         | 404 status codes    | Number of 404 status codes    | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| HttpCode502         | 502 status codes    | Number of 502 status codes    | -    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| RequestTimeAverage  | Average request time | Average request time | ms    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s |
| RequestTimeMax      | Maximum request time | Maximum request time | ms    | domain, loadBalancerPort, protocol, url, vip | 60s, 300s|

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | -------- | ---------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.value | vip      | Specific CLB VIP        | Enter a specific IP address, such as `111.111.111.11`    |
| Instances.N.Dimensions.1.name  | port     | CLB port dimension name  | Enter a String-type dimension name: port                    |
| Instances.N.Dimensions.1.value | port    | Specific CLB port    | Enter a specific port number, such as `80`                  |
| Instances.N.Dimensions.2.name  | protocol | Protocol dimension name            | Enter a String-type dimension name: protocol         |
| Instances.N.Dimensions.2.value | protocol | Specific protocol name                | Enter a specific protocol name, such as `http`            |
| Instances.N.Dimensions.3.name  | vpcId    | VPC ID dimension name       | Enter a String-type dimension name: vpcId                              |
| Instances.N.Dimensions.3.value | vpcId    | Specific CLB VPC ID | Enter a specific VPC ID, such as `1111`. You should enter a numerical `vpcId`. For more information on how to get a `NumericalvpcId`, please see [DescribeLoadBalancerListByCertId](https://intl.cloud.tencent.com/document/product/214/33800) |
| Instances.N.Dimensions.4.name  | domain   | Domain name dimension name              | Enter a String-type dimension name: domain                             |
| Instances.N.Dimensions.4.value | domain   | Specific domain name                     | Enter a specific domain name, such as `www.cloud.tencent.com`                   |
| Instances.N.Dimensions.5.name  | url      | URL dimension name               | Enter a String-type dimension name: url                                |
| Instances.N.Dimensions.5.value | url      | Specific URL                     | Enter a specific URL, such as `/aaa`                                     |

## Input Parameter Description

**Input parameters for monitoring layer-7 CLB - URL dimension:**

&Namespace=QCE/LB_PRIVATE
&Instances.N.Dimensions.0.Name=vip
&Instances.N.Dimensions.0.Value=IP address
&Instances.N.Dimensions.1.Name=port
&Instances.N.Dimensions.1.Value=Specific port of CLB instance
&Instances.N.Dimensions.2.Name=protocol
&Instances.N.Dimensions.2.Value=Specific protocol name
&Instances.N.Dimensions.3.Name=vpcId
&Instances.N.Dimensions.3.Value=VPC ID of CLB instance
&Instances.N.Dimensions.4.Name=domain
&Instances.N.Dimensions.4.Value=Specific domain name
&Instances.N.Dimensions.5.Name=url
&Instances.N.Dimensions.5.Value=Specific URL
