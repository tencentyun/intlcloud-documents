Tencent Cloud offers network infrastructure and security services to ensure your business stays secure, efficient, and flexible.

## Encrypted Login
Tencent Cloud provides two encrypted login methods using [Login Password](https://intl.cloud.tencent.com/document/product/213/6093) and [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092). You can use either one of these to connect to your CVM instance. Windows CVM does not support login using SSH keys.

## Network access
Tencent Cloud products can communicate with one another using [Internet Access](https://intl.cloud.tencent.com/document/product/213/5224) or [Private Network Access](https://intl.cloud.tencent.com/document/product/213/5225).
 - Internet Access: CMV instances and other Tencent Cloud products use Internet access to provide public-facing services. They are assigned public IP addresses to communicate with other computers on the Internet.
 - Private Network Access: Tencent Cloud assigns private IP addresses to resources in the same region so they can communicate with one another on the same LAN for free. 

## Network Environment
Tencent Cloud provides two types of [Network Environments](https://intl.cloud.tencent.com/document/product/213/5227): basic network and private networks (VPC).
 - Basic network is a shared networking resource pool for all users. We recommend basic network for beginners.
 - VPCs are custom network spaces that are logically isolated. You can launch CVM instances on a predefined and customized IP range to isolate your resources from those of other users. We recommend VPCs for users who are comfortable with network administration.

## Security Groups
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means of network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances.
The following is a list of typical security group use cases:
 - Create multiple security groups and populate them with different rules.
 - Associate one or more security groups with each of your CVM instances. The system uses these security groups to control traffic to your instances and the resources your instances can access.
 - Configure your security groups so that only specific IP addresses or security groups can access your instances.

## Elastic Public IPs
[Elastic Public IPs](https://intl.cloud.tencent.com/document/product/213/5733), or EIPs, are static IP addresses specially designed for cloud computing.
We recommend using EIPs in the following cases:
 - An instance can go down for unforeseeable reasons, and the failover instance needs to use the same IP address to provide uninterrupted service. 
 - An instance does not have a public IP address but still needs a static IP address.

## ENIs
An [Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/213/6514) is an elastic network interface that can be bound to a CVM instance on a VPC to provide network connection. ENIs can be freely migrated among instances. This is essential when configuring and managing networks and implementing high availability deployments.
