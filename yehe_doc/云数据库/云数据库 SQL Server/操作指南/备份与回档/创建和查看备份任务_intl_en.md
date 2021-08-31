TencentDB for SQL Server supports automatic backup, and you can adjust the backup cycle by configuring a backup policy. You can also manually back up data in TencentDB for SQL Server.

>!
>- Backup files are stored in a separate backup space and do not occupy the local disk space of the instance.
>- Do not perform DDL operations during the backup process so as to avoid backup failure due to table locking.
>- Try to back up your data during off-peak hours.
>- If the data volume is high, backup may take a long time. Please wait patiently.

**Backup objects**

| **Data Backup** | **Log Backup** |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <li>Currently, full backup is supported. <li>Scheduled backup (once per day) and manual backup are supported. <li>Multi-Database backup is supported, that is, you can specify to back up one or multiple databases on the instance. <li>Instance backup is supported, that is, you can back up all databases on the entire instance (this mode is used for scheduled backup). <li>A backup file has a retention period (7 days) and will be automatically deleted upon expiration. Please download it in time for local storage. <li>Backup files currently cannot be deleted manually. | <li>Transaction log backup is currently supported. <li>Logs are backed up once every 30 minutes and uploaded to the cloud storage. <li>Log files currently cannot be downloaded. |

 

## Setting Scheduled Backup
You can set a scheduled backup time to implement daily automatic database backup in the following steps:
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Manage Backup** > **Backup Settings**, click **Edit**, select the time period for scheduled backup, and click **Save**.
![](https://main.qcloudimg.com/raw/a9fd8e162a02ec7c11c75b9520d3956c.png)


## Setting Manual Backup
>?Before performing manual backup, please make sure that you have created a database. For more information, please see [Creating Database](https://intl.cloud.tencent.com/document/product/238/35780).
>
You can manually create backup files through instance backup or multi-database backup at any time in the following steps:
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Manage Backup** > **Backup List** and click **Create Backup**.
3. Select a backup policy: instance backup (i.e., backing up all databases on the entire instance) or multi-database backup. If you select the latter, you need to select the databases to be backed up and click **OK**.
![](https://main.qcloudimg.com/raw/f33a17aca57a83cb9bbaf262f73d798e.png)

## Viewing Backup Task
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Manage Backup** > **Backup List** to view the creation time, status, file size, and policy of the backup task.
![](https://main.qcloudimg.com/raw/db076dda070a0a3819c547168d53449a.png)

