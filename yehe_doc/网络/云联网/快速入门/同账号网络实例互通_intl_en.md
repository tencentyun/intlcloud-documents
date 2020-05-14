This article describes how to use CCN to interconnect VPCs and IDCs under the same account.

## Prerequisites
- You have created at least one VPC.
- The IP ranges of the VPCs and IDCs do not overlap.

## Step 1: Creating a CCN Instance
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Cloud Connect Network** on the left sidebar to enter the CCN management page.
3. Click **+New**. The **New CCN instance** page appears. 
4. Enter a name for the CCN instance and a description. Select billing mode, service quality, bandwidth limit, and the ID of the VPC you want to associate with. Click **Add** if you want to associate with multiple VPCs.
> You can associate more instances after the CCN is created.
>
5. Click **OK**.

## Step 2: Associating a Network Instance
1. In the CCN list, click the ID of the desired CCN to enter the details page.
2. Click **Add an instance** under **Associate with Instance**. The **Associate with Instance** page appears. 
3. Select the network instance type and region, as well as a specific instance.
> If you need to associate more network instances, click **Add**.
4. Click **OK** to add the selected network instance to CCN.

## Step 3: Checking the Route Table
IP range conflicts produce invalid routes. To check if such conflicts exist, use the following steps:
1. In the CCN list, click the ID of the desired CCN instance.
2. Click **Route Tables** to view the route table of this CCN instance.
3. Check if there is any invalid routing policy.
![](https://main.qcloudimg.com/raw/e802fd5a736644e0a6dc2757400adbf1.png)
4. For more information on routing conflicts, refer to [Route Restrictions](https://intl.cloud.tencent.com/document/product/1003/30052). If you want to enable a route that may lead to routing conflicts, refer to [Enabling a Route](https://intl.cloud.tencent.com/document/product/1003/30069).

## Step 4: Setting Cross-region Bandwidth Cap (Optional)
1. In the CCN list, click the ID of the desired CCN ID.
2. Click **Bandwidth Management**. Click **Change** to change the speed limit mode.
> The default bandwidth cap is 1 Gbps. If you want to increase the bandwidth, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
 - Inter-region bandwidth limit
Click **Change Bandwidth** to go to the **Change Bandwidth** page. Select **Region A** and **Region B** and enter the **Bandwidth Cap**. If you need to add more entries, click **Add**. Click **OK** to finish.
 - Region outbound bandwidth limit
Click **Adjust bandwidth speed limit**. In the page that appears, select desired regions in the **Add region outbound speed limit** list on the left. Enter corresponding speed limits on the right. Click **OK** to finish.

> Communication between CCN instances may incur fees. For pricing details, refer to [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).
