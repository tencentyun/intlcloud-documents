
TencentDB for Redis supports automatic and manual backups.
>?To avoid impact on the business caused by overloading on the master database, the full data backup source of the newly created replica Redis database will be another replica database in the instance during data backup.
>
## Automatic Backup
Daily automatic backup is supported for instances in the following steps:
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** tab and click **Auto-Backup Settings**.
3. In the pop-up window, configure the backup start time and retention period and click **OK**.
>?
> All options are selected for **Backup Cycle** by default and cannot be modified.
>- The backup retention period is 7 days by default. To change it, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/ad9eac661c90d0132c92c5af08af16f4.png" style="zoom:60%;" />
4. The backup will start in the specified time period. During a backup task, you can view its status as needed. After it is completed, you can view the generated backup in **Backup and Restoration**.
>? Backup start may be delayed if affected by relevant processes.

## Manual Backup
On the instance details page, click **Manual Backup** in the top-right corner, edit the remarks, and click **OK**.

## Download a Backup
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** > **Backup List** tab and click **Download** in the **Operation** column.
3. In the pop-up window, copy the download address or click **Download** to download the backup file. Cross-AZ download is not supported.
 - Download backup shard: Download the shard node information of the backup files which is in the format of `instance ID-node-shard ID`. The shard IDs are sequenced from 0.
 - Download from private network: Click **Copy download URL**, copy the private network address, and download backup files via private network.
 - Download from public network: Click **Copy download URL**, copy the public network address, and download backup files via public network; click **Download** to download the backup file to view.
>? The private network address and local download address are valid for 6 hours. Generate new ones after their expiration.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/b6e96ffca354615ec58cc0863315b897.png" style="zoom:50%;" />

## Related APIs

| API | Description |
|---------|---------|
| [ManualBackupInstance](https://intl.cloud.tencent.com/document/product/239/32073) | Backs up an instance |
