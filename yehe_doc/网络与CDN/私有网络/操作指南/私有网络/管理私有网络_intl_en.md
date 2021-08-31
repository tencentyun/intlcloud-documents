 Virtual Private Clouds (VPCs) are the basis for using Tencent Cloud services. When purchasing an instance such as a CVM, you need to choose the VPC to which the instance belongs. This document describes the usage lifecycle of VPCs.

## Background


1. [Creating a VPC](#1): you need to carefully [plan your network](https://intl.cloud.tencent.com/document/product/215/31795) before creating a VPC. The CIDR blocks of VPCs and subnets cannot be modified after creation.
2. [Viewing a VPC](#2): you can view the basic information of a VPC, its CCN association, and the resources it contains.
3. (Optional) Choose the operations that apply to your use cases:
 - When the primary CIDR blocks are insufficient:
    - [Creating secondary CIDR blocks](#21): you can create secondary CIDR blocks to meet your actual network demands.
    - [Deleting secondary CIDR blocks](#32): you can delete secondary CIDR blocks if you don’t need them.
4. [Deleting a VPC](#3): after a VPC is deleted, its subnets and route tables are also deleted.

<span id ="1"></span>
## Creating a VPC

A VPC has at least one subnet, and Tencent Cloud service resources can only be added in a subnet.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select a region at the top of the **VPC** page, and click **+New**.
3. In the **Create VPC** dialog box, enter the VPC information and original subnet information, and then click **OK**.
>?The CIDR blocks of the VPC and subnet cannot be modified after creation.
>
 - The VPC CIDR block can be any of the following IP ranges. For VPCs to communicate with each other over the private network, their CIDR blocks should not overlap.
 - `10.0.0.0` - `10.255.255.255` (mask range between 16 and 28)
 - `172.16.0.0` - `172.31.255.255` (mask range between 16 and 28)
 - `192.168.0.0` - `192.168.255.255` (mask range between 16 and 28)
 - The subnet CIDR block must fall within or the same as the VPC CIDR block.
   For example, if the VPC IP range is `192.168.0.0/16`, then its subnet IP range can be `192.168.0.0/16`, `192.168.0.0/17`, etc. 
   ![](https://main.qcloudimg.com/raw/ed9901dce2ec94302ae14a1fca7d06b8.png)

<span id ="2"></span>
## Viewing a VPC
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page.
3. In the VPC list, click the **ID/Name** of the VPC to view its details.
 On the details page, you can view the basic information of the VPC, its CCN association, and the resources it contains.
![](https://main.qcloudimg.com/raw/779074772193dfa8394256a674f4c36f.png)

<span id ="21"></span>
## Creating Secondary CIDR Blocks
>?
>- The secondary CIDR block feature is currently in beta. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1).
>- The secondary CIDR block can overlap with the destination IP range of a custom route. However, you need to exercise caution with this, because the secondary CIDR block route is a local route and the priority of local routes is higher than that of custom subnet routes.
>- Classic network CVMs do not support interconnection with cloud resources in the secondary CIDR block.
>- Currently, only Cloud Connect Network (CCN) supports passing the secondary CIDR blocks. That is, CVMs in the secondary CIDR block cannot communicate with other VPCs or IDCs via peering connection or Direct Connect.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page.
3. In the VPC list, locate the VPC and select **More** > **Edit IPv4 CIDR Block** under its **Operation** column.
	![](https://main.qcloudimg.com/raw/2f70c86d42da11ba7fa502b3b58e9b74.png)
4. In the pop-up dialog box, click **Add** to enter a secondary CIDR block.
<img src="https://main.qcloudimg.com/raw/2dce76adc2f3b4428d68a9727f55966b.png" width="50%" />
5. Click **OK**.

<span id ="32"></span>
## Deleting Secondary CIDR Blocks
>?The secondary CIDR block feature is currently in beta. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9CVPC&step=1).
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page.
3. In the VPC list, locate the VPC to delete and select **More** > **Edit IPv4 CIDR Block** under its **Operation** column.
4. In the pop-up dialog box, click **Delete** next to the secondary CIDR block.
<img src="https://main.qcloudimg.com/raw/07867a0b1fbca9ad4350ca82d2c54200.png" width="50%" />
5. Click **OK**.

<span id ="3"></span>
## Deleting a VPC
To delete a VPC, there must be no occupation of the VPC’s IP addresses and no cloud resources in the VPC (such as CVMs, TencentDB instances, or gateways).
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top of the **VPC** page.
3. In the VPC list, locate the VPC to delete, click **Delete** under its **Operation** column, and confirm the deletion.
![](https://main.qcloudimg.com/raw/5aaffa07e85e3119c358ff7bc9af9eeb.png)
