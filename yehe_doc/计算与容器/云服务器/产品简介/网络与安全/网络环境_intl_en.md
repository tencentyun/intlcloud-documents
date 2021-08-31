Tencent Cloud provides two network environments: [Virtual Private Cloud](https://intl.cloud.tencent.com/product/vpc) (VPC) and basic network.
After June 13, 2017, newly registered account no longer supports the basic network. We recommend you use a VPC for the following reasons:
- Complete features: VPC covers all basic network features, while providing more flexible network services such as custom IP range, routing, Direct Connect, VPN, NAT, etc.
- Smooth migration: There is no completely smooth migration solution in the industry (the need to shut down, change private IP, etc). If you need to use a VPC for business development later, the migration process may affect your business.

## VPC and basic network

### VPC

With Tencent Cloud’s [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215), you can customize a logical isolated virtual network on the cloud. Even in the same region, different VPCs cannot communicate with each other by default. Similar to the traditional network that you run in your data center, your Tencent Cloud resources, including [CVM](https://intl.cloud.tencent.com/document/product/213/495), [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524), and [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/5147), are hosted on Tencent Cloud’s VPC to give you full control over the environment. For more information on configuration and application scenarios, see [VPC](https://intl.cloud.tencent.com/document/product/215/535). The VPC helps you build more complex network architecture and is suitable for those who are familiar with network management.

![](https://main.qcloudimg.com/raw/b86b2e3af8e21354d317bb2b4739b47d.jpg)

### Basic network

Basic network is the public network resource pool for all Tencent Cloud users. All your Tencent Cloud resources will be centrally managed by Tencent Cloud.

### Feature differences

| **Feature**| **Basic Network**| **VPC** |
|---------|---------|---------|
| Tenant association | Tenant association | Logical isolated network based on GRE encapsulation |
| Network customization | Not Supported | Supported |
| Routing customization | Not Supported | Supported |
| Custom IP | Not Supported | Supported |
| Interconnection rules | Interconnection is allowed for the same tenant in the same region | Cross-region and cross-account interconnection are supported |
| Security control　| [Security groups](https://intl.cloud.tencent.com/document/product/213/12452)| [Security groups](https://intl.cloud.tencent.com/document/product/213/12452) and [Network ACL](https://intl.cloud.tencent.com/document/product/215/5132) |

## Sharing and accessing resources between basic network and VPC

Some Tencent Cloud resources and features support both basic network and VPC, and can be shared or accessed via the two different networks.

|**Resource**|**Description**|
|--|--|
|[Image](https://intl.cloud.tencent.com/document/product/213/4940)|An image can be used to launch a CVM instance in any network environment|
|[Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/5733)|Elastic Public IPs can bind to a CVM instance under any network environment|
|Instances|Instances in the basic network and VPC can communicate with each other through the [Public IP](https://intl.cloud.tencent.com/document/product/213/5224) or [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807)|
|[SSH Key](https://intl.cloud.tencent.com/document/product/213/6092)|SSH key supports loading a CVM instance under any network environment|
|[Security Groups](https://intl.cloud.tencent.com/document/product/213/12452)|Security groups support binding CVM instances under any network environment|

> [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) cannot be shared between the basic network and the VPC. Even when the VPC and the basic network are interconnected, Cloud Load Balancer does not support binding instances in VPCs and basic networks at the same time.

## Migrating instances in basic network to VPC

Please see [Switch to VPC](https://intl.cloud.tencent.com/document/product/213/20278) to migrate instances within the basic network to VPC.
