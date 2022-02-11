This tutorial describes how to quickly build up a Virtual Private Cloud (VPC) with IPv4 CIDR blocks.
## Overview
This document guides through whole process of setting up an IPv4-based VPC. 
![](https://qcloudimg.tencent-cloud.cn/raw/926843feffd998e8dbf151b63178b366.png)

## Prerequisites
Make sure you’ve [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/register) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629) if you need to purchase resources in the Chinese mainland.

## Directions
### Step 1: create a VPC and subnet
>? After creating a VPC and subnet, you cannot modify their CIDR blocks. Therefore, complete [network planning](https://intl.cloud.tencent.com/document/product/215/31795) in advance.
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select the region of the VPC at the top and click **+New**.
3. In the **Create VPC** pop-up window, configure the VPC and subnet information as instructed below.
![](https://qcloudimg.tencent-cloud.cn/raw/ba0387f51ed8112ab819d5cb9c5113b5.png)
 - **VPC information**
    - Name: the name of the VPC.
    - IPV4 CIDR Block: you can choose any one of the IP ranges **10.0**.0.0 - **10.255**.255.255, **172.16**.0.0 - **172.31**.255.255, and 
    **192.168**.0.0 - **192.168**.255.255 as the VPC IP range. The mask range must be 16 to 28, such as `10.0.0.0/16`.
     - Advanced Options: you can optionally add tags to help you better manage resource permissions of sub-users and collaborators.
  - **Subnet information**
    -  IPv4 CIDR Block:
		- you can choose an IP range within or the same as the VPC IP range. For example, if the VPC IP range is 10.0.0.0/16, you can choose an IP range between 10.0.0.0/16 and 10.0.255.255/28 as the subnet IP range.
		- If the VPC in which subnets are located needs to communicate with other VPCs or IDCs, make sure that the subnet IP range does not overlap with the peer IP range. Otherwise, the interconnection through a private network may fail.
    - Availability Zone: select an availability zone in which the subnet resides. A VPC allows subnets in different availability zones, and these subnets can communicate with each other via a private network by default.
    - Advanced Options: you can optionally add tags to help you better manage resource permissions of sub-users and collaborators.

### Step 2: purchase a CVM instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) to create a CVM instance in the VPC created in the previous step.
2. Click **Create** in the top-left corner of the list page to access the CVM purchase page.
<img src="" width="80%">
3. On the custom configuration page, configure the CVM instance and then click **Buy Now**. The CVM network configurations are as follows:
 - Network: select the created VPC and subnet.
![](https://qcloudimg.tencent-cloud.cn/raw/7ec59dbff60a37870ef4f9cdaf2aff70.png)
 - Public network bandwidth: do not check <img src="https://main.qcloudimg.com/raw/50eef42428eb34dc35cf40995c9b7736.png" style="margin:-3px 0">.
![](https://qcloudimg.tencent-cloud.cn/raw/f59fd4da95bd18e3f8585a1541d7547b.png)
 - Security Group: select **New security group** and configure it as instructed in [Configuring Security Groups](https://intl.cloud.tencent.com/document/product/213/15377).
![](https://qcloudimg.tencent-cloud.cn/raw/72584971b62015e38c9ad22da7ddd3d4.png)

### Step 3: apply for an EIP and bind it to the CVM instance
Elastic IP (EIP) is a public IP address that can be applied for and purchased independently. You can bind it to a CVM instance to enable public network access.
1. Log in to the [EIP console](https://console.cloud.tencent.com/cvm/eip).
2. On the **EIP** page, select the region where the CVM is located. Click **Apply** in the top-left corner.
3. In the **Apply for EIP** window, configure relevant parameters and click **OK**.
4. On the **EIP** page, locate the EIP you applied for, and click **More** > **Bind** under its **Operation** column.
5. In the **Bind resources** window, select **CVM Instances** as the resource type to be bound, select the CVM instance, and click **OK**.
![]()
6. In the pop-up confirmation window, click **OK**.


### Step 4: test public network connectivity
Complete the following operations to test the public network connectivity of the CVM instance.
>?Before performing the test, make sure that the security group allows access to the corresponding IP address and port. For example, the ICMP protocol is opened, and the server can be pinged over the public network. For more information, see Viewing a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35514).
>
1. Log in to the CVM instance with an EIP bound. For detailed directions, see [Login and Remote Access](https://intl.cloud.tencent.com/document/product/213/17278).
2. Run the `ping <public IP address>` command, such as `ping www.qq.com` to test public network connectivity.
![](https://main.qcloudimg.com/raw/e19b0921e6d0471ca0e9b78923ccdd06.png)

