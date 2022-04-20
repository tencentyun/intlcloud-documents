Tencent Cloud provides two network environments, [Virtual Private Cloud](https://intl.cloud.tencent.com/product/vpc) (VPC) and classic network.
For Tencent Cloud accounts created after June 13, 2017, only VPC is available. We recommend you use a VPC for the following reasons:
- Complete features: VPC covers all classic network features, while providing more flexible network services such as custom IP range, routing, Direct Connect, VPN, NAT, etc.
- Smooth migration: There is no completely smooth migration solution in the industry (the need to shut down, change private IP, etc). If you need to use a VPC for business development later, the migration process may affect your business.

## VPC and Classic Network

### VPC

With Tencent Cloud’s [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215), you can customize a logical isolated virtual network on the cloud. Even in the same region, different VPCs cannot communicate with each other by default. Similar to the traditional network that you run in your data center, your Tencent Cloud resources, including [CVM](https://intl.cloud.tencent.com/document/product/213/495), [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524), and [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/5147), are hosted on Tencent Cloud’s VPC to give you full control over the environment. For more information on configuration and application scenarios, see [VPC](https://intl.cloud.tencent.com/document/product/215/535). The VPC helps you build more complex network architecture and is suitable for those who are familiar with network management.

![](https://main.qcloudimg.com/raw/b86b2e3af8e21354d317bb2b4739b47d.jpg)

### Classic network

Classic network is the public network resource pool for all Tencent Cloud users. All your Tencent Cloud resources will be centrally managed by Tencent Cloud.

### Feature differences

| **Feature**| **Classic Network**| **VPC** |
|---------|---------|---------|
| Tenant association | Tenant association | Logical isolated network based on GRE encapsulation |
| Network customization | Not Supported | Supported |
| Routing customization | Not Supported | Supported |
| Custom IP | Not Supported | Supported |
| Interconnection rules | Interconnection is allowed for the same tenant in the same region | Cross-region and cross-account interconnection are supported |
| Security control　| [Security groups](https://intl.cloud.tencent.com/document/product/213/12452)| [Security groups](https://intl.cloud.tencent.com/document/product/213/12452) and [Network ACL](https://intl.cloud.tencent.com/document/product/215/5132) |

## Sharing Between Classic Network and VPC

Some Tencent Cloud resources and features support both the classic network and VPC, and can be shared or accessed via the two different networks.

|**Resource**|**Description**|
|--|--|
|[Image](https://intl.cloud.tencent.com/document/product/213/4940)|An image can be used to launch a CVM instance in any network environment|
|[Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/5733)|Elastic Public IPs can bind to a CVM instance under any network environment|
|Instances|Instances in the classic network and VPC can communicate with each other through the [Public IP](https://intl.cloud.tencent.com/document/product/213/5224) or [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807)|
|[SSH Key](https://intl.cloud.tencent.com/document/product/213/6092)|SSH key supports loading a CVM instance under any network environment|
|[Security Groups](https://intl.cloud.tencent.com/document/product/213/12452)|Security groups support binding CVM instances under any network environment|

> A [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) can not work on both the classic network and VPC, even if the VPC and the classic network are interconnected.

## Migrating from Classic Network to VPC

Please see [Switch to VPC](https://intl.cloud.tencent.com/document/product/213/20278) to migrate instances in the classic network to VPC.
