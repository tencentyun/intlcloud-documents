1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and select **Products** -> **Cloud Compute & Network** -> **Virtual Private Cloud** to go to the VPC console.
2. In the left pane, click **Peering Connections** to go to the management page.
3. Select the region and VPC above the list, and click **New**.
 ![](https://main.qcloudimg.com/raw/57786db314c63e45265a9656d6ef4671.png)
4. Enter a name, select the accepter region, account type and VPC.
 - If the accepter account type is **My Account**, choose from the drop-down list.
 - If the accepter account type is **Other accounts**, enter the account ID and VPC ID of the accepter account.
 ![](https://main.qcloudimg.com/raw/a5e601765747a100a60e7845bf2553b8.png)
5. Select the bandwidth cap
 - For an intra-region peering connection, there is no restriction on the bandwidth, so this **cannot be modified**.
 - For a cross-region peering connection, you can select a bandwidth cap. If you need a higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
6. Click **Create**. A peering connection between the VPCs under the same account takes effect immediately after its creation.
>**Note:**
> The fee for a cross-region peering connection is paid by the requester of such connection.

