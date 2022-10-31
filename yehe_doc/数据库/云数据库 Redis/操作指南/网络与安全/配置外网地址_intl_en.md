This document describes how to enable/disable the public network address in the TencentDB for Redis console. You can use the system-assigned domain name and port to [Accessing Database over Public Network](https://intl.cloud.tencent.com/document/product/239/47571), making it easier for you to test, manage, use, and develop the database on a daily basis.

>?
>- The instance service downtime caused by public network errors won't be counted into the "Single Instance Service Downtime" in Redis Service Level Agreement (SLA).
>- Public network access may expose your instances to security threats, and service availability is not guaranteed by SLA. Therefore, we recommend that you access Redis over the public network only when testing, managing, or assisting in managing databases. In the production environment, access Redis over the private network.
>

## Notes
1. When it is enabled, you can use the system-assigned domain name and port to access TencentDB for Redis via public network. It takes about 5 minutes to take effect.
2. You can only develop or help manage the database via public network. You must access your business over the private network.
3. After the public network access is enabled, it will be controlled by the security group policy. You should configure the database access source in the security group's inbound rules and open the protocol ports (both the private network port (6379 by default) and public network port) as instructed in [Configuring Security Group](https://intl.cloud.tencent.com/document/product/239/31945).
4 The instance service downtime caused by public network errors won't be counted into the "Single Instance Service Downtime" in Redis Service Level Agreement (SLA).

## Prerequisite
- Only instances in VPCs can enable the public network address. If an instance is in the classic network, switch it to VPC first before enabling public network access. For more information, see [Configuring Network](https://intl.cloud.tencent.com/document/product/239/31944)
- Currently, the public network address can be enabled for the instances in Chengdu, Beijing, Shanghai, and Guangzhou regions. To use it in other regions, you can access the TencentDB for Redis instance through iptables-based forwarding. For more information, see [Connecting to TencentDB for Redis Instance](https://intl.cloud.tencent.com/document/product/239/9897).
- To enable public network access, you need to disable [password-free access](https://intl.cloud.tencent.com/document/product/239/32548)

## Enabling the Public Network Address
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance details page.
2. Click **Enable** next to **Public Network Address** in the **Network Info** block.
>!After the public network access is enabled, it will be controlled by the security group policy. You should configure the database access source in the security group's inbound rules and open the protocol ports (both the private network port (6379 by default) and public network port) as instructed in [Configuring Security Group](https://intl.cloud.tencent.com/document/product/239/31945).
>
![](https://qcloudimg.tencent-cloud.cn/raw/e321411f59c98cb56089da38f5daec81.png)
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/68286671abbbff9a56a73b7890b7b9bf.png)
4. Return to the instance details page, where you can see the instance in the **Enabling public network** status. If the status stays the same for a long time, refresh the page.
5. If **Public Network Address** shows an address comprising a domain name and port, the address is enabled successfully. Now you can use it to access Redis over the public network.
![](https://qcloudimg.tencent-cloud.cn/raw/0e7954a9edb62be93308250c125c8387.png)

## Disabling the Public Network Address
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance details page.
2. Click **Disable** next to **Public Network Address** in the **Network Info** block.
![](https://qcloudimg.tencent-cloud.cn/raw/c4e569e1f967c6da605fe8e5a4206a1a.png)
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.
4. Return to the instance details page, where you can see the instance in the **Disabling public network** status and **Public Network Address** display nothing.

## Related APIs

| API | Description |
|---------|---------|
| [AllocateWanAddress](https://intl.cloud.tencent.com/document/product/239/46976) | Enables public network access |
| [ReleaseWanAddress](https://intl.cloud.tencent.com/document/product/239/46975) | Disables public network access |

