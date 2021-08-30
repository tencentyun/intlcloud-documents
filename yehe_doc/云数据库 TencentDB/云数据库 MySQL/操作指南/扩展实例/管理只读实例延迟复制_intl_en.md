This document describes how to set delayed read-only instance replication and enable/disable replication in the TencentDB for MySQL console. You can set delayed replication (i.e., delay between a read-only instance and its source instance) and select to replay by flashbacked position or global transaction identifier (GTID) during the delay to efficiently roll back data and fix failures.
- Delayed Replication: you can set the time of delayed replication between a read-only instance and its source instance.
- Enabling/Disabling Replication: you can manually enable or disable data sync between a read-only instance and its source instance.

## Delayed Replication Description
- After delayed replication is enabled for a read-only instance, it will be removed from the RO group with its weight set to 0, and a removal alarm will be triggered. At this point, if you access the removed instance with the VIP address of the RO group, the traffic will not be forwarded to it, and you can only use its own VIP address for access.
- If delayed read-only instance removal is enabled in an RO group and delayed replication is disabled for a read-only instance, only if the delay time of the instance is less than the delay threshold of the RO group will the weight of the instance be recovered, and a restoration alarm will be triggered at the same time.
- During replay by flashbacked position, you cannot restart the instance, adjust its configuration, upgrade its version, or upgrade its kernel minor version.

## Enabling Delayed Replication
>?**Delayed Replication** is **disabled** for a read-only instance by default. If it is enabled, the delayed replication time will be displayed.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. Click **Enable** next to **Delayed Replication** on the instance details page.
![](https://main.qcloudimg.com/raw/23a113ccd7251b379c8de124f0f945d1.png)
3. In the pop-up window, set the delay and click **OK**.
>?The delay ranges from 1 to 259,200 (3,600 * 24 * 3) seconds.

## Modifying Delayed Replication
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click an instance ID in the instance list to enter the instance details page.
2. Click **Modify** next to **Delayed Replication** on the instance details page.
![](https://main.qcloudimg.com/raw/83288194d58e25b6a3bd84f950a2ae5a.pngg)
3. In the pop-up window, set the delay and click **OK**.
![](https://main.qcloudimg.com/raw/40045317eb248fbfdb8b507bea550bdf.png)

## Disabling Delayed Replication
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click an instance ID in the instance list to enter the instance details page.
2. Click **Disable** next to **Delayed Replication** on the instance details page.
3. In the pop-up window, confirm that everything is correct and click **OK**.
>?If delayed replication is disabled, the delayed replication time will be 0 seconds, that is, real-time data sync is resumed between the read-only instance and its source instance. 
> 

## Enabling Data Replication
>?The **Replication Status** of a read-only instance is **Normal** by default. If you set delayed replication and delete data accidentally during the delayed replication time period, you can restore the read-only instance to the specified position or GTID of the binlog file to implement quick data restoration.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click an instance ID in the instance list to enter the instance details page.
2. Click **Enable** next to **Replication Status** at the bottom of the instance details page.
![](https://main.qcloudimg.com/raw/83288194d58e25b6a3bd84f950a2ae5a.png)
3. In the pop-up window, set the configuration items such as start mode and click **OK**.
 - **Replicate All**: once the replication is enabled, the data sync between the read-only instance and the source instance will resume.
 - **Replay by Flashbacked Position**: data can be restored to the specified time point or corresponding GTID. After the restoration, replication of the read-only instance will be disabled until the start mode is switched to **Replicate all**.
    - Time: you can select a time point between the replication end time and the current time of the source instance.
    - GTID: you can select all logs after the binlog not applied. The length of instance `server_uuid` is fixed at 36 bits, and the GTID must be in `server_uuid::transaction_id` format.
   >!
   >- If the entered binlog position has already been applied on the read-only instance or is after the source instance position, replication will fail to be enabled.
   >- When you enable replication, if there is any breakpoint in the binlog, replication will fail to be enabled.
   >- To avoid overusing the disk space of a delayed read-only instance when replication is disabled for it, the I/O thread of the read-only instance will be paused when its available disk space drops below 5 GB.
   > 
![](https://main.qcloudimg.com/raw/2422edcaa53a5cc50089f5c3748eef28.png)

## Disable Data Replication
>?
>- Only after delayed replication is enabled can it be disabled; otherwise, the **Disable** button is grayed out.
>- Once replication is disabled, I/O and SQL threads will also be ended.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click an instance ID in the instance list to enter the instance details page.
2. Click **Disable** next to **Replication Status** at the bottom of the instance details page.
![](https://main.qcloudimg.com/raw/8921d228b70bf42ca5120d6fcf44e92c.png)
3. In the pop-up window, confirm that everything is correct and click **OK**.

## FAQs
#### How do I get the GTID?
We recommend you run the `flush log` command to get the binlog file to locate the position and GTID of the maloperation.

#### How do I view the delay?
You can view the delay between a read-only instance and its source instance on the instance details page in the [console](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/0b975dfca0c575735b94445f11e30d67.png)

#### How do I view the task information of replay by flashbacked position?
You can view the task progress and details on the task list page in the [console](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/f3c0cb3ed4d9488c66fc02cbd96b770d.png)

