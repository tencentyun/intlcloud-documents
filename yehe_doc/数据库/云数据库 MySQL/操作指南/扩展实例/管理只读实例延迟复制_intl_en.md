This document describes how to set delayed replication for read-only instances and enable/disable replication in the TencentDB for MySQL console. You can set delayed replication (i.e., delay between a read-only instance and its source instance) and select to replay by flashbacked position or global transaction identifier (GTID) during the delay to efficiently roll back data and fix failures.
- Delayed Replication: you can enable and configure the replication delay between a read-only instance and its source instance on its RO group configuration page or management page.
- Enabling/Disabling Replication: you can manually enable or disable data sync between a read-only instance and its source instance.

## Delayed Replication Description
- After delayed replication is enabled for a read-only instance, it will be removed from the RO group with its weight set to 0, and a removal alarm will be triggered. At this point, the traffic will not be forwarded to the removed instance if the RO VIP is used to access the RO group. What's more, the removed instance can only be accessed via the instance's VIP.
- After the delayed replication is disabled for a read-only instance ( the corresponding RO group has enabled delayed-replication-read-only-instance removal), the weight of this read-only instance in the RO group will be recovered only if the delay time of this instance is less than the delay threshold of the RO group.  And a restoration alarm will be triggered at the same time.
- During replay by flashbacked position, you cannot restart the instance, adjust its configuration, upgrade its version, or upgrade its kernel minor version.

## Enabling Delayed Replication
>?**Delayed Replication** is **disabled** for a read-only instance by default. If it is enabled, the delayed replication time will be displayed.

### Enabling on the read-only instance's RO group configuration page
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click a source instance ID to enter the instance management page.
2. On the instance management page, select the **Read-Only Instance** tab, locate the desired RO group, and click **Configuration** to enter the RO group configuration page.
![](https://qcloudimg.tencent-cloud.cn/raw/87041c7addd9dcfd058b2d3f7c417625.png)
3. On the RO group configuration page, enable **Delayed Replication**, set the **Replication Delay**, and click **OK**.
   You can set delayed replication and select to replay by flashbacked position or global transaction identifier (GTID) during the delay to efficiently roll back data and fix failures.
   - **Replication Delay**: You can configure the time of delayed replication between a read-only instance and its source instance. The value range is 1–259200 seconds.
   - **Remove Delayed RO Instances**: This option indicates whether to enable the removal policy. If a read-only instance is removed when its delay exceeds the threshold, its weight will be set to 0 automatically, and alarms will be sent (for more information on how to configure the read-only instance removal alarm and recipients, see [Alarm Policies (TCOP)](https://intl.cloud.tencent.com/document/product/236/8457)).
   - **Delay Threshold**: This sets a delay threshold for the read-only instance. When the threshold is exceeded, the instance will be removed from the read-only group.
   - **Least RO Instances**: This is the minimum number of instances that should be retained in the RO group. When there are fewer instances in the RO group, even if an instance exceeds the delay threshold, it will not be removed.
   - **Assign Read Weight**: The RO group supports two weight assignment methods: automatic assignment by the system and custom assignment. The weight value must be an integer between 0 and 100.
   - **Load Rebalancing**:
    - Modifying weight will only affect new loads if rebalancing is disabled. The operation has no impact on read-only instances accessed by existing persistent connections and does not cause momentary database disconnection.
    - If rebalancing is enabled, all connections to the database will be temporarily disconnected, and the loads of newly added connections will be balanced according to the set weights.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c40a92c3a6dcc083ac92f01169b259ff.png"  style="zoom:50%;">

### Enabling on the read-only instance management page
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click a read-only instance ID or **Manage** in the **Operation** column to access the read-only instance details page.
2. On the read-only instance details page, click **Enable** in **Deployment Info** > **Delayed Replication**.
![](https://qcloudimg.tencent-cloud.cn/raw/280f08c04f692445f51b1ab4aa556f58.png)
3. In the pop-up window, set the delay and click **OK**.
>?The delay ranges from 1 to 259,200 seconds.
>Read-Only instances in the same RO group share the same replication delay. If one instance is modified, the rest will be modified automatically at the same time.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/32877ca9c8ab4bb3030bbb508c899374.png"  style="zoom:80%;">

## Modifying Delayed Replication
### Modifying on the read-only instance's RO group configuration page
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click a source instance ID to enter the instance management page.
2. On the instance management page, select the **Read-Only Instance** tab, locate the desired RO group, and click **Configuration** to enter the RO group configuration page.
3. On the RO group configuration page, modify **Replication Delay** and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/437d781e478652416c166449b4420910.png"  style="zoom:60%;">

### Modifying on the read-only instance management page
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click a read-only instance ID in the instance list to enter the read-only instance details page.
2. On the read-only instance details page, click **Modify** in **Deployment Info** > **Delayed Replication**.  

<img src="https://qcloudimg.tencent-cloud.cn/raw/f9b0fffd50ddfb2f2d4819860be9aef0.png"  style="zoom:80%;">
3. In the pop-up window, set the delay and click **OK**.

## Disabling Delayed Replication
### Disabling on the read-only instance's RO group configuration page
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/). In the instance list, click a source instance ID to enter the instance management page.
2. On the instance management page, select the **Read-Only Instance** tab, locate the desired RO group, and click **Configuration** to enter the RO group configuration page.
3. On the RO group configuration page, click **Delayed Replication** and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9191e1c61694da2970323b59a21c59f3.png"  style="zoom:70%;">

### Disabling on the read-only instance management page
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click a read-only instance ID in the instance list to enter the read-only instance details page.
2. On the read-only instance details page, click **Disable** in **Deployment Info** > **Delayed Replication**.

<img src="https://qcloudimg.tencent-cloud.cn/raw/ae3a4a7f40ee28f4d5ad032f68c8a5a2.png"  style="zoom:80%;">
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.
>?If delayed replication is disabled, the delayed replication time will be 0 seconds, that is, real-time data sync is resumed between the read-only instance and its source instance. > 

## Enabling Data Replication
>?The **Replication Status** of a read-only instance is **Normal** by default. If you set delayed replication and delete data accidentally during the delayed replication time period, you can restore the read-only instance to the specified position or GTID of the binlog file to implement quick data restoration.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click a read-only instance ID in the instance list to enter the read-only instance details page.
2. On the read-only instance details page, click **Enable** in **Deployment Info** > **Replication Status**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e6bcd6a0ae7cd0c82cf23da4f10144a7.png"  style="zoom:80%;">
3. In the pop-up window, click **OK**.
>? Once the replication is enabled, the data sync between the read-only instance and the source instance will resume.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/ab58491f328ffe447f8790105699f13b.png"  style="zoom:80%;">
4. You can also select **Replay by Flashbacked Position** in **Deployment Info** > **Operation**. Then, data can be restored to the specified time point or corresponding GTID. After the restoration, replication of the read-only instance will be disabled until the start mode is switched to **Replicate all**.
    - Time: You can select a time point between the replication end time and the current time of the source instance.
    - GTID: You can select all logs after the unapplied binlog. If GTID is selected, data will be replicated until the specified GTID is reached.
The length of instance `server_uuid` is fixed at 36 bits, and the GTID must be in `server_uuid:transaction_id` format.
>!
>- If the entered binlog position has already been applied on the read-only instance or is after the source instance position, replication will fail to be enabled.
>- When you enable replication, if there is any breakpoint in the binlog, replication will fail to be enabled.
>- To avoid overusing the disk space of a delayed read-only instance when replication is disabled for it, the I/O thread of the read-only instance will be paused when its available disk space drops below 5 GB.
> 
<img src="https://qcloudimg.tencent-cloud.cn/raw/92671ad35d5ef5acbfdf3bfbb47f967a.png"  style="zoom:85%;">
5. During the process of replay by flashbacked position, you can click **Replaying** after **Replication Status** to query and refresh the task details.  

<img src="https://qcloudimg.tencent-cloud.cn/raw/39274c3aa8e92e6c4dfe0a242de0392e.png"  style="zoom:85%;">
6. After the replication is completed, click **Enable** after **Replication Status**, and the read-only instance can continue to replicate.  

<img src="https://qcloudimg.tencent-cloud.cn/raw/b27f75181ebae1e8c9b833762ba9388d.png"  style="zoom:85%;">


## Disabling Data Replication
>?
>- Only after delayed replication is enabled can it be disabled; otherwise, the **Disable** button is grayed out.
>- Once replication is disabled, I/O and SQL threads will also be ended.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click a read-only instance ID in the instance list to enter the read-only instance details page.
2. On the read-only instance details page, click **Disable** in **Deployment Info** > **Replication Status**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/6b1570566d533f93306256cf41113fc5.png"  style="zoom:85%;">
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.

## FAQs
#### How do I get the GTID?
We recommend you run the `flush log` command to get the binlog file to locate the position and GTID of the maloperation.

#### How do I view the delay?
You can view the delay between a read-only instance and its source instance on the instance details page in the [console](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/0b975dfca0c575735b94445f11e30d67.png)

#### How do I view the task information of replay by flashbacked position?
You can view the task progress and details on the task list page in the [console](https://console.cloud.tencent.com/mysql/task).


