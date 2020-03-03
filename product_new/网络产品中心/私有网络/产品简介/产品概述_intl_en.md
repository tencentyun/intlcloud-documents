Virtual Private Cloud (VPC) is a logically isolated network space customized in Tencent Cloud. Similar to a conventional network in an IDC, the VPC is where your Tencent Cloud service resources are managed, such as [Cloud Virtual Machines](https://cloud.tencent.com/doc/product/213/495), [Cloud Load Balancers](https://cloud.tencent.com/doc/product/214/524), and [TencentDB](https://cloud.tencent.com/doc/product/236).

This document introduces the core components, connection modes, and security of VPC.
## Core Components
A VPC instance has three core components: VPC IP ranges, subnets, and route tables.
### VPC IP Ranges
When you create a VPC, you need to specify a [CIDR (classless inter-domain routing) block](http://intl.cloud.tencent.com/document/product/215/4925) as the VPC’s IP address group.

Tencent Cloud VPC supports CIDR blocks in any of the following private IP ranges:
- **10.0**.0.0 - **10.255**.255.255 (**the mask must range from 16 to 28**)
- **172.16**.0.0 - **172.31**.255.255 (**the mask must range from 16 to 28**)
- **192.168**.0.0 - **192.168**.255.255 (**the mask must range from 16 to 28**)

### Subnets
A VPC should consists of at least one subnet. The CIDR blocks of subnets must be within the CIDR block of the VPC.
A subnet is a network that is used to manage the network plane of an elastic CVM and can provide IP address management, DNS, and other services. All cloud resources (such as CVMs and TencentDB) within the VPC must be deployed in subnets.

A VPC is set up at the [region](https://cloud.tencent.com/document/product/215/20057#.E5.9C.B0.E5.9F.9F.EF.BC.88region.EF.BC.89) level (such as Guangzhou ), while a subnet is set up at the [availability zone](https://cloud.tencent.com/document/product/215/20057#.E5.8F.AF.E7.94.A8.E5.8C.BA.EF.BC.88zone.EF.BC.89) level (such as Guangzhou Zone 1). Subnets in a VPC can belong to different availability zones within the same region, and resources in all subnets under a VPC can interconnect with private networks by default regardless of they are in the same availability zone or not.

Elastic CVMs in different VPC instances can communicate with each other by establishing [peering connections](https://cloud.tencent.com/document/product/553) or creating [CCN](https://cloud.tencent.com/document/product/877).
![](https://main.qcloudimg.com/raw/9ab6da241dc050a0bb8f33f48859b1f1.png)

### Route Tables
A route table consists of multiple routing policies and is used for controlling outbound traffic routes of subnets in the VPC. Each subnet can be associated with one route table, while each route table can be associated with multiple subnets. You can create multiple route tables for subnets with different traffic routes.

A route table controls traffic routes by using routing policies. A routing policy consists of the destination, next-hop type, and next hop.
- **Destination**: refers to the target IP range to which you want to forward traffic. Destination IP range description supports only the IP range format. If you want the destination to be a single IP address, you can set the mask to `32` (such as `172.16.1.1/32`). The destination cannot be the IP range in the VPC of the route table, because local routing already indicates default private network intercommunication in this VPC.
- **Next-hop type**: indicates the egress for data packets of the VPC. The next-hop type of VPC supports **NAT gateway**, **Peering connection**, **VPN gateway**, **Direct connect gateway**, **CVM**, and others.
- **Next hop**: specifies the next hop instance (represented by using the next-hop ID), such as a NAT gateway in a VPC.


## VPC Connections
Tencent Cloud provides an extensive range of solutions to enable instances within a VPC, such as CVMs and databases, to connect to the Internet, connect to instances in other VPC instances, or interconnect with local IDCs.

For more information on VPC connection modes, see [VPC Connections](https://cloud.tencent.com/document/product/215/37053).

## VPC Security
Based on the OverLay technology, VPC constructs logically isolated network spaces in the cloud. The networks for different tenants and different VPC instances are isolated from each other to ensure customers’ business security.
- Security group: a security group is a stateful virtual firewall for filtering packets that can control the data streams of one or more instances.
- Permission control: VPC supports minimum authorization for accounts through CAM and provides permission control features targeted to accounts, instances, and APIs.
- Network Access Control List (ACL): a network ACL is a stateless virtual firewall for filtering packets at the subnet level. It can be used to control the inbound and outbound data streams of subnets.

For more information on VPC security, see [Security](https://cloud.tencent.com/document/product/215/20087).
