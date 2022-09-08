TencentDB for MariaDB supports full backup and incremental backup, and backups are compressed with LZ4. For more information on how to use LZ4, see [Decompressing Backups and Logs](https://intl.cloud.tencent.com/document/product/237/2088).

## Backup Type
#### Full backup
You can set the backup retention period and backup execution time for full backups, which is set to seven days by default (30 days for finance cloud).

#### Incremental backup
Incremental backup is implemented based on binlogs, which are generated in real time. The binlogs occupy some disk space and are periodically uploaded to the TencentDB backup system.

## Custom Backup Time
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb).Click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2, Click **Backup and Restoration** in the instance management page
3. On **Backup and Restoration** > **Backup and Log Settings** page, you can set the storage period and backup execution time.
 - Storage time: Data and log backups can be retained for 1 to 365 days. Default value: 7 days.
 - Backup execution time: It can be set to any time period in hours.
>? Log backup is enabled by default and cannot be disabled. Logs include error logs, slow logs, and transaction logs (binlogs).
>
![](https://main.qcloudimg.com/raw/40cfdbc1e0b7d23f265373213de2432f.png)
