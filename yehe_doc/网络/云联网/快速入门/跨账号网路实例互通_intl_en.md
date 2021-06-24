This document describes how to associate VPCs under another account with your CCN instance.

## Prerequisites

- The VPCs you want to associate with have been created.
- The IP ranges of the VPCs and IDCs do not overlap.

## Step 1. Create a CCN Instance under Account A

1. Log in to the [Virtual Private Cloud console](https://console.cloud.tencent.com/vpc/vpc?rid=1) with account A.
2. Click **Cloud Connect Network** on the left sidebar to enter the CCN management page.
3. Click **+New**. 
4. In the pop-up window, enter a name for the CCN instance and a description. Select billing mode, service level, bandwidth limit mode, and the ID of the VPC you want to associate with.![](https://main.qcloudimg.com/raw/7248ed21b3c3aeefd0376d888914bdf3.png)

>?You can associate instances when or after creating the CCN.
>

5. Click **OK**.

## Step 2. Use Account B to Apply for Associating VPC with CCN

1. Log in to the [Virtual Private Cloud console](https://console.cloud.tencent.com/vpc/vpc?rid=1) with account B.
2. In the VPC list, click the **ID/Name** of the VPC to associate with CCN.
3. In the **Associate with CCN** section on the **Basic Information** page, click **Associate Now**.
   ![](https://main.qcloudimg.com/raw/a316cdd6c8d32b654037894099a7e75d.png)
4. In the pop-up window, select **Other accounts** and enter the ID of account A and the CCN instance ID.
   ![](https://main.qcloudimg.com/raw/29bbc4c616fd2b6c64b463a6c9a8ec8d.png)
5. Click **OK** to send the association request to the account A.

## Step 3. Use Account A to Accept the Association Request

1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1) with account A.
2. Click **Cloud Connect Network** on the left sidebar. Then, click the **ID/Name** of the CCN instance with a pending association request. 
3. On the **Associated Instances** page, locate the VPC to be associated, and click **Agree** to add the VPC to the CCN instance. 
   ![](https://main.qcloudimg.com/raw/f57c15e2e1ca2e3220f1839ce5e024b2.png)

## Step 4. Check the Route Table

IP range conflicts produce invalid routes. To check if such conflicts exist, perform the following steps:

1. In the CCN list, click the **ID/Name** of the desired CCN instance.
2. Click the **Route Table** tab to view the route table of this CCN instance.
3. Check if there is any invalid routing policy.
   ![](https://main.qcloudimg.com/raw/3d9c915eb46b2bed59947105e611661c.png)
4. See [Route Limits](https://intl.cloud.tencent.com/document/product/1003/30052) to learn more about route conflicts. If you want to enable a route, see [Enabling a Route](https://intl.cloud.tencent.com/document/product/1003/30069).

## Step 5. Set Cross-region Bandwidth Cap (Optional)

1. In the CCN list, click the **ID/Name** of the CCN instance for which to set the bandwidth.
2. Select the **Bandwidth Management* tab on the details page of the CCN instance.
3. (Optional) Click **Change** to select the bandwidth limit mode as needed.
   ![](https://main.qcloudimg.com/raw/9a59e3cfc7bcf92ae6df7b507e8a45d5.png)
   ![](https://main.qcloudimg.com/raw/a7c3ba4bb40af1164df589095731f1a7.png)
4. Configure the bandwidth cap depending on the bandwidth limit mode of the CCN instance:

>?The default bandwidth cap is 1 Gbps. If you require a higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

 - Inter-region bandwidth limit
   Click **Change Bandwidth**. In the pop-up window, select **Region A** and **Region B** from the drop-down list and enter the **Bandwidth Cap**. You can also click **Add** to configure multiple bandwidth limit rules, and then click **OK**.
   ![](https://main.qcloudimg.com/raw/952c27b2590d37f6f14785b12a5d4c2b.png)
 - Region outbound bandwidth limit
   Click **Adjust bandwidth cap**. In the pop-up window, select regions for which you want to limit the bandwidth on the left and set the bandwidth cap on the right. Click **OK**.
   ![](https://main.qcloudimg.com/raw/a961f2724eda0a156304dea7169ae319.png)

>?Communication between CCN instances may incur fees. For pricing details, refer to [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).



