1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Networking** > **Virtual Private Cloud** to access the Virtual Private Cloud (VPC) console.
2. In the left sidebar, click **Peering Connections** to go to the management page.
3. Select a region and a VPC above the list and click **New**.
4. Enter a name and select the peer region, account type, and VPC.
 - If the peer account type is **My Account**, select the account from the drop-down list.
 - If the peer account type is **Other Accounts**, enter the account ID and VPC ID of the peer account.
 ![](https://main.qcloudimg.com/raw/a5e601765747a100a60e7845bf2553b8.png)
5. Select the bandwidth cap.
 - For an intra-region peering connection, there is no bandwidth cap. Therefore, this **cannot be modified**.
 - For a cross-region peering connection, the bandwidth cap can be selected. If you need higher cross-region bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
6. Click **Create**. A peering connection between two VPCs under the same account takes effect immediately after its creation.
>**Note:**
>The cost of a cross-region peering connection is paid by the requester of the connection.
