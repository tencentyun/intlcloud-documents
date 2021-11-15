TencentDB for MySQL supports quick adjustment of instance specification and allows flexible scaling operations in the console. You can elastically adjust the specifications of MySQL instances according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization. For details on instance adjustment fees, please see [Instance Adjustment Fee](https://intl.cloud.tencent.com/document/product/236/32345).

## Instance Disk Space Description
- To ensure business continuity, upgrade your instance specifications or purchase additional disk capacity in time before disk capacity is used up.
>?You can view disk space on the instance details page in the [MySQL console](https://console.cloud.tencent.com/cdb), or receive disk alarms according to the [Alarm Policies (Cloud Monitor)](https://intl.cloud.tencent.com/document/product/236/8457).
- When the size of the data stored on an instance exceeds its capacity limit, the instance will be locked and become read-only. You will not be able to write data to it. You will need to expand its capacity or delete some database tables in the console to unlock it.
- To avoid the database from triggering the lock status repeatedly, a locked instance will be unlocked and allowed for reads and writes only when its remaining available capacity accounts for more than 20% of its total capacity or over 50 GB.

## Configuration Adjustment Description
By default, the instance configuration is adjusted in the normal mode, which requires a data migration for the adjustment to complete after you adjust the instance configuration in the console. But if the physical machine where the instance is located has sufficient remaining resources (aka local resources), you can choose the QuickChange mode. The adjustment process is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/8e7702c81886573a459dbf73b2846701.png)
- **Normal mode**: to adjust the instance configuration, instance data needs to be migrated from the original physical machine to a new one. Because adjustment in this mode requires data migration, comparison, and verification, the overall adjustment process will take a long time in case of a huge amount of data. Besides, an instance switch may occur after the adjustment is completed.
- **QuickChange mode**: the instance configuration can be adjusted without migrating data or switching to another physical machine. As no migration preparation is needed, the overall adjustment process is much shorter.
>!
>- When the local resources are sufficient, you can enable the QuickChange mode by turning on the **QuickChange** toggle on the configuration adjustment page in the console.
>- In the QuickChange mode, the instance may be restarted and unavailable for a short time during configuration adjustment.

## Notes
- A read-only instance with an exclusive VIP enabled does not support QuickChange.
- If a read-only instance group (RO group) enables the "Remove Delayed RO Instances" feature, read-only instances whose delay exceeds the specified threshold will be removed from the RO group until the number of remaining ones reaches the allowed minimum number. If the number of the remaining available read-only instances in an RO group is less than or equal to the allowed minimum number, none of those instances will support QuickChange.
- If an RO group only has one read-only instance, the instance does not support QuickChange.

## [Configuration Adjustment Rules](id:guize)
- You can adjust the configuration of a TencentDB for MySQL instance and its associated read-only and disaster recovery instances only when they are in normal status (running) and are not executing any task.
- You cannot cancel a configuration adjustment operation in progress.
- The name, access IP, and access port of an instance will remain the same after configuration adjustment.
- During configuration adjustment, you should try to avoid such operations as modifying MySQL's global parameters and user password.
- Data migration may be involved in configuration adjustment. During data migration, the TencentDB for MySQL instance can be accessed normally and the business will not be affected.
- Instance switchover may be needed after configuration adjustment is completed (i.e., the MySQL instance may be disconnected for seconds). It is recommended that applications be configured with auto reconnection feature and that instance switchover be conducted during the instance maintenance period. For more information, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/236/10929).
- Basic single-node TencentDB for MySQL instances are unavailable for about 15 minutes in the process of configuration adjustment. We recommend that you adjust instance configuration during off-peak hours.

## Adjusting the Instance Configuration in the Console
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), locate the desired instance in the instance list, and select **More** > **Adjust Configurations** in the **Operation** column.
2. In the pop-up dialog box, select the desired configuration and click **Submit**.
>?
>- When the local resources are sufficient, you can enable the QuickChange mode by turning on the **QuickChange** toggle on the configuration adjustment page in the console.
>![](https://main.qcloudimg.com/raw/c37bb99f0a2db0a9108c7068ad72ba7c.png)
>- In some cases, instance restart is not required in the QuickChange mode and the configuration adjustment will take effect immediately after you submit the request, as shown below:
![](https://main.qcloudimg.com/raw/6f5e9ab54f270c0833f5545cccbc8c6d.png)
>
![](https://main.qcloudimg.com/raw/ef2bf519dabe88cb23b9c73993602b9b.png)

## Adjusting the Instance Configuration through the API
You can adjust the instance configuration using the `UpgradeDBInstance` API. For more information, please see [UpgradeDBInstance](https://intl.cloud.tencent.com/document/product/236/15876).

## FAQs
#### Will instance configuration adjustment affect instances?
- In the process of TencentDB for MySQL configuration adjustment, data migration may occur, and instances can still be accessed during the process. After the migration is completed, there is a switch which causes a short disconnection lasting for just seconds, please ensure that your business has a reconnection mechanism.
- Basic single-node TencentDB for MySQL instances are unavailable for about 15 minutes in the process of configuration adjustment. We recommend that you adjust instance configuration during off-peak hours.

#### Why can't my instance be downgraded?
It may be because the used storage capacity has reached the maximum capacity of the hard disk. To downgrade you instance, you need to clean up data first and make sure the remaining available capacity accounts for more than 20% of the total capacity or over 50 GB.

#### Why is my instance in the "Waiting for switch" status for a long time after I adjust instance configuration in the console?
It may be because you select **During maintenance time** as the **Switch Time** when you adjust instance configuration in the [console](https://console.cloud.tencent.com/cdb), so the instance will not be switched immediately after the adjustment.
To switch immediately, you can locate the desired instance in the instance list and click **Switch Now** in the **Operation** column. The switch causes a short disconnection lasting for just seconds. Please ensure that your business has a reconnection mechanism.

#### How long does it take to upgrade instance configuration?
The time it takes depends on the data volume the instance has and the read requests to replicate data.
Instances can still be accessed during the upgrade, but after the upgrade is completed, there is a VIP switch which causes a short disconnection lasting for just seconds.

#### How do I view the progress of instance configuration adjustment?
You can view the progress in [Task List](https://console.cloud.tencent.com/mysql/task) in the console.

#### What should I do if the disk space is being used up?
If over 85% disk space is used, we recommend that you delete data no longer used or expand disk space in the [console](https://console.cloud.tencent.com/cdb).

#### How do I know whether the QuickChange mode is supported when I adjust instance memory or disk capacity?
On the configuration adjustment page, if the QuickChange mode is supported, the **QuickChange** toggle can be turned on or off as needed; otherwise, the toggle cannot be used.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### Does expanding memory or disk capacity affect the kernel minor version of the instance?
If the kernel minor version of the instance is not the latest when memory or disk capacity is expanded, it will be upgraded to the latest. In this case, enabling the QuickChange mode will cause the database to restart.

#### Will enabling the QuickChange mode cause the instance to restart?
The instance needs to be restarted in some cases. A prompt whether to restart the instance will be displayed on the configuration adjustment page as shown below:
![](https://main.qcloudimg.com/raw/d97d2daa7cb8e5aa0924355c59bc4fc8.png)

>?If the kernel minor version of the instance is the latest, adjusting only the disk capacity in the QuickChange mode will not cause the instance to restart.

#### How do I know whether the QuickChange mode is enabled when I upgrade instance configuration in the console?
You can check the **QuickChange** toggle on the configuration adjustment page: if the toggle is turned on, the QuickChange mode is enabled; otherwise, the mode is disabled.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### How do I know whether the QuickChange mode is enabled when I use APIs to adjust instance configuration?
APIs do not support QuickChange for the time being, so instance configuration can be adjusted only by migrating data if you use APIs. APIs will support QuickChange in the future.

#### Will database parameters be modified during database configuration adjustment?
The `innodb_buffer_pool_size` parameter will be modified according to the configuration changes.

#### Will database parameters be modified during database configuration adjustment in the QuickChange mode?
It is the same with the normal mode. In the QuickChange mode, some parameters will be modified according to the configuration changes.

#### What is the difference between QuickChange mode and normal mode?
The QuickChange mode requires no data migration, so it takes less time to adjust instance configuration.
