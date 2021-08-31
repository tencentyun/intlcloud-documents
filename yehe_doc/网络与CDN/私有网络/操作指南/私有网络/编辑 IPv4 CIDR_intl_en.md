Once created, the primary CIDR block of your VPC cannot be modified. When the primary CIDR block is insufficient, you can create secondary CIDR blocks to add IP ranges.

>?
>- The secondary CIDR block feature is currently in beta. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1).
>- A secondary CIDR block can overlap with the destination IP range of a custom route. Note that the secondary CIDR block uses a local route, which has a higher priority than that of custom subnet routes.
>- Classic network-based CVMs cannot interconnect with cloud resources in the secondary CIDR block.
>- Currently, only Cloud Connect Network (CCN) supports secondary CIDR blocks. That is, CVMs in the secondary CIDR blocks cannot communicate with other VPCs or IDCs via peering connection or Direct Connect.

<span id="21"></span>
## Creating Secondary CIDR Blocks
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page.
3. In the VPC list, locate the VPC and select **More** > **Edit IPv4 CIDR block** under the **Operation** column.

4. In the pop-up dialog box, click **Add** to enter a secondary CIDR block.

5. Click **OK**.

<span id="32"></span>
## Deleting Secondary CIDR Blocks
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page.
3. In the VPC list, locate the target VPC, and select **More** > **Edit IPv4 CIDR block** under the **Operation** column.
4. In the pop-up dialog box, click **Delete** next to the secondary CIDR block.

5. Click **OK**.
