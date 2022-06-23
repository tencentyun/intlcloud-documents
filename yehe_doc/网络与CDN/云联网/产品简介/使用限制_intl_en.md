## Limits on the Multi–Route Table Feature in Beta Test
CCN's multi–route table and route table selection policy features (hereinafter referred to as the multi–route table feature) are currently in beta test. Relevant documents are available only to beta users for reference. Users that are not included in the beta test need to wait until the feature is officially commercialized.
Currently, the multi–route table feature is available only in some test regions. It also has the following limits:

- The multi–route table feature can be tested by CCN instance. You can submit the ID of a CCN instance to Tencent Cloud for evaluation. After the CCN instance passes the evaluation, we will contact you to start testing.
- The multi–route table feature cannot be tested on CCN instances bound with SD-WAN access service Edge devices.
- Route table selection policies take effect only for CCN's cross-region traffic and direct connect gateway–based traffic.


## Resource Limits
The following table lists the limits on the supported CCN resources. For limits on other Virtual Private Cloud (VPC) products, see [Quota Limit](https://intl.cloud.tencent.com/document/product/215/38959).
<table>
<tr>
<th>Resource</th>
<th>Limit</th>
</tr>
<tr>
<td>Number of CCN instances per account</td>
<td>5</td>
</tr>
<tr>
<td>Number of network instances that can be associated with one CCN instance</td>
<td>25 </td>
</tr>
</table>

## Feature Limits
**Non-transitivity of peering connections**
A peering connection does not affect the interconnection between a CCN instance and VPC instances associated with it. A CCN instance distributes routes only to the network instances associated with it for interconnection.
For example, as shown in the following figure, a peering connection has been established between VPC1 and VPC2. After VPC1 is associated with a CCN instance, only VPC1 can interconnect with network instances VPC3 and IDC associated with the CCN instance, while VPC2 can only interconnect with VPC1 through the peering connection, but not other instances associated with the CCN instance.
![](https://main.qcloudimg.com/raw/f764269dbb106d6f6f47bd8470bb3aa5.png)

## Route Limits
To ensure that network instances in CCN are interconnected, CCN restricts the CIDR blocks of the network instances.

### Limits on VPC CIDR blocks
CCN restricts CIDR blocks at the subnet level: Two subnets with identical CIDR blocks in different VPCs cannot interconnect with each other (see "Rules for CIDR overlapping conflicts" below). Accordingly, even if the CIDR blocks of two VPCs overlap, as long as their subnets have different CIDR blocks, you can still associate them with a CCN instance for interconnection.

### Rules for CIDR overlapping conflicts
1. If the CIDR blocks of network instances overlap, only the route of the network instance that is first associated with the CCN instance will take effect.
2. For a network instance already in a CCN instance, if a route conflict occurs due to operations such as subnet creation, the new route will not take effect, and the existing valid route will remain valid.

**Solution**:
 + Evaluate the network condition, disable/delete the conflicting route, and enable the route needed.
 + Change the IP range to ensure that there is no IP range overlapping between the subnets that need to interconnect with each other through a CCN instance. For example, you can change the CVM instance network to another subnet or VPC with a non-conflicting IP range and then use a CCN instance for interconnection. For more information, see [Changing Instance Subnet](https://intl.cloud.tencent.com/document/product/213/16565) and [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### Rules for CIDR inclusive conflicts
If the CIDR blocks of multiple network instances have an inclusive conflict, only the route of the network instance that is first associated with the CCN instance will take effect. 

**Solution**:
 + You can enable invalid routes in the route table, which, once enabled, will forward data based on the longest mask matching rule.
 + Change the IP range to ensure that there is no inclusive conflict between the subnets that need to interconnect with each other through a CCN instance. For example, you can change the CVM instance network to another subnet or VPC with a non-conflicting IP range and then use a CCN instance for interconnection. For more information, see [Changing Instance Subnet](https://intl.cloud.tencent.com/document/product/213/16565) and [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).


#### Example of an inclusive conflict
Assume that VPC1 is first associated with CCN instance A, the CIDR block of its subnet A is `10.0.1.0/20`, and VPC1 can interconnect with other instances in CCN instance A. Then, VPC2 is associated with CCN instance A, and the CIDR block of its subnet B is `10.0.1.0/24`, which is included in the CIDR block of subnet A in VPC1. In this case, a CIDR block inclusive conflict occurs. As a result, the routing policy of subnet B in VPC2 will become invalid by default, and VPC2 cannot interconnect with other network instances in CCN instance A.

However, you can enable this invalid route in the CCN route table, which can forward data according to the longest mask matching rule. If the destination IP address of the routing policy is `10.0.1.0/24`, the data will be forwarded to subnet B in VPC2 based on the rule.

