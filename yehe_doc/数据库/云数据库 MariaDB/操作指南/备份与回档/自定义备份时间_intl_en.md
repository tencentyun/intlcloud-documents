TencentDB runs the backup policy you set to automatically back up the database.

1.Log in to the [MariaDB Console](https://console.cloud.tencent.com/mariadb) and click an instance ID or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Backup and Restore** > **Backup and Log Settings** and click the icon as shown below to set the storage period.
 - Backup Cycle: the backup task is performed every day by default.
 - Storage Period: the number of days for storing the data and log backup files, which is 30 days by default. It can be set to a value between 1 and 30 days. If you want to set it to above 30 days, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application. The maximum configurable value is 3,650 days.
 - Backup Execution Time: it can be set to any time period in hours.
 - Log Backup: it is enabled by default and cannot be disabled. Logs include error logs, slow logs, and transaction logs (binlogs).
![](https://main.qcloudimg.com/raw/40cfdbc1e0b7d23f265373213de2432f.png)
