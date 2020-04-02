A route table consists of multiple routing policies and is used for controlling outbound traffic routes of subnets in the VPC. Each subnet can be associated with only one route table, while each route table can be associated with multiple subnets. You can create multiple route tables for subnets with different traffic routes.

## Types
There are two types of route tables: default route tables and custom route tables:
- When you create a VPC, the system will automatically generate a default route table for it. A subnet created later is automatically associated with the default route table if no custom route table is selected. You cannot delete the default route table, but you can add, delete, and modify routing policies in this route table.
- You can create a custom route table in VPC, and custom route tables can be deleted. You can create a custom route table for subnets with the same routing policy and associate the route table with all subnets that need to follow this routing policy.
  
When [creating a subnet](https://intl.cloud.tencent.com/document/product/215/31806#.E5.88.9B.E5.BB.BA.E5.AD.90.E7.BD.91), you can associate it with a route table. After the subnet is created, you can also [change the route table associated with the subnet](https://intl.cloud.tencent.com/document/product/215/31806#.E6.9B.B4.E6.8D.A2.E5.AD.90.E7.BD.91.E5.85.B3.E8.81.94.E7.9A.84.E8.B7.AF.E7.94.B1.E8.A1.A8).

## Routing Policies
A route table controls traffic routes by using routing policies. A routing policy consists of the destination, next-hop type, and next hop:
- **Destination**: the target IP range to which you want to forward traffic. Destination IP range description supports only the IP range format. If you want the destination to be a single IP address, you can set the mask to ‘32’ (such as `172.16.1.1/32`). The destination cannot be an IP range of the route table in the VPC, because local routing already implements private network intercommunication in this VPC by default.
- **Next-hop type**: the egress for data packets of the VPC. The VPC supports the following next-hop types: **NAT gateway**, **Peering connection**, **VPN gateway**, **Direct connect gateway**, and **CVM**.
- **Next hop**: specifies the next-hop instance to which you redirect (by using the next-hop ID), such as a NAT gateway in your VPC.

### Routing policy priorities
When multiple routing policies are defined in a route table, the following routing priorities apply, from high to low:
- Traffic within the VPC: traffic within the VPC is matched first.
- Most precise routing (longest prefix matching): when multiple entries in the route table match the destination IP address, the route with the longest (most precise) mask is used as the hit item to determine the next hop.
- Public IP: if no routing policy is hit, the Internet can be accessed through the public IP address.

### Priorities of the NAT gateway and EIP
When a subnet is associated with a NAT gateway, and the CVM in the subnet has a public IP address (or EIP), it will access the Internet through the NAT gateway by default, because the priority of the most precise route is higher than that of the public IP address. However, you can also set a routing policy to enable access to the Internet by using the public IP address of the CVM. For details, see [Adjusting the Priorities of NAT Gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/30012).
