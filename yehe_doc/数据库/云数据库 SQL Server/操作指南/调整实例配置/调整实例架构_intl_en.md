
This document describes how to adjust the instance architecture in the TencentDB for SQL Server console.

## Architecture background
TencentDB for SQL Server supports the following architectures:

| Type | Description |
|---------|---------|
| Single-node (formerly Basic Edition) | (1) It is deployed on a single node and based on premium cloud disks, with computing and storage separated. <br>(2) It offers extremely high cost-effectiveness. |
| Two-node (formerly High Availability/Cluster Edition) <br>2008 R2/2012/2014/2016 Enterprise | (1) It consists of one primary database and one mirror database deployed across racks/AZs. <br>(2) Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time. |
| Two-node (formerly High Availability/Cluster Edition) <br>2017/2019 Enterprise | (1) It adopts the Always On cluster deployment architecture, including one primary and one replica deployed across racks/AZs by default. <br>(2) Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time. |

For detailed descriptions, see [Product Architecture](https://intl.cloud.tencent.com/document/product/238/3254).

## Prerequisites
- You can adjust the configuration of a TencentDB for SQL Server instance and its associated instances only when they are in running status and are not executing any tasks.


## Notes
Currently, the architecture cannot be downgraded back after an upgrade.

## Impact of configuration adjustment
- Data migration will be involved during the instance configuration adjustment, and the larger the data volume, the longer the data migration time. Access to the instance will not be affected during this period.
>- A switch will be performed after migration is completed, which causes a momentary disconnection from the database for few seconds. Make sure that your business has a reconnection mechanism.
- Most database, account, and network operations are unavailable during the momentary disconnection. Therefore, we recommend that you perform the switch during off-peak hours.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), select the region and target instance in the instance list, and click **Adjust Configuration** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/84f60eedd1e5492b31da602ef387b9f9.png)
2. In the **Adjust Configuration** window that pops up, select the desired architecture and click **Confirm**.
>?If data migration is involved during the change, you need to select the effective time and click the orange note; otherwise, you don't need to select the effective time.
>- During maintenance time: You can modify the maintenance time on the instance details page.
>- Adjust now: The configuration adjustment will be performed immediately.
>
![](https://qcloudimg.tencent-cloud.cn/raw/a84d518ad3526ffd1958cca11061f0a3.png)
3. You will be redirected to the instance list. When the instance status changes from **Switching (after configuration adjustment)** to **Running**, the architecture upgrade is completed. You can query and check the new architecture on the **Instance List** or **Instance Details** page.
