To implement the communication between a CCN and the direct connect gateway, you need to configure a routing policy for the CCN, in which configure the direct connect gateway as the next hop and IDC IP range as the destination. The routing policy can be either manually entered (Static) or automatically synced (BGP). For more information, see [Route Overview](https://intl.cloud.tencent.com/document/product/1003/34259). This document describes how to configure IDC IP range on the direct connect gateway.

## Background
As shown in the following Direct Connect network architecture, your IDC associated with the CCN-based direct connect gateway and CCN can communicate with a Tencent Cloud VPC. The destination IP range of VPC routes to IDC is `192.168.0.0/24`. After configuring the IDC IP range on the direct connect gateway, the CCN route table will add a routing policy with the direct connect gateway as the next hop and `192.168.0.0/24` as the destination.
>?If you configure multiple IDC IP ranges, CCN will forward the route with the longest mask. For more information, see [Route Overview](https://intl.cloud.tencent.com/document/product/1003/34259).
>
![](https://main.qcloudimg.com/raw/6df64ad17e1489d57d65657d9741a696.png)

## Prerequisites
- You have created a CCN-based direct connect gateway as instructed in [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).

## Directions
1. Log in to the [Direct Connect Gateway console](https://console.cloud.tencent.com/vpc/dcgw?rid=1).
2. Select a region and VPC at the top of the **Direct Connect Gateway** page. Click the **ID/Name** of the target direct connect gateway to enter its details page.
3. Select the **IDC IP Range** tab.
An IDC IP range specifies the direct connect gateway route to CCN. After the route is received, CCN will automatically add a route with the direct connect gateway as the next hop and IDC IP range as the destination.
4. Configure IDC IP ranges as needed.
 - Manually enter (Static)
    1. Click **Add**on the **IDC IP Range** tab.
    2. Enter the IDC IP range (such as `192.168.0.0/24`) and click **Save**. You can click **Add** to enter another IDC IP range and repeat this step.
 - Dynamically sync (BGP)
  >?The BGP route is currently in beta. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
  >
    1. Select the **BGP Route** tab. This mode enables the direct connect gateway to automatically obtain and send the IDC IP range to CCN. It takes one minute to update the data. To obtain the real-time IDC IP range, you can manually refresh the page.
    2. Click the edit icon on the right of the **Static Route**, select **BGP Route** for the mode in the pop-up dialog box, and click **OK**.  



