This document describes how to manually upgrade the kernel minor version of the database proxy in the console.

## Prerequisite
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/236/42052).

## Notes
- There will be a momentary disconnection when you upgrade the kernel minor version of the database proxy. Therefore, upgrade the version during off-peak hours and make sure that your application has an automatic reconnection mechanism.
- If the upgrade fails, the reason may be that the kernel minor version of the database is earlier than 20211031. You need to upgrade the kernel minor version of the database before upgrading the kernel version of the database proxy. For more information, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/236/36816)

## Directions
1. Log in to the [TencentDB for MySQL console] (https://console.cloud.tencent.com/cdb). Select the region at the top and click the target instance ID to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab.
3. In **Overview** > **Basic Info** > **Proxy Version** on the **Database Proxy** tab, click **Upgrade Kernel Minor Version**.
![](https://qcloudimg.tencent-cloud.cn/raw/b3e4b48ccd4faff89c72e658aebc6925.png)
4. In the pop-up window, check the target version and select the upgrade switch time. After confirming that everything is correct, click **OK**.
Switch Time:
  - During maintenance time: The upgrade will be performed during the maintenance time, which can be modified on the instance details page.
  - Upon upgrade completion: The upgrade will be performed immediately after the upgrade operation is confirmed.
>!
>- There will be a momentary disconnection during upgrade. Therefore, make sure that your business has a reconnection mechanism.
>- Except for abnormal nodes, all nodes are upgraded at the same time by default during the kernel minor version upgrade.
>
![](https://qcloudimg.tencent-cloud.cn/raw/ef9c24a60a94603205fe2d30376cb74f.png)
