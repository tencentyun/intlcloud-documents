A route table consists of multiple routing policies and is used for controlling outbound traffic routes of subnets in the VPC. Each subnet can be associated with one route table, while each route table can be associated with multiple subnets. You can create multiple route tables for subnets with different traffic routes.

## Type
There are two types of route tables: default route tables and custom route tables:
- When a user creates a VPC, the system will automatically generate a default route table for it. A subnet created later is automatically associated with the default route table if no custom route table is selected. You cannot delete the default route table, but you can add, delete, and modify routing policies in it.
- You can create a custom route table in VPC, and custom route tables can be deleted. You can establish a custom route table for subnets with the same routing policy and associate the route table with all subnets that need to follow this routing policy.
  

You can associate a route table when [creating a subnet](https://intl.cloud.tencent.com/document/product/215/31806), or [changing the route table associated with a subnet](https://intl.cloud.tencent.com/document/product/215/31806) after a subnet is created.

## Routing Policy
A route table controls traffic routes by using routing policies. A routing policy consists of the destination, next-hop type, and next hop.
- **Destination**: refers to the target IP range to which you want to forward traffic. Destination IP range description supports only the IP range format. If you want the destination to be a single IP address, you can set the mask to `32` (such as `172.16.1.1/32`). The destination cannot be the IP range in the VPC of the route table, because local routing already indicates default private network intercommunication in this VPC.
- **Next-hop type**: indicates the egress for data packets of the VPC. The next-hop type of VPC supports **NAT gateway**, **Peering connection**, **VPN gateway**, **Direct connect gateway**, **CVM**, and others.
- **Next hop**: specifies the next hop instance (represented by using the next-hop ID), such as a NAT gateway in a VPC.

### Routing policy priority
When there are multiple routing policies in a route table, the following routing priority applies, from high to low:
- Traffic within VPC: traffic within VPC is matched first.
- Most precise routing (longest prefix match): when there are multiple entries in the route table that can match the destination IP, the route with the longest (most precise) mask is used as the match to confirm the next hop.
- Public IP: if matching fails for all routing policies, the Internet can be accessed through the public IP.

### Explanation of NAT Gateway/EIP priorities
When a subnet is associated with a NAT gateway, and the CVM in the subnet has a public IP (or EIP), it will access the Internet through the NAT gateway by default (because the priority of the most precise route is higher than that of the public IP). However, you can set a routing policy to enable access to the Internet by using the public IP of the CVM. For details, see [Adjusting the Priorities of NAT Gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).
