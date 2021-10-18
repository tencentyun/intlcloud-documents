Each VPC can have one primary CIDR block, which cannot be modified after the VPC creation. When the IPs in the primary CIDR block can not meet your needs, you can create multiple secondary CIDR blocks to add IP ranges.
You can allocate the subnet with an IP range from the primary or secondary CIDR blocks. All subnets of the same VPC are interconnected by default, regardless of whether they belong to the primary or secondary CIDR blocks.

## Use Limits
+ Classic network-based CVMs cannot interconnect with cloud resources in the secondary CIDR block.
+ A peering connection does not support secondary CIDR blocks.
+ Cloud Connect Network, VPN gateway, and standard direct connect gateway supports secondary CIDR blocks. Note the following limits for a direct connect gateway:
  - This feature is unavailable in the Finance Cloud regions.
  - Up to 10 secondary CIDR blocks can be propagated.
  - This feature is unavailable to a NAT direct connect gateway.



## Creating Secondary CIDR Blocks[](id:21)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page.
3. In the VPC list, locate the VPC and select **More** > **Edit IPv4 CIDR block** under the **Operation** column.
4. In the pop-up dialog box, click **Add** to enter a secondary CIDR block.
>!A secondary CIDR block can overlap with the destination IP range of a custom route. Note that the secondary CIDR block uses a local route, which has a higher priority than that of custom subnet routes.
>
5. Click **OK**.

## Deleting Secondary CIDR Blocks[](id:32)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page.
3. In the VPC list, locate the VPC from which secondary CIDR blocks will be deleted, and select **More** > **Edit IPv4 CIDR block** under the **Operation** column.
4. In the pop-up dialog box, click **Delete** next to the secondary CIDR block.

5. Click **OK**.
