By instantly enabling and disabling routing policies, CCN makes it possible to smoothly migrate a peering connection-enabled VPC to CCN.
Scenario description:
VPC1 and VPC2 are interconnected through a peering connection and now need to be joined to CCN to achieve full-mesh interconnection with other VPCs.
IP address range 1: VPC1 in Guangzhou: 192.168.0.0/16, subnet A: 192.168.0.0/24, subnet B: 192.168.1.0/24.
IP address range 2: VPC2 in Shanghai: 10.0.0.0/16, subnet C: 10.0.0.0/24, subnet D: 10.0.1.0/24.
![Image description](https://main.qcloudimg.com/raw/243d6a566eab7e1ea23cb8519cc9085f.png)
You need to complete the following steps:
1. Create a CCN instance (if there is already one, skip this step). For more information, see [Creating a CCN Instance](/document/product/877/18752).
2. Associate VPC1 and VPC2 with the corresponding CCN instance. For more information, see [Associating a Network Instance](/document/product/877/18747).
3. In the routing table of the CCN instance, you can see the routing policy with the subnets in VPC1 and VPC2 as the destination.
![Image description](https://main.qcloudimg.com/raw/39de66b68b8a761ec0f8b888116e0df1.png)
4. Enter the routing table of the subnets in VPC1 to check the routing conditions.
5. Enter the routing table of the subnets in VPC2 to check the routing conditions.
Case 1: If the route automatically distributed by CCN has no conflict with the existing peering connection, it is valid by default and you do not need to do anything.
![Image description](
https://main.qcloudimg.com/raw/f25bfe0d73627404a6b081203baf4bc1.png)
Case 2: If the route automatically distributed by CCN has an overlapping conflict with the existing peering connection, you need to first **disable** the routing policy whose next hop is the peering connection and then **enable** the routing policy whose next hop is the CCN.
![Image description](https://main.qcloudimg.com/raw/de6869e6e4c07181574a0d88bbfdd685.png)
Case 3: If the route automatically distributed by CCN has an inclusive conflict with the existing peering connection, you can **enable** the routing policy whose next hop is the CCN and then set forwarding based on the longest mask match principle. It is recommended that you [disable] the routing policy whose next hop is the peering connection to avoid duplicate billing.
![Image description](https://main.qcloudimg.com/raw/5cfd481eed906ccf1e2aa7ca2cc16e11.png)







