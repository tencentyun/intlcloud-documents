This document describes how to enable/disable the public network address in the TencentDB for Redis console. You can use the system-assigned domain name and port to access an instance over the public network, facilitating your daily test, management, use, and development of the database.

>?
>- The instance service downtime caused by public network errors won't be counted into the "Single Instance Service Downtime" in Redis Service Level Agreement (SLA).
>- Public network access will undermine the security of instances, and service availability is not guaranteed by SLA. Therefore, we recommend you access Redis over the public network only when testing, managing, or assisting in managing databases. In the production environment, please access Redis over the private network.

## Prerequisites
- Only instances in VPCs can enable the public network address.
- Currently, only instances in the Chengdu, Beijing, Shanghai, and Guangzhou regions can enable the public network address.

## Enabling the Public Network Address
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance details page.
2. Click **Enable** next to **Public Network Address** in the **Network Info** block.
![](https://qcloudimg.tencent-cloud.cn/raw/45ba379ace466f7256e489387661bacb.png)
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/7644853f0a294487b0fd44e0d9657479.png)
4. Return to the instance details page, where you can see the instance in the **Enabling public network** status. If the status stays the same for a long time, please refresh the page.
5. If **Public Network Address** shows an address comprising a domain name and port, the address is enabled successfully. Now you can use it to access Redis over the public network.
>?After the public network access to TencentDB for Redis is enabled, it will be controlled by the security group policy. For more information, please see [Configuring Security Groups](https://intl.cloud.tencent.com/document/product/239/31945).
>
![](https://qcloudimg.tencent-cloud.cn/raw/14843fcd53a18df45726b3456b44f465.png)

## Disabling the Public Network Address
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance details page.
2. Click **Disable** next to **Public Network Address** in the **Network Info** block.
![](https://qcloudimg.tencent-cloud.cn/raw/4bcd7d4d286ccce548c393433bece283.png)
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.
4. Return to the instance details page, where you can see the instance in the **Disabling public network** status and **Public Network Address** display nothing.

