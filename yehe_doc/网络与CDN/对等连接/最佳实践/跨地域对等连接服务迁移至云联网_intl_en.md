## Overview
Both CCN and Peering Connection can realize cross-region VPC interconnection. Compared with Peering Connection, CCN features linkage interconnection, self-learning of routes, simple configuration, stability and reliability, and lower cost and latency.
This document guides you through plans to migrate the cross-region connection from Peering Connection to CCN.

## Scenarios
+ **Scenario 1**: Nanjing VPC1 and VPC2 are connected through a peering connection.
**Migration plan**: Associate the two VPCs with CCN to realize the cross-region VPC interconnection.
 + Before migration:
![](https://qcloudimg.tencent-cloud.cn/raw/611e69a61efcf4a901109b8d23a441d1.png)
 + After migration:
![](https://qcloudimg.tencent-cloud.cn/raw/e74c2ad1a76e0bf6205e4538e266d6a7.png)
+ **Scenario 2**: Multiple VPCs across regions need to be fully interconnected. Since the connectivity of peering connections cannot be transferred, you need to create one peering connection between every two VPCs.
 **Migration plan**: Add multiple VPCs to a CCN instance to realize the public and private network interconnection.
 + Before migration:
![](https://qcloudimg.tencent-cloud.cn/raw/ad9b5f6140c8f0db6820eecc46be0bad.png)
 + After migration:
![](https://qcloudimg.tencent-cloud.cn/raw/1c85740f9e423952797b3f3978a7d39d.png)
+ **Scenario 3**: VPC1 is connected to VPC2 and VPC3 respectively through peering connections, but VPC2 and VPC3 are not interconnected.
  **Migration plan**: Use CCN to connect VPC1 with VPC2 and VPC3. For the non-interconnection between VPC2 and VPC3, associate their subnets with the network ACLs to realize access control, that is, allow the IP range used for communication only in the ACL.
	Before migration:
	![](https://qcloudimg.tencent-cloud.cn/raw/6b8a072fb99dba9f432cf9cff91e3564.png)
	After migration:
	![](https://qcloudimg.tencent-cloud.cn/raw/9303ef9f65fd712024287eb18bd67265.png)
+ **Scenario 4**: VPC1 is connected to VPC2 and VPC3 via peering connections. VPC2 and VPC3 are not interconnected. The VPC1 subnet 11 is connected to the VPC2 subnet 21 and the VPC3 subnet 31. The VPC1 subnet 13 is connected to the VPC2 subnet 23 and the VPC3 subnet 33.
>?Access control between subnets is implemented through their own network ACLs. For example, for the network ACL21 of the VPC2 subnet 21, only the IP range of subnet 11 within VPC1 is allowed for communication, so as to realize the traffic access control between subnets.
>
**Migration plan**: Use CCN to fully connect VPC1, VPC2, and VPC3. Confirm the ACL rules of each subnet in advance to ensure that only the required subnet IP ranges are allowed.
	 Before migration:
	 ![]()
	 After migration:
	 ![](https://qcloudimg.tencent-cloud.cn/raw/b79d263535fa728032f342a083f88e51.png)

## Directions
>?
>+ The directions are given based on scenario 1.
>+ In scenario 2, multiple VPCs are fully interconnected. Please add these VPCs to CCN one by one, and check the routing conditions in CCN and VPCs in time. When a route conflict occurs due to overlapping IP ranges, the route becomes invalid. For solutions, see [Use Limits](https://intl.cloud.tencent.com/document/product/1003/30052) and [Migrating VPCs with Peering Connection to CCN](https://intl.cloud.tencent.com/document/product/1003/30078).
>+ In scenario 3 and scenario 4, please configure an appropriate ACL policy as instructed in [Managing Network ACLs](https://intl.cloud.tencent.com/document/product/215/31852) for the subnet in advance according to the communication between the subnets. Then associate the VPCs with CCN one by one, and migrate the routes to CCN. During the period, you can monitor the business situation in real time.
>
1. [Create a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062) and associate the VPC1 to it.
 ![]()
2. Click the CCN instance ID and enter the route table tab. You can see the routing policy whose destination is the VPC1 subnet. To add a CCN route, see [Route Overview](https://intl.cloud.tencent.com/document/product/1003/34259).
![]()
3. Associate VPC2 with the CCN instance as instructed in [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
4. Click the CCN instance ID again and re-enter the route table tab. You can see a new routing policy whose destination is the VPC2 subnet. For solutions of CCN routing exceptions, see [Use Limits](https://intl.cloud.tencent.com/document/product/1003/30052).
 ![]()
5. Check the route tables associated with the subnets of VPC1 and VPC2 respectively. You can see both VPC1 and VPC2 subnets have added a routing policy with the next hop to CCN. But due to the routing conflict, when the destination IP range overlaps, the routing policy added later is invalid, so the communication between VPC1 and VPC2 is still implemented through the peering connection.
VPC1 subnet route tables:
 ![]()
VPC2 subnet route tables:
![]()
6. <span id="step6">In the VPC1 route tables, enable VPC1 - VPC2 routing policy directed to a CCN instance, and disable the VPC1 - VPC2 routing policy directed to a peering connection instance, as instructed in [Managing Routing Policies](https://intl.cloud.tencent.com/document/product/215/40080). At this time, VPC1 communicates with VPC2 via a CCN connection, while VPC2 communicates with VPC1 via a peering connection.
	![]()
7. Check the monitoring information as instructed in [View Monitoring Information](https://intl.cloud.tencent.com/document/product/1003/30071) or [Viewing Monitoring Data of Network Traffic Over a Cross-region Peering Connection](https://intl.cloud.tencent.com/document/product/553/18842) or log in to a CVM instance as instructed in [Logging In to Linux Instance (Web Shell)](https://intl.cloud.tencent.com/document/product/213/5436). `Ping` the network to check whether the traffic is normal. If it is not normal, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
    ![](https://qcloudimg.tencent-cloud.cn/raw/0b107fad18337e7359249f53939ad706.png)
8. In the VPC2 route tables, please refer to <a href ="#step6">step 6</a> to enable the VPC2 - VPC1 routing policy directed to a CCN instance, and disable the VPC2 - VPC1 routing policy directed to a peering connection instance.
9. Check the monitoring information or check whether the traffic is normal by a `ping` test.
    + If the traffic is abnormal, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
    + If the business traffic is normal within a week, and monitoring reveals that the peering connections have no traffic, you can refer to [Managing Routing Policies](https://intl.cloud.tencent.com/document/product/215/40080) and [Deleting a Peering Connection](https://intl.cloud.tencent.com/document/product/553/18848) to delete the routing policies directed to peering connection in the VPC1 and VPC2 route tables and the peering connection instances that you no longer use.
    
