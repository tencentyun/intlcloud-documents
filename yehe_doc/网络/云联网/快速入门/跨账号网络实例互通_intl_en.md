This article describes how to associate VPCs under another account with your CCN instance.

## Prerequisites
- The VPCs you want to associate with have been created.
- The IP ranges of the VPCs and IDCs do not overlap.

## Step 1: Create a CCN Instance in Account A
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1) with account A.
2. Click **Cloud Connect Network** on the left sidebar to enter the CCN management page.
3. Click **+New**. The **New CCN instance** page appears. 
4. Enter a name for the CCN instance and a description. Select billing mode, service quality, bandwidth limit, and the ID of the VPC you want to associate with. Click **Add** if you want to associate with multiple VPCs.
> You can associate more instances after the CCN is created.
>
5. Click **OK**.

## Step 2: Use Account B to Apply for the VPC Association.
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1) with account B.
2. In the VPC list, click the ID of the desired VPC.
3. In the details page, click **Associate Now**. The **Associate with CCN** page appears.
4. Select **Other Account** and enter the ID of account A and the CCN instance ID.
![](https://main.qcloudimg.com/raw/9a05b970aeb3b22997f56c25b7014b9d.png)
5. Click **OK** to send the association request to the account A.

## Step 3: Accept the Association Request in Account A
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1) with account A.
2. Click **Cloud Connect Network** in the left sidebar. Then, click the ID of the desired CCN instance. 
3. On the **Associate with Instance** tab, find the information about the VPC to be approved, and click **Accept** to add the VPC to the CCN. 
![](https://main.qcloudimg.com/raw/075e5fd56abae0e8debe0291e67be60b.png)

## Step 4: Checking the Route Table
IP range conflicts produce invalid routes. To check if such conflicts exist, use the following steps:
1. In the CCN list, click the ID of the desired CCN instance.
2. Click **Route Tables** to view the route table of this CCN instance.
3. Check if there is any invalid routing policy.
![](https://main.qcloudimg.com/raw/e45af94ef787df2f74c6c96366499c5f.png)
4. For more information on routing conflicts, refer to [Route Restrictions](https://intl.cloud.tencent.com/document/product/1003/30052). If you want to enable a route that may lead to routing conflicts, refer to [Enabling a Route](https://intl.cloud.tencent.com/document/product/1003/30069).

## Step 5: Setting Cross-region Bandwidth Cap (Optional)
1. In the CCN list, click the ID of the desired CCN ID.
2. Click **Bandwidth Management**. Click **Change** to change the speed limit mode.
> The default bandwidth cap is 1 Gbps. If you want to increase the bandwidth, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
 - Inter-region bandwidth limit
Click **Change Bandwidth** to go to the **Change Bandwidth** page. Select **Region A** and **Region B** and enter the **Bandwidth Cap**. If you need to add more entries, click **Add**. Click **OK** to finish.

 - Region outbound bandwidth limit
Click **Adjust bandwidth speed limit**. In the page that appears, select desired regions in the **Add region outbound speed limit** list on the left. Enter corresponding speed limits on the right. Click **OK** to finish.

> Communication between CCN instances may incur fees. For pricing details, refer to [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).

