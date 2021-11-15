TencentDB for SQL Server supports automatic backup, and you can adjust the backup cycle by configuring a backup policy. You can also manually back up data in TencentDB for SQL Server.

>!
>- Backup files are stored in a separate backup space and do not occupy the local disk space of the instance.
>- It is not recommended to perform DDL operations during the backup process, so as to avoid backup failure due to table locking.
>- You are recommended to back up your data during off-peak hours.
>- If the data volume is high, backup may take a long time.

## Backup Objects
| **Data Backup** | **Log Backup** |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| <li>Currently, full backup is supported. <li>Regular backup (once per day) and manual backup are supported. <li>Multi-database backup is supported, that is, you can back up one or more databases in the instance. <li>Instance backup is supported, that is, you can back up all databases in the entire instance (this mode is used for scheduled backup). <li>A backup file has a retention period (seven days) and will be automatically deleted upon expiration. Please download it in time for local storage. <li>Backup files currently cannot be deleted manually. | <li>Transaction log backup is supported. <li>Logs are backed up once every 30 minutes and uploaded to the cloud for storage. <li>Log files currently cannot be downloaded.</li> |

## Setting Manual Backup
>?Before performing manual backup, please make sure that you have created a database. For more information, please see [Creating Database](https://intl.cloud.tencent.com/document/product/238/35780).
>
You can manually create backup files through instance backup or multi-database backup at any time in the following steps:
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Backup Management** tab, click **Manual Backup**.
3. In the pop-up dialog box, enter the backup name and select the backup policy.
  - Backup name: enter the name of the manual backup.
  - Backup policy: instance backup (i.e., backing up all databases in the entire instance) or multi-database backup. If you select the latter, you need to select the databases to be backed up.
![](https://main.qcloudimg.com/raw/f33a17aca57a83cb9bbaf262f73d798e.png )

## Setting Scheduled Backup
You can set a scheduled backup time to implement daily automatic database backup in the following steps:
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Backup Management** tab, click **Auto-Backup Settings**, set the scheduled backup time, and click **Save**.
![](https://main.qcloudimg.com/raw/a9fd8e162a02ec7c11c75b9520d3956c.png)

## Setting Backup Tasks
Backup task settings include global variables of manual and scheduled backup, such as the backup file format and backup task execution option.
- Backup file format: you can specify the format of backup files. By default, backup files (i.e., .bak files) will be archived into a .tar file and then uploaded to COS. If you select "unarchived files" as the backup file format, the .bak file of each database in the instance will be directly uploaded to COS without being archived.
- Backup task execution option: you can decide whether to back up at the primary node or the replica node. By default, data is backed up at the primary node.

>?Only cluster edition 2017/2019 instances support the backup task execution option.

1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Backup Management** tab, click **Backup Task Settings**.
3. Specify configuration items in the pop-up dialog box and click **Save**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/38947de70c67afe4abf614d6aef0b78e.png" style="zoom:50%;" />

## Viewing Backup Tasks
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Backup Management** tab, view backup tasks in the backup list.
 - If the backup file is an archive file, the backup information is directly displayed in the backup list, including backup start time, backup end time, backup name, backup policy, backup mode, backup size, database, status, and operations (download, restoration, and deletion).</span>
![](https://main.qcloudimg.com/raw/db076dda070a0a3819c547168d53449a.png)
 - If the backup files are unarchived files, the backup information is displayed in two nested lists. The outer list displays the backup information of the whole instance, including backup start time, backup end time, backup name, backup policy, backup mode, database, and status. The inner list displays the backup information of each database in the instance, including database name, backup size, and operations (download, restoration, and deletion).</span>
![](https://qcloudimg.tencent-cloud.cn/raw/d79de61562248cbee2d73bf71c5385a8.png)

