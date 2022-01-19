This document describes how to adjust the instance version in the TencentDB for SQL Server console.

## Prerequisites
You can adjust the configuration of a TencentDB for SQL Server instance and its associated instances only when they are in normal status (Running) and are not executing any tasks.

## Notes
Currently, the database version cannot be downgraded back after an upgrade.

## Impact of Configuration Adjustment
- Data migration will be involved during the instance configuration adjustment, and the higher the data volume, the longer the data migration time. Access to the instance will not be affected during this period.
>- A switch will be performed after migration completion, which is accompanied by a disconnection from the database lasting for just seconds. Make sure that your business has a reconnection mechanism.
- During the momentary disconnection, most operations related to databases, accounts, and networks cannot be executed. Therefore, be sure to perform the switch during off-peak hours.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select the region and target instance in the instance list, and click **Adjust Configuration** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/84f60eedd1e5492b31da602ef387b9f9.png)
2. In the **Adjust Configuration** window that pops up, select the desired **database version** and click **Confirm**.
>?Select the **Time to Take Effect** of the configuration adjustment and click the orange note.
> - During maintenance time: you can modify the maintenance time on the instance details page.
>- Adjust now: the configuration adjustment will be performed immediately.
>
![](https://qcloudimg.tencent-cloud.cn/raw/f232f1ed96e136d859685b302d3061cf.png)
3. On the payment page you are redirected to, confirm the configuration information and fees and click **Submit Order**.
4. You will be redirected to the instance list. When the instance status changes from **Switching (after configuration adjustment)** to **Running**, the version upgrade is completed. You can query and check the new version on the **Instance List** or **Instance Details** page.

