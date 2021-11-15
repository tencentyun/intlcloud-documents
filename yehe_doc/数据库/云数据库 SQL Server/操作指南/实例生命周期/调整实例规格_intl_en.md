## Operation Scenarios
TencentDB for SQL Server supports quick adjustment of instance specification and allows flexible scale-out operations. (Self-service degrading and scale-in are not supported currently. If needed, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.)
You can elastically adjust the instance specifications according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

#### Instance disk space description
- To ensure the normal operation of your business, please upgrade database instance specification or purchase more disk storage in time when your disk is going to run out of space.
- When the data size stored on the instance exceeds capacity limit, the instance is locked and only allows reading data (writing data is not allowed). You need to expand the capacity or delete some of the database tables in the console to remove the read-only status.
- To avoid the database from triggering the locked status repeatedly, a locked instance will be unlocked and allow reads and writes only when its remaining available space accounts for more than 20% of its total space or over 50 GB.

## Prerequisites
You can adjust the configuration of a TencentDB for SQL Server instance and its associated instances only when they are in normal status (running) and are not executing any tasks.

## Configuration Adjustment Rules
- You cannot cancel a configuration adjustment operation in progress.
- The name, access IP, and access port of an instance will remain the same after configuration adjustment.
- Data migration may be involved in configuration adjustment. During data migration, the TencentDB for SQL Server instance can be accessed normally, and the business will not be affected.
- Instance switch may be needed after configuration adjustment is completed (i.e., the TencentDB for SQL Server instance may be disconnected for seconds). It is recommended that applications be configured with auto reconnection feature. The instance switch will be conducted during instance maintenance window. For more information, please see [Setting Instance Maintenance Time](https://intl.cloud.tencent.com/document/product/238/35785).

## Directions
1. Log in to the [TencentDB for SQL Server Console](https://console.cloud.tencent.com/sqlserver), select the target instance in the instance list, and click **Upgrade** in the "Operation" column.
![](https://main.qcloudimg.com/raw/1fbf33d88523863129042fc58afea8ac.png)
2. In the pop-up instance upgrade dialog box, select the target specification, and click **Upgrade**.
>
>- Before maintenance is carried out for TencentDB for SQL Server, notifications will be sent to the contacts configured in your Tencent Cloud account through SMS and email.
>- If instance switch is involved, it will be performed during the maintenance window you configured. You can also initiate a manual switch after the migration is completed. Please be sure to switch during off-peak hours.
>
![](https://main.qcloudimg.com/raw/3d739db1f7bdf171b133b315c7b62773.png)
3. On the order information page, after confirming that everything is correct, click **Buy Now**.
4. Make the payment and return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.


