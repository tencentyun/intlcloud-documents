
TencentDB for MariaDB runs the backup policy you set to automatically back up the database.

1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb) and click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. Select **Backup and Restoration** > **Backup and Log Settings** and click the icon as shown below to set the storage time.
 - Backup Cycle: The backup task is performed every day by default.
 - Storage Time: Data and log backups can be retained for 1 to 30 (default) days.
>?TencentDB for MariaDB's backup feature will be commercialized in June 2022. You will be able to set more backup and log storage days then.
 - Backup Execution Time: It can be set to any time period in hours.
 - Log Backup: It is enabled by default and cannot be disabled. Logs include error logs, slow logs, and transaction logs (binlogs).
![](https://main.qcloudimg.com/raw/40cfdbc1e0b7d23f265373213de2432f.png)
