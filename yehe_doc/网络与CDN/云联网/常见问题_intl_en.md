## Concepts

### What are the use cases of CCN?
CCN bridges between Tencent Cloud VPCs and between VPCs and local IDCs. It provides capabilities such as public and private network multi-point interconnection, self-learning routing, linkage prioritization, and failure fast convergence to meet requirements for **cross-account**, **cross-region**, and **multi-network** high-quality resource interconnection.
Typical use cases of CCN include building a hybrid cloud, online education, and gaming acceleration. For more information, see [Use Cases](https://intl.cloud.tencent.com/document/product/1003/30051).

## Billing

### How is intra-region interconnection between CCN instances billed?
Bandwidth of 5 Gbps or less in the same region (same account or cross account) is free of charge. If you need more than 5 Gbps of bandwidth in the same region, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### How is cross-region interconnection between CCN instances billed?
CCN is billed according to the interconnection bandwidth, and supports pay-as-you-go by monthly 95th percentile. CCN supports three service levels - Platinum, Gold, and Silver. You can choose a plan that best meets your cost and quality requirements.
Cross-region interconnection incurs fees, which are related to the service level. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).


### How is cross-account interconnection between CCN instances billed?
Cross-account fees are paid by the account to which CCN instances belong. For example, if user A creates a CCN instance and user B applies to associate with the CCN instance, user A pays the fee for the CCN instance.

### What are the service levels for CCN?
Tencent Cloud CCN provides three service levels, including Platinum, Gold, and Silver.
- The service level for the same region is "Gold" and cannot be modified.
- Three levels are applied for cross-region interconnection. You can select the service level when creating a CCN instance.
Costs vary with service levels. You can select a service level based on your business needs. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).

### How do I view the details of the bandwidth usage based on the monthly 95th percentile billing mode?
CCN provides details of the bandwidth usage based on the monthly 95th percentile billing mode for cross-region network instance interconnection to help you accurately quantify the bandwidth consumption of each network instance and easily calculate the bandwidth costs. For detailed directions, see [Downloading Usage Details](https://intl.cloud.tencent.com/document/product/1003/47888).

## Features
### When I purchase or configure CCN bandwidth, do I need to distinguish between the directions of the two regions associated with the CCN instance?
After creating a CCN instance and associating it with two network instances, you need to configure bandwidth to enable interconnection between the two network instances. When configuring the bandwidth, you do not need to distinguish between the directions of the two network instance regions. The interconnection between the two regions is related only to the names of the two regions, not their locations. For detailed directions, see [Configuring Bandwidth](https://intl.cloud.tencent.com/document/product/1003/38894).

### How do I increase bandwidth?
For pay-as-you-go CCN instances billed by monthly 95th percentile, you can adjust the bandwidth in the console. For detailed directions, see [Managing Bandwidth](https://intl.cloud.tencent.com/document/product/1003/38895).

### How do I migrate a peering connection or a direct connect to CCN?
You can associate the corresponding network instance with the CCN instance and then implement smooth migration by disabling and re-enabling the related route. For more information, see [Migrating VPCs with Peering Connection to CCN](https://intl.cloud.tencent.com/document/product/1003/30078).

### How do I enable private network interconnection between two CVM instances?
By default, private networks in the same VPC can interconnect with each other, but private networks in different VPCs cannot. To enable interconnection between private networks in different VPCs, follow the directions below:
<dx-steps>
- Create a CCN instance.
- Associate the CCN instance with network instances (for example, two VPC instances that need to interconnect with each other).
- Check the route table
- Configure the bandwidth
</dx-steps>

<dx-alert infotype="explain" title="">
To enable cross-account and cross-VPC CVM instance interconnection through a CCN instance, the VPC account needs to submit an application for CCN instance association. The interconnection is established only after the application is approved. For more information, see [Network Instance Interconnection in One Account](https://intl.cloud.tencent.com/document/product/1003/31986) and [Network Instance Interconnection Across Accounts](https://intl.cloud.tencent.com/document/product/1003/31987).
</dx-alert>

### How do I associate a cross-account VPC instance?
For cross-account VPC instance association, the VPC account needs to initiate an association application, and the CCN account can approve or reject the application. For detailed directions, see [Associating a Cross-Account VPC](https://intl.cloud.tencent.com/document/product/1003/30076).

### What are the restrictions on IP ranges for CCN-based interconnection between VPC IP ranges?
CCN can enable multiple network instances to interconnect with each other, but there are certain limits on the CIDR blocks of the network instances.
**Limits on VPC CIDR blocks:**
CCN restricts CIDR blocks at the subnet level: Two subnets with identical CIDR blocks in different VPCs cannot interconnect (see below for route validity rules); accordingly, even if the CIDR blocks of two VPCs overlap, as long as their subnets have different CIDR blocks, you can still add them to CCN for interconnection.

For VPC subnets, if CIDR blocks that communicate with other have **overlapping** or **inclusive** conflicts, the following rules apply:
- Rules for CIDR overlapping conflict
If the CIDR blocks of network instances overlap, only the route of the network instance that is first associated with the CCN instance will take effect.
For a network instance already in CCN, if a route conflict occurs due to operations such as subnet creation, the new route will not take effect, and the existing valid route will remain valid.
- Rules for CIDR inclusive conflict
If the CIDR blocks of multiple network instances have an inclusive conflict, only the route of the network instance that is first associated with the CCN instance will take effect. However, you can enable invalid routes in the route table, which, once enabled, will forward data based on the longest mask matching rule.

 For more information on the association limits, see [Use Limits](https://intl.cloud.tencent.com/document/product/1003/30052).


### How do I address the IP range conflicts between VPC instances associated with a CCN instance?
- For an IP range overlapping conflict, you can disable/delete the conflicting route in the route table as required and enable the route needed.
- For an IP range inclusive conflict, you can enable the route needed in the route table, which, once enabled, will forward data based on the longest mask matching rule.
- You can also directly change the IP range, that is, change the subnet of the CVM instance to another subnet or directly change to another private network, to ensure that there is no IP range overlapping or inclusive conflict between the subnets. Then associate the subnets with a CCN instance to enable interconnection between them. For more information, see [Changing Instance Subnet](https://intl.cloud.tencent.com/document/product/213/16565) and [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### How do I implement private network interconnection between Lighthouse instances?
Lighthouse uses the VPC automatically assigned by Tencent Cloud for network isolation. By default, Lighthouse instances cannot interconnect with other Tencent Cloud resources in VPCs such as CVM and TencentDB over the private network, and their interconnection needs to be implemented by associating a CCN instance. For more information, see [Private Network Interconnection](https://intl.cloud.tencent.com/document/product/1103/41396).
>?Lighthouse instances can be associated with CCN instances under the same account only. Cross-account Lighthouse instances cannot be interconnected.
>

### How can I resolve the failure of private network interconnection of CCN?
After connecting two VPCs through CCN, it is found that the network `ping` fails. For troubleshooting, see [Network Failure After Connecting Two VPCs Through CCN](https://intl.cloud.tencent.com/document/product/1003/47892).

### Can the invalid routes in the CCN be deleted?
The routes in the CCN are automatically delivered, and there is no **Delete** button in the console.

### Can CCN only be implemented on Tencent Cloud?
Tencent Cloud CCN can be supported not only on Tencent Cloud but also on other clouds. Competitor VPCs and IDCs can be connected through VPNs or direct connect gateways.


## Cross-MLC-Border Service
### What is a cross-MLC-border service?
Currently, CCN supports the cross-MLC-border linkage (the Chinese Mainland - Hong Kong, China) operated by CUCC.

### How do I apply for the qualification review for the CUCC cross-MLC-border service?
Users need to apply for CCN private network cross-MLC-border interconnection. Currently, this service is available to the authenticated enterprise users only. For more information, see [Configuring Bandwidth](https://intl.cloud.tencent.com/document/product/1003/38894#kjdk).
