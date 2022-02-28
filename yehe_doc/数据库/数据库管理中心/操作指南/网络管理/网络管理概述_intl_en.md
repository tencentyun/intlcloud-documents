This document describes the network of TencentDB for PostgreSQL. TencentDB for PostgreSQL offers the network management feature to protect your instance security and provide service to internal and external businesses efficiently and freely.

## Network Types
There are two types of TencentDB network environments: VPC and classic network.
- VPC: it is a logically isolated network space that can be customized in Tencent Cloud. Even in the same region, different VPCs cannot communicate with each other by default. Similar to the traditional network in an IDC, a VPC is where your Tencent Cloud service resources are managed.
- Classic network: it is the public network resource pool for all Tencent Cloud users. All your Tencent Cloud resources will be centrally managed by Tencent Cloud.
>?Currently, resources cannot be created in the classic network.

#### Feature comparison

| Feature | Classic Network | VPC |
|---------|---------|---------|
| Custom network | Unsupported | Supported |
| Custom routing | Unsupported  | Supported |
| Custom IP | Unsupported | Supported |
| Interconnection rule | Interconnection in the same region | Interconnection between subnets in the same VPC in the same region |
| Security control | Security group | Security group |

## Network Access
Tencent Cloud services can be accessed over both the public and private networks.
- Public network access: it is a service provided by Tencent Cloud to implement public data transfer for an instance. You can enable the public IP of the instance for it to communicate with other computers and allow access over the public network.
- Private network access: it is used to provide Local Area Network (LAN) service. Tencent Cloud assigns resources with private IP addresses to allow a free private network communication in the same region or instance access over the private network.

>!Security groups that currently support public network access are available only in the Guangzhou, Shanghai, Beijing, and Chengdu regions. Instances in other regions may be attacked if the public network access is enabled. We do not recommend that you enable public network access for instances in production environment. If you need to enable public network access, security group rules must be configured.

## Network Configuration
You can configure one or two networks for each TencentDB for PostgreSQL instance.

In scenarios where the instance supports two networks:
- An instance can be accessed through different VIPs that belong to different VPCs and subnets.
- You can use this feature to change the instance network, for example, from the classic network to VPC or from VPC A to VPC B.
- You can use this feature to implement the multi-plane network feature in scenarios where businesses in two different VPCs need to access the same database instance.

## Managing Instance Network
You can add, delete, and change networks in the TencentDB for PostgreSQL console. For more information, see [Modifying Network](https://intl.cloud.tencent.com/document/product/409/44360).
