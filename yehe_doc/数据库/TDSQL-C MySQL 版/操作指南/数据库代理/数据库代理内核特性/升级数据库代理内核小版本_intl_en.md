This document describes how to manually upgrade the kernel minor version of the database proxy in the console.

## Prerequisite
You have enabled the database proxy. For more information,see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/1098/49999).

## Notes
There will be a momentary disconnection when you upgrade the kernel minor version of the database proxy. Therefore, upgrade the version during off-peak hours and make sure that your application has an automatic reconnection mechanism.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql), select the region at the top of the page, and click the ID of the target cluster to enter the cluster management page.
2. On the cluster management page, select the **Database Proxy** tab.
3. In **Overview** > **Basic Info** > **Proxy Version** on the **Database Proxy** tab, click **Upgrade Kernel Minor Version**.
4. In the pop-up window, check the target version and select the upgrade switch time. After confirming that everything is correct, click **OK**.
   Switch Time:
    - During maintenance time: The upgrade will be performed during the maintenance time, which can be modified on the instance details page.
    - Upon upgrade completion: The upgrade will be performed immediately after the upgrade operation is confirmed.
>!
>- There will be a momentary disconnection during upgrade. Therefore, make sure that your business has a reconnection mechanism.
>- Except for abnormal nodes, all nodes are upgraded at the same time by default during the kernel minor version upgrade.
>

