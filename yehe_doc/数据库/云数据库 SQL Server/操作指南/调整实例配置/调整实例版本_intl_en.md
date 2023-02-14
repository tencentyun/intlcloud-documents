This document describes how to adjust the instance version in the TencentDB for SQL Server console.

## Supported versions
TencentDB for SQL Server Basic, Dual-Server High Availability, and Cluster Editions support version upgrade.

## Prerequisites
You can adjust the configuration of a TencentDB for SQL Server instance and its associated instances only when they are in running status and are not executing any tasks.

## Notes
Currently, the database version cannot be downgraded back after an upgrade.

## Impact of configuration adjustment
- Data migration will occur during the instance configuration adjustment, and the larger the data volume, the longer the data migration time. During this period, access to the instance will not be affected.
>- A switch will be performed after migration is completed, which causes a momentary disconnection from the database for few seconds. Make sure that your business has a reconnection mechanism.
- Most database, account, and network operations are unavailable during the momentary disconnection. Therefore, we recommend you perform the switch during off-peak hours.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select the region and target instance in the instance list, and click **Adjust Configuration** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/IQuS751_25.png)
2. In the **Adjust Configuration** window that pops up, select the desired **database version** and click **Confirm**.
>?Select the **Time to Take Effect** of the configuration adjustment and click the orange note.
> - During maintenance time: You can modify the maintenance time on the instance details page.
> - Adjust now: The configuration adjustment will be performed immediately.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/u8ch887_26.png)
3. In the payment window that pops up, confirm the configuration information and fees and click **Submit**. For pay-as-you-go instances, click **Adjust** in the window.
4. You will be redirected to the instance list. When the instance status changes from **Adjusting instance configuration** to **Running**, the version upgrade is completed. You can query and check the new version on the **Instance List** or **Instance Details** page.
