## Network Overview
Tencent Cloud offers [VPC](https://intl.cloud.tencent.com/document/product/215) (recommended) and classic network environments. A VPC is a logically isolated network space that can be customized in Tencent Cloud. Similar to the traditional network run in an IDC, a VPC is where your Tencent Cloud service resources are managed, such as [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/495), [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524), and [TencentDB](https://intl.cloud.tencent.com/document/product/236/5147).
For the differences between VPC and classic network, please see [VPC and Classic Network](https://intl.cloud.tencent.com/document/product/215/35505).
For common operations on VPCs and subnets, please see [Managing VPC and Subnet](https://intl.cloud.tencent.com/document/product/215/31805).

## Redis Network Configuration
1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis) and click **Create Instance** in the instance list.
2. In "Network Type" on the purchase page, you can choose the classic network or a **VPC** (recommended).
![](https://main.qcloudimg.com/raw/8be0e67db61e588d2b8ec4bc43ef2c1f.png)

## Redis Network Change
>!To ensure service availability and keep your businesses uninterrupted during network change, update the IP address as needed promptly and be cautious in releasing the old IP address.
>
1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis) and click an instance ID in the instance list to enter the instance details page.
2. In the "Network Info" module, you can view the network and private IP of the current TencentDB for Redis instance. You can also click **Change Network** to change from the classic network to VPC or from the current VPC to another VPC.
![](https://main.qcloudimg.com/raw/882d495354b725a4fa0b4d9b6b513d29.png)
3. In the pop-up dialog box, configure new network information and click **OK**.
  - New IP: you can choose to automatically assign or specify an address.
  - Old IP: you can choose to release it immediately or in days so as to ensure business continuity during the network change.
![](https://main.qcloudimg.com/raw/1befc1f612813a27792cd811b7c2f8c1.png)

