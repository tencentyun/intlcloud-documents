
TencentDB for Redis supports automatic and manual backups.
>?To avoid impact on the business caused by overloading on the master database, the full data backup source of the newly created replica Redis database will be another replica database in the instance during data backup.
>
## Automatic Backup
Daily automatic backup is supported for instances in the following steps:
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** tab and click **Auto-Backup Settings**.
3. In the pop-up window, configure the backup start time and retention period and click **OK**.
>? 
>- All options are selected for **Backup Schedule** by default and cannot be modified.
>- Backup the retention time of the default 7 days, if you need to modify please [submit ticket](https://console.cloud.tencent.com/workorder/category).  
![](https://qcloudimg.tencent-cloud.cn/raw/ad9eac661c90d0132c92c5af08af16f4.png)
4. The backup will start in the specified time period. During a backup task, you can view its status in the Task Center. After it is completed, you can view the generated backup in **Backup and Restoration**.
>? Backup start may be delayed if affected by relevant processes.

## Manual Backup
On the instance details page, click **Manual Backup** in the top-right corner, edit the remarks, and click **OK**.

## Backup Download
>? Currently, you can only download backup files in Redis Standard Edition.
>
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** > **Backup List** tab and click **Download** in the **Operation** column.
3. In the pop-up window, copy the download address or click **Download** to download the backup file. Cross-AZ download is not supported.
>?Private network address and local download address are valid for 12 hours. You need to obtain them again upon expiration.
