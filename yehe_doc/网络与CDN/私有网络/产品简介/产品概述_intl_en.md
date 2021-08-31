A Virtual Private Cloud (VPC) is a logically isolated network space. With VPC, you can configure logically isolated network space for your resources such as [CVMs](https://intl.cloud.tencent.com/document/product/213/495) and [cloud databases](https://intl.cloud.tencent.com/document/product/236). This product provides better cloud resource security and can meet your needs in various scenarios.

This document introduces the core components, connection modes, and security of VPCs.
## Core Components
A VPC instance has three core components: VPC IP ranges, subnets, and route tables.
### VPC IP ranges
When you create a VPC, you need to specify a [CIDR (classless inter-domain routing) block](http://intl.cloud.tencent.com/document/product/215/4925) as the VPC’s IP address group.

Tencent Cloud VPC supports CIDR blocks in any of the following private IP ranges:
- **10.0**.0.0 - **10.255**.255.255 (**the mask range must be 16 to 28**)
- **172.16**.0.0 - **172.31**.255.255 (**the mask range must be 16 to 28**)
- **192.168**.0.0 - **192.168**.255.255 (**the mask range must be 16 to 28**)

### Subnets
A VPC is made up of at least one subnet. All cloud resources in a VPC (such as CVMs and cloud databases) must be deployed in a subnet, and the subnet CIDR block must be within the VPC CIDR block.

A VPC is set up at the [region](https://intl.cloud.tencent.com/document/product/215/31786) level (such as Guangzhou), while a subnet is set up at the [availability zone](https://intl.cloud.tencent.com/document/product/215/31786) level (such as Guangzhou Zone 1). You can divide a VPC into one or more subnets. Subnets in the same VPC can interconnect with one another by default, while subnets in different VPCs are isolated by default.
![](https://main.qcloudimg.com/raw/9fe1af6b2ee439449a6fefa64663215c.png)

### Route tables
When you create a VPC, the system automatically generates a default route table to ensure that all subnets in the VPC interconnected. If the routing policies in the default route table cannot meet your business needs, you can create a custom route table.

For more information on route tables, see [Route Table Overview](https://intl.cloud.tencent.com/document/product/215/31810).

## VPC Connections
Tencent Cloud provides a wide range of VPC connection solutions for different scenarios.
- CVMs and cloud databases in a VPC can connect to the Internet via Elastic IP and NAT Gateway.
- Peering Connection and Cloud Connect Network are used to enable communication between VPCs.
- VPCs and local IDCs are interconnected through VPN Connection, Direct Connect, and Cloud Connect Network. 


## VPC Security
A VPC is a logically isolated network space in the cloud. Different VPCs are isolated from each other to protect business security.
- Security group: a security group is a stateful virtual firewall capable of packet filtering. It controls inbound and outbound traffic at the instance level and is an important means of network security isolation.
- Network Access Control List (ACL): a network ACL is a stateless virtual firewall for filtering packets at the subnet level. It can be used to control the inbound and outbound data streams of subnets at the protocol and port granularity.
- Cloud Access Management (CAM): CAM helps you securely manage access to your Tencent Cloud resources. For example, CAM provides identity management and policy management so you can control who has access to your VPCs.

For more information on VPC security, see [Security Management](https://intl.cloud.tencent.com/document/product/215/31848).
