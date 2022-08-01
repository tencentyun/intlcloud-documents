## Network overview

Tencent Cloud offers [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215) (recommended) and classic network environments. A VPC is a logically isolated network space that can be customized in Tencent Cloud. Similar to the traditional network run in an IDC, a VPC is where your Tencent Cloud service resources are managed, such as [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/495), [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524), and [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/5147).
The difference between classic network and VPC is as follows:
- The classic network is a public network resource pool shared by all Tencent Cloud users. The private IPs of all CVM instances are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses.
- A VPC is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies, making it more suitable for use cases requiring custom configurations.
  - A subnet is a network space in a VPC where Tencent Cloud resources are deployed. A VPC has at least one subnet. An initial subnet will be created together with a VPC. You can also create more subnets in a VPC that suit your specific requirements to deploy different businesses.
  - A subnet is AZ-specific. You can create subnets in different AZs in the same VPC, which communicate with each other over the private network by default.
![](https://qcloudimg.tencent-cloud.cn/raw/eadfeac00fadeb298413d42ef091e38d.png)

## Notes

- You can switch from classic network to VPC but not vice versa.
- You can switch from one VPC to another or between subnets in the same VPC.
- After the network switch, the new IP address will take effect immediately, and all connections to the original IP address will be closed. The original IP address will be retained for up to 15 days.

>!To ensure the service availability and keep your businesses uninterrupted during network switch, update the IP address promptly as needed and be cautious about releasing the old IP address.

## Prerequisites

- You have created a database instance and configured the classic network or VPC as instructed in [Creating TencentDB for Redis Instance](https://intl.cloud.tencent.com/document/product/239/37712).
- You have created the target VPC as instructed in [Creating VPC](https://intl.cloud.tencent.com/document/product/215/31805).
- The database instance is in **Running** status, with no ongoing tasks.

## Changing the network

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the target instance ID to enter the **Instance Details** page.
5. In the **Network Info** section on the **Instance Details** page, you can see the network and private IP of the current TencentDB for Redis instance. Click **Change Network** next to **Network**.
In this way, you can switch from the classic network to a VPC or from the current VPC to another VPC.
![](https://qcloudimg.tencent-cloud.cn/raw/cb6d76439123170f21225ee2b052d568.png)
6. In the **Change Network** window, configure the new network information and click **OK**.
   - **Network**: Select a VPC and a subnet in the drop-down lists next to **Network** respectively.
   - **New IP**: Select **Auto Assign** or **Designate Address**. If you select the latter, then enter a custom IP address in the input box.
   - **Old IP**: Set the release time of the old IP. You can select **Release Now**, **Release after 1 day**, **Release after 2 days**, **Release after 3 days**, **Release after 7 days**, or **Release after 15 days** as needed to ensure the business continuity during the network change.
![](https://qcloudimg.tencent-cloud.cn/raw/94543dfc8284575ad4989f5706e14c1a.png)

## Changing the subnet

>!
> - The subnet change feature is available only when the **Network** is **VPC**.
> - The subnet can be changed only to another subnet in the same AZ.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the target instance ID to enter the **Instance Details** page.
5. In the **Network Info** section, you can see the network and private IP of the current TencentDB for Redis instance. Click **Change Subnet**.
![](https://qcloudimg.tencent-cloud.cn/raw/e0dc10a696e72b12b96ab5923202d5d7.png)
6. In the pop-up window, select the target subnet and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/eba35ebe27df4dea797a0e5a9ef8fbe0.png)

## Related APIs

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [ModifyNetworkConfig](https://intl.cloud.tencent.com/document/product/239/32056) | Modifies the network configuration of an instance. |

