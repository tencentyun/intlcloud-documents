This document describes how to associate VPCs under another account with your CCN instance.

## Prerequisites
- The VPCs you want to associate with have been created.
- The IP ranges of the VPCs and IDCs do not overlap.

## Step 1. Create a CCN Instance under Account A
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) with account A and click **+ New** on the CCN instance management page. 
2. Enter a name for the CCN instance and a description. Select billing mode, service quality, bandwidth limit, and the ID of the VPC you want to associate with. Click **Add** if you want to associate with multiple VPCs.
>?You can associate instances when or after creating the CCN.
>
![](https://main.qcloudimg.com/raw/b72cc7c286f94d8b958def554dfc0150.png)
3. Click **OK**.

## Step 2. Use Account B to Apply for Associating VPC with CCN
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) with account B and click the ID of the VPC to be associated with the CCN instance in the VPC list to enter the details page.
2. Click **Associate Now**.
![](https://main.qcloudimg.com/raw/3d034f69e2bb198c0604f698a8c5e614.png)
3. In the pop-up window, select **Other accounts** and enter the ID of account A and the CCN instance ID.
![](https://main.qcloudimg.com/raw/461d6ca46bb20c141dc538348b542f1a.png)
4. Click **OK** to send the association request to account A.

## Step 3. Use Account A to Accept the Association Request
1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) with account A.
2. Click the **ID/Name** of the CCN instance with a pending association request. 
3. On the **Associated Instances** page, locate the VPC to be associated, and click **Agree** to add the VPC to the CCN instance. 
![](https://main.qcloudimg.com/raw/a6371867413e26ec0274c12386b4c6ff.png)

## Step 4. Check the Route Table
IP range conflicts produce invalid routes. To check if such conflicts exist, perform the following steps:
1. In the CCN list, click the **ID/Name** of the desired CCN instance.
2. Click the **Route Table** tab to view the route table of this CCN instance.
3. Check if there is any invalid routing policy.
![](https://main.qcloudimg.com/raw/6e8f71bbd8addfa7df60ed6061df9b38.png)
4. See [Route Limits](https://intl.cloud.tencent.com/document/product/1003/30052) to learn more about route conflicts. If you want to enable a route, please see [Enabling a Route](https://intl.cloud.tencent.com/document/product/1003/30069).

## Step 5. Set Cross-region Bandwidth Cap (Optional)
1. In the CCN list, click the **ID/Name** of the CCN instance for which to set the bandwidth.
2. Select the **Bandwidth Management** tab on the details page of the CCN instance.
3. (Optional) Click **Change** to select the bandwidth limit mode as needed.
![](https://main.qcloudimg.com/raw/bc93b28f5c0fb5fee6ce51e1b73dab1c.png)
![](https://main.qcloudimg.com/raw/f7d06cf1f591f25950d0b8a745fafa71.png)
4. Configure the bandwidth cap depending on the bandwidth limit mode of the CCN instance:
>?The default bandwidth cap is 1 Gbps. If you require a higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
 - Inter-region bandwidth limit
Click **Change Bandwidth**. In the pop-up window, select **Region A** and **Region B** from the drop-down list and enter the **Bandwidth Cap**. You can also click **Add** to configure multiple bandwidth limit rules, and then click **OK**.
![](https://main.qcloudimg.com/raw/5424741fb17864f3f98da59ba047d9f5.png)
 - Region outbound bandwidth limit
Click **Adjust bandwidth cap**. In the pop-up window, select regions for which you want to limit the bandwidth on the left and set the bandwidth cap on the right. Click **OK**.
![](https://main.qcloudimg.com/raw/aef1779f4c11d8f0fe716c287cb60b90.png)
>?Communication between CCN instances may incur fees. For pricing details, refer to [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).



