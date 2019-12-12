
## Resource Limits
The following table lists the limits on the supported CCN resources. <!--For limits on other Virtual Private Cloud (VPC) products, see [Limitations]().-->
<table>
<tr>
<th>Resource</th>
<th>Limit</th>
</tr>
<tr>
<td>Number of CCN per account</td>
<td>5</td>
</tr>
<tr>
<td>Number of network instances that can be bound to a CCN instance</td>
<td>25</td>
</tr>
</table>

## Feature Limits
**Non-transferrable with a Peering Connection**

A peering connection does not affect the interconnection between a CCN and a VPC added to the CCN. To implement interconnection, the CCN delivers routes only to a network instance that is associated with this CCN.
For example, as shown in the following figure, a peering connection has been established between VPC 1 and VPC 2. After VPC 1 is added to the CCN, only VPC 1 can interconnect with network instances such as VPC 3 and the IDC in the CCN. VPC 2 can interconnect with VPC 1 only through the peering connection, but cannot interconnect with other instances in the CCN.
![Image description](https://main.qcloudimg.com/raw/f764269dbb106d6f6f47bd8470bb3aa5.png)

## Route Restrictions
To ensure that the interconnection between multiple network instances is smooth, CCN restricts the CIDR blocks of the network instances.

### Restrictions on VPC CIDR Blocks

CCN restricts CIDR blocks at the subnet level. It means that two subnets with identical CIDR blocks cannot interconnect with each other even if they are in the same VPC. And if the CIDR blocks of two VPCs overlap, as long as they have different CIDR blocks of subnets, you can add them to CCN to implement intercommunication between them. For the route validation rule, see the conflict rules for overlapped CIDR blocks below. 

### In case of overlapped CIDR blocks

1. If the CIDR blocks of network instances overlap, only the route of the network instance that is first associated with the CCN instance is valid.
2. For a network instance already in CCN, if route conflicts occur due to operations like creating subnets, the new route does not take effect, and the existing valid route remains valid.

### In case of CIDR block containment conflict

If the CIDR blocks of multiple network instances are in a containment relationship, only the route table of a network instance that is first associated with the CCN instance is valid. However, you can enable invalid routes in route tables, so that you can forward data according to the longest mask matching rule.

#### Example of a Containment Conflict
Assume that VPC 1 is first associated with CCN instance A, the CIDR block of subnet A of VPC 1 is 10.0.1.0/20, and VPC 1 can interconnect with other instances in CCN instance A. Then, VPC 2 is associated with CCN instance A, and the CIDR block of subnet B of VPC 2 is 10.0.1.0/24, which is contained in the CIDR block of subnet A. In this case, a CIDR block containment conflict occurs. As a result, the routing policy for subnet B is invalid by default, and VPC 2 cannot interconnect with other instances in CCN instance A.

However, you can enable this invalid route in the route table of subnet B, so that you can forward data according to the longest mask matching rule. If the destination IP address of the routing policy is 10.0.1.0/24, the data will be forwarded to subnet B of VPC 2 according to the rule.




