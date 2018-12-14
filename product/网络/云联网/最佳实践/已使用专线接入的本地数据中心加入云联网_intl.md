 
By instantly enabling and disabling routing policies, CCN makes it possible to smoothly migrate to CCN a local IDC that is connected to a VPC through Direct Connect.
**Scenario description:**
Your local IDC is connected to a VPC in the cloud through Direct Connect. Now you need to join the two to CCN to achieve the connection of multiple VPCs using one single Direct Connect tunnel.

![](
https://main.qcloudimg.com/raw/e5aaa24de41749ee2c7dd20d5d037512.png)

You need to complete the following steps:
1. Create a CCN instance (if there is already one, skip this step). For details, see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
2. Create a CCN-type Direct Connect gateway. For details, see [Creating a Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).
3. Add your IDC IP address range to the newly created Direct Connect gateway. For details, see [Adding an IDC IP Address Range](https://intl.cloud.tencent.com/document/product/1003/30075).
4. Create a dedicated tunnel on the original physical Direct Connect line using the new VLAN to connect the CCN and the Direct Connect gateway (created in step 2). For details, see the [Dedicated Tunnel Guide](/document/product/216/19261).
5. Join the VPC and the new Direct Connect gateway to the CCN. For details, see [Associating a Network Instance](https://intl.cloud.tencent.com/document/product/1003/30064). After successful joining, your two dedicated tunnels will receive the route from the same VPC at the same time. As the VPC routing table has not been changed, the VPC still transmits traffic to the IDC through the original dedicated tunnel.
6. In the corresponding routing table of the VPC, disable the routing policy from the VPC to the original dedicated gateway. For details, see [Disabling a Route](https://intl.cloud.tencent.com/document/product/1003/30068). And then enable in your IDC the newly created dedicated tunnel route to the CCN. In this process, the traffic from the VPC to the IDC will be interrupted, and the interruption duration depends on the time used by the disabling and enabling operations.
7. On your IDC device, verify that the IDC router has received all routes from the CCN and then switch the route from the IDC to the cloud to the new dedicated tunnel.
8. At this point, both the inbound and outbound traffic has been switched to the CCN, and you can delete the original dedicated tunnel.

>**Note:**
After the Direct Connect gateway and the VPC are joined to the CCN, if no route conflict is present, the route is automatically distributed and valid by default.
