## Network Environment Overview
Tencent Cloud offers two network environments: [Virtual Private Cloud](https://intl.cloud.tencent.com/product/vpc?idx=2) (VPC) and basic network, of which the former is recommended.
VPC is a logically isolated network space that can be customized in Tencent Cloud. Similar to the traditional network run in an IDC, the VPC is where your Tencent Cloud service resources are managed, such as [Cloud Virtual Machine](http://intl.cloud.tencent.com/document/product/213/495), [Cloud Load Balancer](http://intl.cloud.tencent.com/document/product/214/524), and [TencentDB](https://intl.cloud.tencent.com/doc/product/236).
For the differences between basic network and VPC, see [VPC Overview](http://intl.cloud.tencent.com/document/product/215/535).

## Configuring a Network for TencentDB for Redis
### Configuring a Network for a Newly Purchased Redis Instance
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/), select **Cloud Products** > **Database** > **TencentDB for Redis** to enter the TencentDB for Redis Console, and click **Create Instance** to create a database; or, go to [Tencent Cloud's official website](https://cloud.tencent.com/), select **Products** > **Basic** > **Database** > **TencentDB for Redis**, click **Buy Now**, and then create a database on the [TencentDB for Redis Purchase Page](https://buy.cloud.tencent.com/buy/redis?regionId=4#/).

![](https://main.qcloudimg.com/raw/f391b05ba2abb90f54d68eee3c075fa5.png)
2. On the [TencentDB for Redis Purchase Page](https://buy.cloud.tencent.com/buy/redis?regionId=4#/), find **Network Type**, select **Basic Network** or **VPC** (recommended), and select an existing **VPC** and **Subnet**; if there are no VPCs in the current **availability zone**, please [Create VPC](https://console.cloud.tencent.com/vpc/vpc?rid=4) first, refresh **Network Type** on the purchase page, and then select the VPC.

![](https://main.qcloudimg.com/raw/8be0e67db61e588d2b8ec4bc43ef2c1f.png)
### Changing Network for an Existing Redis Instance
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Cloud Products** > **Database** > **TencentDB for Redis** to enter the TencentDB for Redis Console.
2. In the TencentDB for Redis Console, click **Instance List** and then click **ID/Instance Name** to enter the **Instance Details** page.

![](https://main.qcloudimg.com/raw/8a2383161e87e03ca1c53c33b935274f.png)
![](https://main.qcloudimg.com/raw/882d495354b725a4fa0b4d9b6b513d29.png)
3. In the **Network Info** section of **Instance Details**, you can view network information such as the network where the current Redis instance resides and the VPC address. Click **Change Network** to switch from **Basic Network** to **VPC**, or from one **VPC** to another **VPC**. **New IP** can be automatically assigned or specified, and **Old IP** can be released immediately or after a few days to ensure business continuity during network change. Click OK to finish the process.
> The old IP address can be released immediately or after a few days. To ensure service availability and keep your businesses uninterrupted during network change, update the IP address as needed in a timely manner and be cautious in releasing the old IP address.
>
![](https://main.qcloudimg.com/raw/1befc1f612813a27792cd811b7c2f8c1.png)

## Basic Operations of a VPC
When using a VPC for TencentDB for Redis, problems may be encountered when you create a VPC or ENI and bind or unbind HAVIP, among other actions. This document describes common operations for using VPCs and relevant products for your reference.

### VPC and Subnet
The relationship between [VPC and subnet](http://intl.cloud.tencent.com/document/product/215/4927) is as follows: A subnet is an IP address block within a VPC, and all Tencent Cloud resources in the VPC must be deployed in subnets. A subnet has an attribute of AZ. Once a VPC is created, you can create a subnet in each AZ in the region where the VPC is located. The following introduces common operations for VPCs, subnets, and relevant products for your reference.
- [Creating a VPC](https://intl.cloud.tencent.com/document/product/215/8113)
- [Creating a Subnet](https://intl.cloud.tencent.com/document/product/215/8114)
- [Deleting a VPC](https://cloud.tencent.com/document/product/215/20113)
- [Deleting a Subnet](https://cloud.tencent.com/document/product/215/20114)

For more information, see [Overview of VPC and Subnet Operations](https://cloud.tencent.com/document/product/215/20121).

## Network Connection to TencentDB for Redis
When TencentDB for Redis is used in cache, storage, and computing scenarios, network connection problems in CVM and TencentDB may be encountered. The two can be deployed in the same region or in different regions, involving communication between basic network and VPC, and communication between VPCs. For more information, see [TencentDB for Redis Connection and Login Problems](http://intl.cloud.tencent.com/document/product/239/18664).

