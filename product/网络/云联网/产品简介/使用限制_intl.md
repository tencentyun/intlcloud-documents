CCN is currently in internal trial. You need to submit a [ticket](https://console.cloud.tencent.com/workorder) first. After your application is approved, you can start using it.

### Resource Limitations

The CCN resource limitations are as shown below. You can also view [usage restrictions of VPC and other products](https://intl.cloud.tencent.com/document/product/215/537).

- At most 5 CCN instances can be created for each account
- At most 25 network instances can be associated with each CCN instance
- Unlimited number of routing entries can be created for each CCN instance

### Non-transferable Interconnection

The presence of a peering connection does not affect the interconnection realized after a VPC is joined to CCN. CCN only distributes routes to the network instances associated with it for interconnection.
For example, as shown in the figure below, a peering connection has been established between VPC1 and VPC2. After VPC1 is joined to a CCN instance, only VPC1 can interconnect with network instances VPC3 and IDC in CCN; while VPC2 can only interconnect with VPC1 through the peering connection but not other instances in CCN.
![Image description](https://main.qcloudimg.com/raw/76e9c5f7fe001b444dd3f69dfc8e5e71.png)

### Routing Restrictions

#### CIDR Restrictions for VPC

- CCN sets the following CIDR restrictions for VPC at the subnet level: If two VPCs have the same CIDR but their subnets have different CIDRs, they can be joined to CCN for interconnection.
  For example, if the CIDR of VPC1 is 192.168.0.0/16, which contains 2 subnets: subnet 1 (192.168.1.0/24) and subnet 2 (192.168.2.0/24),
  and the CIDR of VPC2 is 192.168.0.0/16, which contains 2 subnets: subnet 3 (192.168.3.0/24) and subnet 4 (192.168.4.0/24), then although the CIDRs of VPC1 and VPC2 overlap, the subnet CIDRs do not overlap, so they can both be joined to the same CCN instance, and the routes can be automatically distributed for interconnection.

#### Rules for CIDR Overlapping Conflict

- If the CIDRs of network instances have an overlapping conflict, the routing entry of the first network instance associated with the CCN instance is valid, while that of the second network instance associated is invalid.
  For example, if VPC1 is associated with CCN instance A and the CIDR of its subnet A is 10.0.3.0/24, which does not overlap with the CIDR of other network instances in the CCN instance, then the routing policy is valid, and other network instances in the CCN instance can interconnect with subnet A of VPC1.
  At this point, if VPC2 is associated with CCN instance A and the CIDR of its subnet B is 10.0.3.0/24, then the routing policy is invalid, and subnet B of VPC2 cannot interconnect with other network instances in the CCN instance.
  You can first disable the routing policy to CCN in the routing table of subnet A and then enable the routing policy to CCN in the routing table of subnet B to allow subnet B to interconnect with other network instances in the CCN instance.
- If a routing conflict is caused by an operation (such as creating a subnet) after the network instance is joined to CCN, the route is invalid and the existing valid route remains valid.
  For example, if VPC1 is associated with CCN instance A and the CIDR of its subnet A is 10.0.1.0/24, and VPC2 is also associated with CCN instance A and the CIDR of its subnet B is 10.0.2.0/24, then the CIDRs do not conflict and are both valid. At this point, if a subnet C with CIDR of 10.0.2.0/24 is created in VPC1, which conflicts with subnet B of VPC2, then the route from subnet C to CCN is invalid, but the existing routes from subnet A and subnet B to CCN remain valid.

#### Rules for CIDR Inclusive Conflict

- If the CIDRs of network instances have an inclusive conflict, the routing entry corresponding to the first network instance associated with the CCN instance is valid, while that to the second network instance associated is invalid. However, you can enable this route in the routing table, which, after enabled, will forward the data based on the longest mask match rule.
  For example, if VPC1 is associated with CCN instance A and the CIDR of its subnet A is 10.0.1.0/20, which does not overlap with the CIDR of other network instances in the CCN instance, then the routing policy is valid, and other network instances in the CCN instance can interconnect with subnet A of VPC1.
  At this point, if VPC2 is associated with CCN instance A and the CIDR of its subnet B is 10.0.1.0/24 (included in the CIDR of subnet A of VPC1), then the routing policy is invalid by default, and subnet B of VPC2 cannot interconnect with other network instances in the CCN instance for the time being.
  You can enable this route in the routing table of subnet B, which, after enabled, will forward the data based on the longest mask match rule.
