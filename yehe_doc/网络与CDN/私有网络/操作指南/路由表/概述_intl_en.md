A route table consists of multiple routing policies that control the outbound traffic direction of subnets in the VPC. Each subnet can only be associated with one route table, while each route table can be associated with multiple subnets. You can create multiple route tables for subnets with different traffic routes.

## Types
There are two types of route tables: default and custom. 
- **Default route table**: when you create a VPC, the system automatically generates a default route table, which will be associated with subnets created later if no custom route table is selected. You cannot delete the default route table, but you can add, delete, and modify routing policies in it.
- **Custom route table**: you can create or delete a custom route table in the VPC. This custom route table can be associated with all the subnets to apply the same routing policy.
>?You can associate a route table when [creating a subnet](https://intl.cloud.tencent.com/document/product/215/31806), or [changing the route table](https://intl.cloud.tencent.com/document/product/215/40090) after a subnet is created.

## Routing Policy
A route table controls traffic routes by using routing policies. A routing policy consists of the destination, next-hop type, and next hop.
- **Destination**: specifies the destination IP range to which you want to forward traffic. It should be an IP range. If you want to enter a single IP address, set the mask to `32` (for example, `172.16.1.1/32`). The destination cannot be an IP range of the VPC where the route table resides, because the local route already allows private network interconnection in this VPC.
>?If you have deployed a [TKE service](https://intl.cloud.tencent.com/document/product/457/6759) in the VPC, the destination you configure in the routing policy of the VPC subnet cannot fall within the VPC CIDR block or contain the TKE IP range.
>For example, if the VPC CIDR block is `172.168.0.0/16` and the TKE CIDR block is `192.168.0.0/16`, the destination IP range cannot fall within `172.168.0.0/16`, or contain `192.168.0.0/16` when you configure routing policy for a VPC subnet.
- **Next-hop type**: indicates the egress of data packets for the VPC. The next-hop type of VPC supports **NAT Gateway**, **Peering connection**, **VPN gateway**, **Direct connect gateway**, **CVM**, and others.
- **Next hop**: specifies the next hop instance (identified by the next-hop ID) to which the traffic is forwarded, such as a NAT Gateway in a VPC.


### Routing policy priority
When there are multiple routing rules in a routing table, the following routing priority applies:
- Traffic within VPC: traffic within VPC is matched first.
- Exact match route (the longest prefix match): when there are multiple routes in the route table that can match the destination IP, the route with the longest (exact) mask is matched to determine the next hop.
- Public IP: if no routing policy is matched, a CVM instance can access the Internet through its public IP address.

**Use case:**
When a subnet is associated with a NAT Gateway, and the CVM in the subnet has a public IP (or EIP), the CVM accesses the Internet through the NAT Gateway by default (because the priority of the exact match route is higher than that of the public IP). However, you can set a routing policy to allow the CVM to access the Internet by using its public IP address. For details, see [Adjusting the Priorities of NAT Gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).


