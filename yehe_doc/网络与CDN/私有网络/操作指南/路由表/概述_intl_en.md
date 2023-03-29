A route table consists of multiple routing policies that control the outbound traffic direction of subnets in the VPC. Each subnet can only be associated with one route table, while each route table can be associated with multiple subnets. You can create multiple route tables for subnets with different traffic routes.

## Types
There are two types of route tables: default and custom. 
- **Default route table**: When you create a VPC, the system automatically generates a default route table, which will be associated with subnets created later if no custom route table is selected. You cannot delete the default route table, but you can add, delete, and modify routing policies in it.
- **Custom route table**: You can create or delete a custom route table in the VPC. This custom route table can be associated with all the subnets to apply the same routing policy.
![]()
>?You can associate a route table when [creating a subnet](https://intl.cloud.tencent.com/document/product/215/31806), or [changing the route table](https://intl.cloud.tencent.com/document/product/215/40090) after a subnet is created.
>

## Routing Policy
A route table controls traffic routes by using routing policies. A routing policy consists of the destination, next-hop type, and next hop:
- **Destination**: Specifies the destination IP range to which you want to forward the traffic. It should be an IP range. If you want to enter a single IP address, set the mask to `32` (for example, `172.16.1.1/32`). The destination cannot be an IP range of the VPC where the route table resides, because the local route already allows private network interconnection in this VPC.
>?
>+ If you have [Tencent Kubernetes Engine](https://intl.cloud.tencent.com/document/product/457/6759) deployed in your VPC, when you create a route table policy for the VPC subnet, the destination range cannot be within the VPC IP range or the [container IP range](https://intl.cloud.tencent.com/document/product/457/38966).
>+ If the container network and VPC routes overlap, traffic will be preferentially forwarded within the container network.
- **Next-hop type**: Indicates the egress of data packets for the VPC. The next-hop type of VPC supports **NAT Gateway**, **Peering connection**, **VPN Gateway**, **Direct Connect gateway**, **CVM**, and others.
- **Next hop**: Specifies the next hop instance (identified by the next-hop ID) to which the traffic is forwarded, such as a NAT gateway in the VPC.


### Routing policy priority
When there are multiple routing policies in a route table, the following routing priority applies, from high to low:
- Traffic within the VPC: Traffic within the VPC is matched first.
- Exact match route (the longest prefix match): When there are multiple routes in the route table that can match the destination IP, the route with the longest (exact) mask is matched to determine the next hop.
- Public IP: If no routing policy is matched, a CVM instance can access the internet through its public IP address.
**Use case:**
When a subnet is associated with a NAT gateway, and the CVM instance in the subnet has a public IP (or EIP), the CVM instance accesses the internet through the NAT gateway by default (because the priority of the exact match route is higher than that of the public IP). However, you can set a routing policy to allow the CVM instance to access the internet through its public IP address. For more information, see [Adjusting the Priorities of NAT Gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).

## ECMP 
Equal-cost multipath (ECMP) routing means there are multiple equal-cost routes to a single destination. The traditional routing technology only uses one path to transfer packets to the same destination, while the remaining paths are in the standby or invalid status. When the path fails, it takes time to switch to another path. By contrast, ECMP uses multiple equal-cost routes in the network environment to increase the transfer bandwidth, balance traffic over multiple routes, and achieve backup with redundant linkages.

- ECMP with VPC routes of the same type is as detailed below:
<table>
<tr>
<th>Next hop type</th>
<th>Whether ECMP Is Formed with Routes of the Same Type</th>
<th>Maximum Number of Routes Supported by ECMP</th>
</tr>
<tr>
<td>NAT Gateway</td>
<td>Yes</td>
<td>N/A</td>
</tr>
<tr>
<td>CVM public IP</td>
<td>No</td>
<td>N/A</td>
</tr>
<tr>
<td>CVM</td>
<td>Yes</td>
<td>Up to eight routes of the same type</td>
</tr>
<tr>
<td>Peering connection</td>
<td>No</td>
<td>N/A</td>
</tr>
<tr>
<td>Direct Connect gateway</td>
<td>No</td>
<td> N/A</td>
</tr>
<tr>
<td>CCN</td>
<td>No</td>
<td> N/A</td>
</tr>
<tr>
<td>HAVIP</td>
<td>Yes</td>
<td>Up to eight routes of the same type</td>
</tr>
<tr>
<td>VPN Gateway</td>
<td>Yes</td>
<td>Up to eight routes of the same type</td>
</tr>
</table>
- ECMP with VPC routes of different types is as detailed below:
  + NAT gateways and CVM instances can form the ECMP.
  + If there is already a self-learning CCN route, when a configured custom route to a Direct Connect gateway/peering connection is added, CCN and the Direct Connect gateway/peering connection can form the ECMP.
  + If there is already a custom route for the Direct Connect gateway/peering connection, and you want to form the ECMP with CCN, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.



### Use cases
ECMP is often used to balance the traffic load over gateways with a limited bandwidth. Assume that you need 2,000 Mbps to interconnect your VPC-based and IDC-based businesses, but the current maximum VPN bandwidth is 1,000 Mbps. To achieve the goal, you can create two 1,000-Mbps VPN gateways and two VPN tunnels.

## Primary/Secondary Routes
Primary and secondary routes refer to two or more paths to the same destination with only one active path. Assume there are two VPC routes to the IDC, that is, paths A and B. All packets are sent to the destination via path A, while path B is invalid or on standby. When path A suffers linkage failures, you can switch to path B to take over traffic from path A, thus ensuring business availability. In this case, paths A and B are called primary and secondary routes.

The next hop type determines the route priority. When adding a routing policy to the VPC route table, you can configure different types of gateways to act as primary and secondary routes to a single destination. Then, the VPC network probe can be used to check the linkage quality and accessibility. After configuring an alarm policy, you can promptly detect any linkage exception and quickly switch between primary and secondary routes to meet the high availability requirements.
>?
>+ VPC does not have the route priority feature by default. This feature is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>+ The next hop type determines the route priority in the VPC route table. By default, the route priority from high to low is CCN, Direct Connect gateway, VPN Gateway, and others.
>+ Currently, you cannot adjust the route priority in the console. If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

The following table describes the primary/secondary support of different types of VPC routes:

| Next Hop Type         | Support for Primary/Secondary Routes                                            |
| ------------------ | ------------------------------------------------------- |
| NAT Gateway            | No                                                      |
| Public IP of CVM     | No                                                      |
| CVM          | Yes, with CCN, VPN Gateway, Direct Connect gateway, or HAVIP  |
| Peering connection (intra-region) | No                                                      |
| Peering connection (cross-region) | No                                                      |
| Direct Connect gateway          | Yes, with CCN, VPN Gateway, HAVIP, or CVM  |
| CCN          | Yes, with VPN Gateway, Direct Connect gateway, HAVIP, or CVM  |
| HAVIP          | Yes, with CCN, VPN Gateway, Direct Connect gateway, or CVM  |
| VPN Gateway         | Yes, with CCN, Direct Connect gateway, HAVIP, or CVM  |


### Use cases
Primary and secondary routes are often used to smoothly forward traffic when a gateway linkage fails, for example:
+ VPC-based Direct Connect gateway (primary) and VPN gateway for VPC (secondary)
  **Scenario**: Interconnect a Tencent Cloud VPC and an on-premises IDC through a VPC-based Direct Connect gateway. Meanwhile, create VPN tunnels through a VPN gateway to act as the secondary communication linkage between the IDC and VPC.
  ![](https://main.qcloudimg.com/raw/683779ec1aef376985b027df945fe54c.png)
+ CCN-based Direct Connect gateway (primary) and VPN gateway for VPC (secondary)
  **Scenario**: Interconnect a Tencent Cloud VPC and an on-premises IDC through a CCN instance. Meanwhile, create VPN tunnels through a VPN gateway to act as the secondary communication linkage between the IDC and VPC.
	![](https://main.qcloudimg.com/raw/7e21527a285edb29c7e57df566723acb.png)
