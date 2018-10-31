## Overview

The NAT gateway is a network cloud service that supports IP address translation. It provides high-performance Internet access services for resources within Tencent Cloud. With NAT gateways, the resources on Tencent Cloud can access the Internet more securely, and the information of VPCs is not directly exposed on the public network. NAT gateways enable massive public network access with a maximum of more than 10,000,000 concurrent connections. NAT gateways also support IP-level traffic control, which allows you to view traffic data instantly, helping you quickly locate exceptional traffic and troubleshoot network failures.

## Network Topology

As shown below, when resources like CVMs within the VPC send outgoing data packets via the NAT gateway, the data will first flow through the router that selects routes based on the routing policies. Subsequently, the NAT gateway will use the bound EIP as the source IP address to send the traffic to the Internet.
![img](https://main.qcloudimg.com/raw/3c4bdc38f992ab789eac9a53ccca9914.png)

## Differences between the NAT Gateway and Public Gateway

A CVM within a VPC can access the Internet through the NAT gateway or public gateway. The differences between the two gateways are shown in the following table.

| Attribute | NAT Gateway | Public Gateway |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------- |
| Availability | Master/slave hot backup, and automatic hot switching | Manual switching of failed gateway |
| Public network bandwidth | Maximum of 5 Gbps | Depends on the network bandwidth of the CVM |
| Public IP | A maximum of 10 EIPs can be bound | One EIP or ordinary public IP |
| Rate limit of public network | N/A | Depends on the rate limit of the CVM |
| Maximum number of connections | 10,000,000 | 500,000 |
| Private IP | Private IPs of VPC users are not occupied | Private IPs of the subnet are occupied |
| Security group     | Binding of a security group is not supported. You can bind a security group to the backend CVM     | Binding of a security group is supported |
| Network ACL | Binding of a network ACL is not supported. You can bind a network ACL to the subnet in which the backend CVM resides | Binding of a network ACL is not supported. You can bind a network ACL to the subnet in which the public gateway resides |

As shown in the above table, the NAT gateway has the following advantages:

- Large capacity
  It supports a maximum of 10,000,000 concurrent connections, 5 Gbps bandwidth, and 10 EIPs to meet the demand of users with a large business scale.
- Highly available master/slave hot backup
  It supports automatic switching when a single server suffers a failure, to allow automatic disaster recovery and 99.99% service availability, superior to the manual switching of a public network gateway.
- Cost effectiveness
  Three configuration types, high, medium, and low, are available for users to choose from as needed, offering flexibility in billing and high cost effectiveness.
