
## Overview
TencentDB for MySQL supports quick adjustment of instance specification and allows flexible scaling operations. You can elastically adjust the specifications of MySQL instances according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization. For details on instance adjustment fees, please see [Instance Adjustment Fee](https://intl.cloud.tencent.com/document/product/236/32345).

#### Instance disk space description
- To ensure business continuity, upgrade your instance specifications or purchase additional disk capacity in time before disk capacity is used up.
>?You can view disk space on the instance details page in the [MySQL Console](https://console.cloud.tencent.com/cdb), or receive disk alarms with the [Alarming Feature](https://intl.cloud.tencent.com/document/product/236/8457).
- When the size of the data stored on an instance exceeds its capacity limit, the instance will be locked and become read-only. You will not be able to write data to it. You will need to expand its capacity or delete some database tables in the console to unlock it.
- To avoid the database from triggering the lock status repeatedly, a locked instance will be unlocked and allowed for reads and writes only when its remaining available capacity accounts for more than 20% of its total capacity or over 50 GB.

<span id="guize"></span>
## Configuration Adjustment Rules
- You can adjust the configuration of a TencentDB for MySQL instance and its associated instances only when they are in normal status (running) and are not executing any tasks.
- You cannot cancel a configuration adjustment operation in progress.
- The name, access IP, and access port of an instance will remain the same after configuration adjustment.
- During configuration adjustment, you should try to avoid such operations as modifying MySQL's global parameters and user password.
- Data migration may be involved in configuration adjustment. During data migration, the TencentDB for MySQL instance can be accessed normally and the business will not be affected.
- Instance switchover may be needed after configuration adjustment is completed (i.e., the MySQL instance may be disconnected for seconds). It is recommended that applications be configured with auto reconnection feature and that instance switchover be conducted during the instance maintenance period. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/236/10929).
- For TencentDB for MySQL Basic Edition, instances are unavailable for about 15 minutes in the process of configuration adjustment. We recommend that you adjust instance configuration during off-peak hours.

## Directions
### Adjusting the instance configuration in the console
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb), find the desired instance in the instance list, and select **More** > **Adjust Configurations** in the "Operation" column.
![](https://main.qcloudimg.com/raw/bddf4d9354753da23a0730fb91e01227.png)
2. In the pop-up dialog box, adjust the instance configurations, and click **Submit**.

![](https://main.qcloudimg.com/raw/fd7b5ead8e0aaeaa89248dcf12f58c02.png)

### Adjusting the instance configuration through the API
You can adjust the instance configuration using the [UpgradeDBInstance](https://intl.cloud.tencent.com/document/product/236/15876) API.

## FAQs
#### Will instance configuration adjustment affect instances?
- In the process of TencentDB for MySQL configuration adjustment, data migration may occur, and instances can still be accessed during the process. After the migration is completed, there is a switch which causes a short disconnection lasting for just seconds, please ensure that your business has a reconnection mechanism.
- For TencentDB for MySQL Basic Edition, instances are unavailable for about 15 minutes in the process of configuration adjustment. We recommend that you adjust instance configuration during off-peak hours.

#### Why can't my instance be downgraded?
It may be because your storage capacity has exceeded the maximum capacity of the hard disk. To downgrade you instance, you need to clean up data first and make sure the remaining available capacity accounts for more than 20% of the total capacity or over 50 GB.

#### Why is my instance in the "Waiting for switch" status for a long time after I adjust instance configuration in the console?
It may be because you select **During maintenance window** as the **Switch Time** when you adjust instance configuration in the [console](https://console.cloud.tencent.com/cdb), so the instance will not be switched immediately after the adjustment.
To switch immediately, you can locate the desired instance in the instance list and click **Switch Now** in the **Operation** column. The switch causes a short disconnection lasting for just seconds, please ensure that your business has a reconnection mechanism.

#### How long does it take to upgrade instance configuration?
The time it takes depends on the data volume and data replication and read requests of your instance. Instances can still be accessed during the upgrade, but after the upgrade is completed, there is a VIP switch which causes a short disconnection lasting for just seconds.

#### How do I view the progress of instance configuration adjustment?
You can view the progress in [Task List](https://console.cloud.tencent.com/mysql/task) in the console.

#### What should I do if the disk space is being used up?
If over 85% disk space is used, we recommend that you delete data no longer used or expand disk space in the [console](https://console.cloud.tencent.com/cdb).
