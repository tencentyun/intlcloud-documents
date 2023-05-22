This tutorial describes how to quickly build up a Virtual Private Cloud (VPC) with IPv4 CIDR blocks.
## Scenarios
This document guides through whole process of setting up an IPv4-based VPC. 
![](https://qcloudimg.tencent-cloud.cn/raw/926843feffd998e8dbf151b63178b366.png)

## Prerequisites
Before using Tencent Cloud products, [create a Tencent Cloud account](https://www.tencentcloud.com/account/register) and complete [identity verification](https://www.tencentcloud.com/document/product/378/3629).

## Directions
### Step 1: create a VPC and subnet
>? Once created, the CIDR blocks (IP ranges) of VPCs and subnets cannot be modified. Therefore, complete [network planning](https://www.tencentcloud.com/document/product/215/31795) in advance.
>
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select a region at the top of the page and click **+ New**.
3. In the **Create VPC** pop-up window, configure the VPC and subnet information as instructed below.
![](https://qcloudimg.tencent-cloud.cn/raw/ba0387f51ed8112ab819d5cb9c5113b5.png)
 - **VPC information**
    - Name: the name of the VPC.
    - IPV4 CIDR Block: You can choose any one of the IP ranges as the VPC IP range, such as `10.0.0.0/16`.
      - `10.0.0.0` - `10.255.255.255` (mask range: 12 to 28)
      - `172.16.0.0` - `172.31.255.255` (mask range: 12 to 28)
      - `192.168.0.0` - `192.168.255.255` (mask range: 16 to 28)
     - Tags: You can optionally add tags to help you better manage resource permissions of sub-users and collaborators.
  - **Subnet information**
    - IPv4 CIDR Block:
		- You can choose an IP range within or the same as the VPC IP range. For example, if the VPC IP range is `10.0.0.0/16`, you can choose an IP range between `10.0.0.0/16` and `10.0.0.248/29` as the subnet IP range.
		- If the VPC in which subnets are located needs to communicate with other VPCs or IDCs, make sure that the subnet IP range does not overlap with the peer IP range. Otherwise, the interconnection over a private network may fail.
    - Availability Zone: select an availability zone in which the subnet resides. A VPC allows subnets in different availability zones, and these subnets can communicate with each other via a private network by default.
    - Tags: You can optionally add tags to help you better manage resource permissions of sub-users and collaborators.

### Step 2: purchase a CVM instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm) to create a CVM instance in the VPC created in the previous step.
2. Click **Create** in the top-left corner of the list page to go to the [CVM purchase page](https://buy.intl.cloud.tencent.com/cvm?tab=custom).
3. On the custom configuration page, configure the CVM instance and then click **Buy Now**. The CVM network configurations are as follows:
 - Network: select the created VPC and subnet.
![](https://qcloudimg.tencent-cloud.cn/raw/7ec59dbff60a37870ef4f9cdaf2aff70.png)
 - Public network IP: do not check <img src="https://main.qcloudimg.com/raw/50eef42428eb34dc35cf40995c9b7736.png" style="margin:-3px 0">.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HMtv404_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230522111237.png)
 - Security Group: select **New security group** and configure it as instructed in [Configuring Security Groups](https://www.tencentcloud.com/document/product/213/15377).
![](https://qcloudimg.tencent-cloud.cn/raw/72584971b62015e38c9ad22da7ddd3d4.png)

### Step 3: apply for an EIP and bind it to the CVM instance
An EIP is a public IP address that can be applied for and purchased independently. You can bind an EIP to a CVM instance to enable public network access.
1. Log in to the [EIP console](https://console.cloud.tencent.com/cvm/eip).
2. On the **EIP** page, select the region where the CVM instance is located. Click **Apply** in the top-left corner.
3. In the **Apply for EIP** pop-up window, configure relevant parameters and click **OK**.
4. On the **EIP** page, locate the EIP you applied for, and click **More** > **Bind** in the **Operation** column.
5. In the **Bind resources** window, select **CVM Instances** as the resource type to be bound, select the CVM instance, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/s36E860_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230406180609.png)
6. In the pop-up confirmation window, click **OK**.


### Step 4: test public network connectivity
Perform the following operations to test the public network connectivity of the CVM instance.
>?Before performing the test, make sure that the security group allows access to the corresponding IP address and port. For example, the ICMP protocol is opened, and the server can be pinged over the public network. For more information, see [Viewing a Security Group Rule](https://www.tencentcloud.com/document/product/215/35514).
>
1. Log in to the CVM instance with an EIP bound. For more information, see [Login and Connect to Instances](https://www.tencentcloud.com/document/product/213/17278).
2. Run the `ping Another public IP` command, such as `ping www.qq.com`, to test public network connectivity.
![](https://main.qcloudimg.com/raw/e19b0921e6d0471ca0e9b78923ccdd06.png)


