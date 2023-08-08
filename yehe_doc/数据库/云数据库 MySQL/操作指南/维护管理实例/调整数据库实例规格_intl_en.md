TencentDB for MySQL supports flexible scaling that allows you to quickly adjust instance specification in the console. You can do so at any time (at the start, during rapid development, or during peak/off-peak hours), so you can get the most out of your resources and reduce unnecessary costs in real time. For more information, see [Instance Adjustment Fee](https://intl.cloud.tencent.com/document/product/236/32345).

## Instance Disk Space Description
- To ensure business continuity, upgrade your instance specifications or purchase additional disk capacity in time before disk capacity is used up.
>?You can view disk space on the instance details page in the [MySQL console](https://console.cloud.tencent.com/cdb), or receive disk alarms by configuring [Alarm Policies (TCOP)(https://intl.cloud.tencent.com/document/product/236/8457).
- When the size of the data stored on an instance exceeds its capacity limit, the instance will be locked and become read-only. You will not be able to write data to it. You will need to expand its capacity or delete some database tables in the console to unlock it.
- To avoid the database from triggering the lock status repeatedly, a locked instance will be unlocked and allowed for reads and writes only when its remaining available capacity is more than 20% of its total capacity or over 50 GB.

## Configuration Adjustment Description
By default, the instance configuration is adjusted in the normal mode, which requires a data migration for the adjustment to complete after you adjust the instance configuration in the console. But if the physical machine where the instance is located has sufficient remaining resources (aka local resources), you can choose the QuickChange mode. The adjustment process is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/8e7702c81886573a459dbf73b2846701.png)

- **Normal mode**: to adjust the instance configuration, instance data needs to be migrated from the original physical machine to a new one. Because adjustment in this mode requires data migration, comparison, and verification, the overall adjustment process will take a long time in case of a huge amount of data. Besides, an instance switch may occur after the adjustment is completed.
- **QuickChange mode**: the instance configuration can be adjusted without migrating data or switching to another physical machine. As no migration preparation is needed, the overall adjustment process is much shorter.
>! If the local resources are sufficient and meet the conditions of the QuickChange mode, this mode will be used by default. If you don't need to use it, you can disable it by toggling it off on the configuration adjustment page.


## Use Limits
- A read-only instance with an exclusive VIP enabled does not support QuickChange.
- If a read-only instance group (RO group) enables the "Remove Delayed RO Instances" feature, read-only instances whose delay exceeds the specified threshold will be removed from the RO group until the number of remaining ones reaches the allowed minimum number. If the number of the remaining available read-only instances in an RO group is less than or equal to the allowed minimum number, none of those instances will support QuickChange.
- If an RO group only has one read-only instance, the instance does not support QuickChange.
- If the kernel minor version of the instance is not the latest when the configuration is adjusted, it will be upgraded to the latest. In this case, whether instance restart is required will be as prompted on the **QuickChange** page.

## [Configuration Adjustment Rules](id:guize)
- You can adjust the configuration of a TencentDB for MySQL instance and its associated read-only and disaster recovery instances only when they are in normal status (running) and are not executing any task.
- You cannot cancel a configuration adjustment operation in progress.
- The name, access IP, and access port of the instance remain unchanged after configuration adjustment.
- During configuration adjustment, you should try to avoid such operations as modifying MySQL's global parameters and user password.
- Data migration may be involved in configuration adjustment. During data migration, the TencentDB for MySQL instance can be accessed normally and the business will not be affected.
- Instance switchover may be needed after configuration adjustment is completed (i.e., the MySQL instance may be disconnected for seconds). It is recommended that applications be configured with auto reconnection feature and that instance switchover be conducted during the instance maintenance period. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
- Basic single-node TencentDB for MySQL instances are unavailable for about 15 minutes in the process of configuration adjustment. We recommend you adjust instance configuration during off-peak hours.

## Instance Specification and Storage Table
### Two-node/Three-node (local SSD disk)
<table class="table-striped">
<tbody>
<tr><th>Isolation Policy</th><th>CPU and Memory</th><th>Maximum IOPS</th><th>Storage Space</th></tr>
<tr>
<td rowspan="14">General</td>
<td>1-core 1000 MB MEM</td><td>1200</td><td rowspan="4">25–3000 GB</td></tr>        
<tr>
<td>1-core 2000 MB MEM</td><td>2000</td></tr>
<tr>
<td>2-core 4000 MB MEM</td><td>4000</td></tr>
<tr>
<td>4-core 8000 MB MEM</td><td>8000</td></tr>
<tr>
<td>4-core 16000 MB MEM</td><td>14000</td><td rowspan="6">25–4000 GB</td></tr>
<tr>
<td>8-core 16000 MB MEM</td><td>20000</td></tr>
<tr>
<td>8-core 32000 MB MEM</td><td>28000</td></tr>
<tr>
<td>16-core 32000 MB MEM</td><td>32000</td></tr>
<tr>
<td>16-core 64000 MB MEM</td><td>40000</td></tr>
<tr>
<td>16-core 96000 MB MEM</td><td>40000</td></tr>
<tr>
<td>16-core 128000 MB MEM</td><td>40000</td><td rowspan="3">25–8000 GB</td></tr>
<tr>
<td>24-core 244000 MB MEM</td><td>60000</td></tr>
<tr>
<td>32-core 256000 MB MEM</td><td>80000</td></tr>
<tr>
<td>48-core 488000 MB MEM</td><td>120000</td><td rowspan="1">25–12000 GB</td></tr>
<tr>
<td rowspan="26">Dedicated</td>
<td>2-core 16000 MB MEM</td><td>8000</td><td rowspan="7">25–3000 GB</td></tr>        
<tr>
<td>4-core 16000 MB MEM</td><td>10000</td></tr>
<tr>
<td>4-core 24000 MB MEM</td><td>13000</td></tr>
<tr>
<td>4-core 32000 MB MEM</td><td>16000</td></tr>
<tr>
<td>8-core 32000 MB MEM</td><td>32000</td></tr>
<tr>
<td>8-core 48000 MB MEM</td><td>36000</td></tr>
<tr>
<td>8-core 64000 MB MEM</td><td>40000</td></tr>
<tr>
<td>12-core 48000 MB MEM</td><td>36000</td><td rowspan="15">25–4000 GB</td></tr>
<tr>
<td>16-core 64000 MB MEM</td><td>60000</td></tr>
<tr>
<td>12-core 72000 MB MEM</td><td>40000</td></tr>
<tr>
<td>12-core 96000 MB MEM</td><td>48000</td></tr>
<tr>
<td>16-core 96000 MB MEM</td><td>60000</td></tr>
<tr>
<td>24-core 96000 MB MEM</td><td>72000</td></tr>
<tr>
<td>16-core 128000 MB MEM</td><td>60000</td></tr>
<tr>
<td>32-core 128000 MB MEM</td><td>80000</td></tr>
<tr>
<td>24-core 144000 MB MEM</td><td>76000</td></tr>
<tr>
<td>24-core 192000 MB MEM</td><td>80000</td></tr>
<tr>
<td>32-core 192000 MB MEM</td><td>90000</td></tr>
<tr>
<td>48-core 192000 MB MEM</td><td>120000</td></tr>
<tr>
<td>32-core 256000 MB MEM</td><td>100000</td></tr>
<tr>
<td>48-core 288000 MB MEM</td><td>140000</td></tr>
<tr>
<td>48-core 384000 MB MEM</td><td>140000</td></tr>
<tr>
<td>64-core 256000 MB MEM</td><td>150000</td><td rowspan="2">25–9000 GB</td></tr>
<tr>
<td>64-core 384000 MB MEM</td><td>150000</td></tr>
<tr>
<td>64-core 512000 MB MEM</td><td>150000</td><td rowspan="2">25–12000 GB</td></tr>
<tr>
<td>90-core 720000 MB MEM</td><td>150000</td></tr>
</tbody></table>        

>?The storage space cap of an instance specification may vary by region as displayed on the purchase page.

## Adjusting Instance Configuration in the Console
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), locate the desired instance in the instance list, and select **More** > **Adjust Configurations** in the **Operation** column.
2. In the pop-up window, select the desired configuration and click **Submit**.
>?
>- When the local resources are sufficient, you can enable the QuickChange mode by turning on the **QuickChange** toggle on the configuration adjustment page in the console.
>![](https://main.qcloudimg.com/raw/c37bb99f0a2db0a9108c7068ad72ba7c.png)
>- In some cases, instance restart is not required in the QuickChange mode and the configuration adjustment will take effect immediately after you submit the request, as shown below:
![](https://main.qcloudimg.com/raw/6f5e9ab54f270c0833f5545cccbc8c6d.png)
>
![](https://qcloudimg.tencent-cloud.cn/raw/b73de2f9742e3cc7b2d9296082d72f81.png)

## Adjusting Instance Configuration Through API
You can adjust the instance configuration using the `UpgradeDBInstance` API. For more information, see [UpgradeDBInstance](https://intl.cloud.tencent.com/document/product/236/15876).

## FAQs
#### Will instance configuration adjustment affect instances?
- In the process of TencentDB for MySQL configuration adjustment, data migration may occur, and instances can still be accessed during the process. After the migration is completed, there is a switch which causes a short disconnection lasting for just seconds, ensure that your business has a reconnection mechanism.
- Basic single-node TencentDB for MySQL instances are unavailable for about 15 minutes in the process of configuration adjustment. We recommend you adjust instance configuration during off-peak hours.

#### Why can't my instance be downgraded?
It may be because the used storage capacity has reached the maximum capacity of the hard disk. To downgrade you instance, you need to clean up data first and make sure the remaining available capacity accounts for more than 20% of the total capacity or over 50 GB.

#### Why is my instance in the "Waiting for switch" status for a long time after I adjust instance configuration in the console?
It may be because you select **During maintenance time** as the **Switch Time** when you adjust instance configuration in the [console](https://console.cloud.tencent.com/cdb), so the instance will not be switched immediately after the adjustment.
To switch immediately, find the target instance in the instance list and click **Switch Now** in the **Operation** column. The switch will cause a momentary disconnection. Make sure that your business has a reconnection mechanism.

#### How long does it take to upgrade instance configuration?
The time it takes depends on the instance's data volume and data replication speed.
Instances can still be accessed during the upgrade, but after the upgrade is completed, there is a VIP switch which causes a short disconnection lasting for just seconds.

#### How do I view the progress of instance configuration adjustment?
You can view the progress in [Task List](https://console.cloud.tencent.com/mysql/task) in the console.

#### What should I do if the disk space is being used up?
If over 85% disk space is used, we recommend that you delete data no longer used or expand disk space in the [console](https://console.cloud.tencent.com/cdb) by selecting **More** > **Adjust Configurations** in the **Operation** column on the right of the instance list.

#### How do I know whether the QuickChange mode is supported when I adjust instance memory or disk capacity?
On the configuration adjustment page, if the QuickChange mode is supported, the **QuickChange** toggle can be turned on or off as needed; otherwise, the toggle cannot be used.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### Does expanding memory or disk capacity affect the kernel minor version of the instance?
If the kernel minor version of the instance is not the latest when memory or disk capacity is expanded, it will be upgraded to the latest. In this case, enabling the QuickChange mode will cause the database to restart.

#### Will the instance restart if the QuickChange mode is enabled?
The instance needs to be restarted in some cases. A prompt will appear asking if you want to restart the instance on the configuration adjustment page.
![](https://main.qcloudimg.com/raw/d97d2daa7cb8e5aa0924355c59bc4fc8.png)

>?If the instance is running the latest kernel minor version, it won’t restart if you only adjust the disk capacity in the QuickChange mode.

#### How do I know whether the QuickChange mode is enabled when I upgrade instance configuration in the console?
You can check the **QuickChange** switch on the configuration adjustment page: if the switch is toggled on, the QuickChange mode is enabled; otherwise, the mode is disabled.
![](https://main.qcloudimg.com/raw/0ecdc6d86e3727e7a688a559ce217d7d.png)

#### How do I know whether the QuickChange mode is enabled when I use APIs to adjust instance configuration?
APIs do not support QuickChange for the time being, so instance configuration can be adjusted only by migrating data if you use APIs. APIs will support QuickChange in the future.

#### Will database parameters be modified during database configuration adjustment?
The `innodb_buffer_pool_size` parameter will be modified according to the configuration changes.

#### Will database parameters be modified during database configuration adjustment in the QuickChange mode?
It is the same with the normal mode. In the QuickChange mode, some parameters will be modified according to the configuration changes.

#### What is the difference between QuickChange mode and normal mode?
The QuickChange mode requires no data migration, so it takes less time to adjust instance configuration.

