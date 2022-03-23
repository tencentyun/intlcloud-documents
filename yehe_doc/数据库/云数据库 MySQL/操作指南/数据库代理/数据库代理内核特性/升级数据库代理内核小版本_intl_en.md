This document describes how to manually upgrade the kernel minor version of the database proxy in the console.

## Prerequisites
You have [enabled the database proxy](https://intl.cloud.tencent.com/document/product/236/42052).

## Notes
- There will be a momentary disconnection when you upgrade the kernel minor version of the database proxy. Therefore, upgrade the version during off-peak hours and make sure that your application has an automatic reconnection mechanism.
- If the upgrade fails, the reason may be that the kernel minor version of the database is earlier than 20211031. In this case, upgrade the kernel version of the database first and then upgrade the kernel version of the database proxy.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab.
3. In **Overview** > **Basic Info** > **Proxy Version** on the **Database Proxy** tab, click **Upgrade Kernel Minor Version**.
![](https://qcloudimg.tencent-cloud.cn/raw/b3e4b48ccd4faff89c72e658aebc6925.png)
4. In the pop-up window, check the target version and select the upgrade switch time. After confirming that everything is correct, click **OK**.
Switch Time:
    - During maintenance time: The upgrade will be performed during the maintenance time, which can be modified on the instance details page.
    - Upon upgrade completion: The upgrade will be performed immediately after the upgrade operation is confirmed.
>!
>- There will be a momentary disconnection during upgrade. Therefore, make sure that your business has a reconnection mechanism.
>- During the kernel minor version upgrade, all nodes will be upgraded at the same time by default, but abnormal nodes cannot be upgraded.
>
![](https://qcloudimg.tencent-cloud.cn/raw/ef9c24a60a94603205fe2d30376cb74f.png)

