A route table consists of multiple routing policies that control the outbound traffic direction of subnets in the VPC. Each subnet can only be associated with one route table, while each route table can be associated with multiple subnets. You can create multiple route tables for subnets with different traffic routes.

## Types
There are two types of route tables: default and custom. 
- **Default route table**: when you create a VPC, the system automatically generates a default route table, which will be associated with subnets created later if no custom route table is selected. You cannot delete the default route table, but you can add, delete, and modify routing policies in it.
- **Custom route table**: you can create or delete a custom route table in the VPC. This custom route table can be associated with all the subnets to apply the same routing policy.
![](https://main.qcloudimg.com/raw/a86260ffb40bec52c9f64a307d956691.png)  
>?You can associate a route table when [creating a subnet](https://intl.cloud.tencent.com/document/product/215/31806), or [changing the route table](https://intl.cloud.tencent.com/document/product/215/40090) after a subnet is created.
>

## Routing Policy
A route table controls traffic routes by using routing policies. A routing policy consists of the destination, next-hop type, and next hop.
- **Destination**: specifies the destination IP range to which you want to forward traffic. It should be an IP range. If you want to enter a single IP address, set the mask to `32` (for example, `172.16.1.1/32`). The destination cannot be an IP range of the VPC where the route table resides, because the local route already allows private network interconnection in this VPC.
>?If you have deployed a [TKE service](https://intl.cloud.tencent.com/document/product/457/6759) in the VPC, the destination you configure in the routing policy of the VPC subnet cannot fall within the VPC CIDR block or contain the TKE IP range.
>For example, if the VPC CIDR block is `172.168.0.0/16` and the TKE CIDR block is `192.168.0.0/16`, the destination IP range cannot fall within `172.168.0.0/16`, or contain `192.168.0.0/16` when you configure routing policy for a VPC subnet.
>
- **Next-hop type**: indicates the egress of data packets for the VPC. The next-hop type of VPC supports **NAT Gateway**, **Peering connection**, **VPN gateway**, **Direct connect gateway**, **CVM**, and others.
- **Next hop**: specifies the next hop instance (identified by the next-hop ID) to which the traffic is forwarded, such as a NAT Gateway in a VPC.


### Routing policy priority
When there are multiple routing policies in a route table, the following routing priority applies, from high to low:
- Traffic within VPC: traffic within VPC is matched first.
- Exact match route (the longest prefix match): when there are multiple routes in the route table that can match the destination IP, the route with the longest (exact) mask is matched to determine the next hop.
- Public IP: if no routing policy is matched, a CVM instance can access the Internet through its public IP address.
**Use case:**
When a subnet is associated with a NAT Gateway, and the CVM in the subnet has a public IP (or EIP), the CVM accesses the Internet through the NAT Gateway by default (because the priority of the exact match route is higher than that of the public IP). However, you can set a routing policy to allow the CVM to access the Internet by using its public IP address. For details, see [Adjusting the Priorities of NAT Gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).

## ECMP 
Equal-cost Multipath Routing (ECMP) means there are multiple equal-cost routes to a single destination. The traditional routing technology only uses one path to transfer packets to the same destination, while the remaining paths are in the standby or invalid status. When the path fails, it takes time to use another path. By contrast, ECMP uses multiple equal-cost routes in the network environment to increase the transmission bandwidth, balance traffic over multiple routes, and achieve backup with redundant linkages.

VPC supports ECMP for the same type of routes, as detailed below.

| Next hop type     | Support ECMP (same route type)  | Maximum number of ECMPs |
| -------------- | ----------------------- | --------------------------- |
| NAT Gateway        | No                       | N/A                 |
| Public IP of CVM | No                     | N/A                 |
| CVM       | Yes                    | 8       |
| Peering connection       | No                     | N/A                 |
| Direct connect gateway       | Yes                     | 8       |
| CCN         | No                    | N/A                 |
| HAVIP   | Yes                    | 8       |
| VPN gateway        | Yes                      | 8       |

<dx-alert infotype="explain" title="">
CCN supports one ECMP with direct connect gateway or peering connection.
</dx-alert>


### Use cases
ECMP is often used to balance the traffic load over gateways with a limited bandwidth. Assume that you need 2000 Mbps to interconnect your VPC-based and IDC-based businesses, but the current maximum VPN bandwidth is 1000 Mbps. To achieve the goal, you can create two 1000-Mbps VPN gateways and two VPN tunnels.

## Primary/Secondary Routes
Primary/secondary routes refer to two or more paths to the same destination, with one active path and standby or invalid paths. Assume there are two VPC routes to the IDC, that is, path A and path B. All packets are sent to the destination via the path A, while path B is invalid or standby. When the path A suffers linkage failures, you can enable the path B to take over traffic from the path A, thus ensuring the application availability. In this case, paths A and B are called primary and secondary routes.

The next hop type determines the route priority. When adding a routing policy to the VPC route table, you can configure different types of gateways to act as primary and secondary routes to a single destination. Then, the VPC network probe can be used to check the linkage quality and accessibility. After configuring an alarm policy, you can promptly detect any linkage exception and quickly switch between primary and secondary routes to meet the high availability requirements.
>?
>+ The route priority feature is currently in beta. To use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>+ The next hop type determines the route priority in the VPC route table. By default, the route priority from high to low is CCN, direct connect gateway, VPN gateway, and others.
>+ Currently, you cannot adjust the route priority in the console. If needed, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

The following table describes the primary/secondary support of different types of VPC routes.

| Next hop type         | Support for primary/secondary routes                                            |
| ------------------ | ------------------------------------------------------- |
| NAT Gateway            | No                                                      |
| Public IP of CVM     | No                                                      |
| CVM          | Yes, with CCN, VPN gateway, direct connect gateway, or HAVIP  |
| Peering connection (intra-region) | No                                                      |
| Peering connection (cross-region) | No                                                      |
| Direct connect gateway          | Yes, with CCN, VPN gateway, HAVIP, or CVM  |
| CCN          | Yes, with VPN gateway, direct connect gateway, HAVIP, or CVM  |
| HAVIP          | Yes, with CCN, VPN gateway, direct connect gateway, or CVM  |
| VPN gateway         | Yes, with CCN, direct connect gateway, HAVIP, or CVM  |


### Use cases
The primary/secondary routes are often used to smoothly forward traffic when a gateway linkage fails.
+ VPC-based direct connect gateway (primary) and VPN gateway for VPC (secondary)
  **Scenario**: interconnect a Tencent Cloud VPC and an on-premise IDC through a VPC-based direct connect gateway. Meanwhile, create VPN tunnels through a VPN gateway to act as the secondary communication linkage between IDC and VPC.
   ![](https://main.qcloudimg.com/raw/683779ec1aef376985b027df945fe54c.png)
+ CCN-based direct connect gateway (primary) and VPN gateway for VPC (secondary)
  **Scenario**: interconnect a Tencent Cloud VPC and an on-premise IDC through a CCN instance. Meanwhile, create VPN tunnels through a VPN gateway to act as the secondary communication linkage between IDC and VPC.
	![](https://main.qcloudimg.com/raw/7e21527a285edb29c7e57df566723acb.png)
