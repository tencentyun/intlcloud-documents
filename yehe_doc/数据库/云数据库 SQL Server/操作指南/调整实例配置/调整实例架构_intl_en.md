
This document describes how to adjust the instance architecture in the TencentDB for SQL Server console.

## Architecture Background
TencentDB for SQL Server supports the following deployment architectures:

| Type | Description |
|---------|---------|
| Basic Edition | a. It separates computing and storage based on Premium Cloud Storage and is deployed on a single node. <br>b. It offers extremely high cost-effectiveness. |
| Dual-Server High Availability Edition | a. It consists of one primary database and one mirror database deployed across racks/AZs. <br>b. Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time. |
| Cluster Edition | a. It adopts the Always On cluster deployment architecture, including one primary and one replica deployed across racks/AZs by default. <br>b. Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time. |

For more information, see [Architecture](https://intl.cloud.tencent.com/document/product/238/3254).

## Prerequisites
- You can adjust the configuration of a TencentDB for SQL Server instance and its associated instances only when they are in normal status (Running) and are not executing any tasks.
- Only the High-Availability Edition (SQL Server 2017 Enterprise and above) can be adjusted to the Cluster Edition.

## Notes
Currently, the architecture cannot be downgraded back after an upgrade.

## Impact of Configuration Adjustment
- Data migration will be involved during the instance configuration adjustment, and the higher the data volume, the longer the data migration time. Access to the instance will not be affected during this period.
>- A switch will be performed after migration completion, which is accompanied by a disconnection from the database lasting for just seconds. Make sure that your business has a reconnection mechanism.
- During the momentary disconnection, most operations related to databases, accounts, and networks cannot be executed. Therefore, be sure to perform the switch during off-peak hours.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select the region and target instance in the instance list, and click **Adjust Configuration** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/84f60eedd1e5492b31da602ef387b9f9.png)
2. In the **Adjust Configuration** window that pops up, select the desired architecture and click **Confirm**.
>?If data migration is involved during the change, you need to select the effective time and click the orange note; otherwise, you don't need to select the effective time.
>- During maintenance time: you can modify the maintenance time on the instance details page.
>- Adjust now: the configuration adjustment will be performed immediately.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a84d518ad3526ffd1958cca11061f0a3.png)
3. On the payment page you are redirected to, confirm the configuration information and fees and click **Submit Order**.
4. You will be redirected to the instance list. When the instance status changes from **Switching (after configuration adjustment)** to **Running**, the architecture upgrade is completed. You can query and check the new architecture on the **Instance List** or **Instance Details** page.


