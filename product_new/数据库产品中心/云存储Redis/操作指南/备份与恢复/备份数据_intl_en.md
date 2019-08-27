TencentDB for Redis supports automatic and manual backups.

## Automatic Backup
Daily automatic backup is supported for instances in the following steps:
1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis) and click an instance name in the instance list to enter the instance details page.
2. Select **Backup and Restore** > **Auto Backup Settings** and click **Edit**.
3. Set the time period for the backup to start and click **Save**.
> All options are selected for Backup Cycle by default and cannot be modified.
>
![](https://main.qcloudimg.com/raw/02813e57aa17fab2c5db77a3922469b0.png)
4. The backup will start in the specified time period. During a backup task, you can view its status in the Task Center. After it is completed, you can view the generated backup in **Backup and Restore**.
> Backup start may be delayed if affected by relevant processes.


## Manual Backup
On the instance details page, click **Manual Backup** in the top-right corner, edit the remarks, and click **OK**.
![](https://main.qcloudimg.com/raw/5997f5e0d5afc8e6b917817faa9df7ed.png)


## Download a Backup
> Currently, you can only download backup files in Redis Standard Edition.

1. On the instance details page, select **Backup and Restore**, and click **Download** in the **Operation** column.
2. In the pop-up window, copy the private network address or click **Download** to download the backup file. Cross-AZ download is not supported.
>The private network address and local download address are valid for 12 hours. Please generate new ones after their expiration.