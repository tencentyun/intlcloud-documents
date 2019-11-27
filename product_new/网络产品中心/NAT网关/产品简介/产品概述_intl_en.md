## Overview
NAT Gateway is a service that supports IP address translation and provides the [SNAT](https://cloud.tencent.com/document/product/552/12952) and [DNAT](https://cloud.tencent.com/document/product/552/12952) capabilities. It provides secure and high-performance Internet access for resources in [VPCs](https://intl.cloud.tencent.com/document/product/215/535). NAT Gateway supports a high availability of up to 99.99%, 5 Gbps bandwidth, and more than 10 million concurrent connections. Its typical application scenarios are as follows:
1. Large bandwidth and high-availability public network egress services, such as web crawlers and access to Internet public services.
2. Secure public network egress services, for example, you would like to have a CVM  communicates with internet but don’t want to bind the CVM to a public IP address for security reasons.

## Network Topology
As shown in the following figure, when resources in the VPC, such as CVMs, send outbound data packets through the NAT gateway, these data packets first travel through the router and then are routed according to the routing policy. Finally, the NAT gateway sends the traffic to the Internet by using the bound EIP as the source IP address.
![](https://main.qcloudimg.com/raw/3c4bdc38f992ab789eac9a53ccca9914.png)

## Differences Between the NAT Gateway and the Public Gateway
CVMs in a VPC can access the Internet through a NAT gateway or a public gateway. The following table lists the differences between both types of gateways.

| Attribute | NAT Gateway | Public Gateway |
| ------ | ---------------------------------------- | ---------------------------------------- |
| Availability | Master/Slave hot backup and automatic hot switching | Manually switches the failed gateway. |
| Public network bandwidth | Maximum of 5 Gbps | Depends on the network bandwidth of the CVM. |
| Public IP address | A maximum of 10 EIPs can be bound | Supports one EIP or ordinary public IP address. |
| Rate limit of the public network | N/A | Depends on the rate limit of the CVM. |
| Max concurrent connections | 10,000,000 | 500,000 |
| Private IP address | Private IP addresses of VPC users are not consumed | Private IP addresses of subnets are consumed. |
| Security group | Binding a security group to a NAT gateway is not supported. Instead, you can bind a security group to the backend CVM. | Binding a security group is supported. |
| Network ACL | Binding a network ACL to a NAT gateway is not supported. Instead, you can bind a network ACL to the subnet where the backend CVM resides. | Binding a network ACL is not supported. Instead, you can bind a network ACL to the subnet where the public gateway resides. |
| Cost | Mainland China:<br/>Small (max. 1,000,000 connections): 0.5 CNY/hr<br/>Medium (max. 3,000,000 connections: 1.5 CNY/hr<br/>Large (max. 10,000,000 connections): 5 CNY/hr | Depends on the specifications of the CVM that is used as the public gateway, taking mainland China as an example:<br/>1 core and 2 GB: 0.44 CNY/hr<br/>4 cores and 8 GB: 1.76 CNY/hr<br/>12 cores and 24 GB: 5.28 CNY/hr. |

The NAT gateway has the following advantages:
- Large capacity
It supports a maximum of 10,000,000 concurrent connections, 5 Gbps bandwidth, and 10 EIPs, meeting the demands of customers with a large business scale.
- Highly available master/slave hot backup
It supports automatic failover in case of a single point of failure to implement automatic disaster recovery and 99.99% service availability, which is superior to the manual switching of a public gateway.
- Cost effectiveness
Three configuration types (small, medium, and large) are available for users to purchase as needed, offering flexibility in billing and high cost-effectiveness.
