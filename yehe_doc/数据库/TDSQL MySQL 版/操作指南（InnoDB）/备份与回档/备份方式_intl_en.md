
TDSQL for MySQL supports full backup and incremental backup.

## Backup Type
### Full backup
You can set the backup retention period for full backups, which is set to seven days by default.

### Incremental backup
Incremental backup is implemented based on binlogs, which are generated in real time. The binlogs occupy some disk space and are periodically uploaded to the TencentDB backup system.

## Custom Backup Time
1. Log in to the [TencentDB for MySQL console] (https://console.cloud.tencent.com/cdb). Click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. Click **Backup and Restoration** in the instance management page
3. Select **Backup and Restoration** > **Backup and Log Settings** to set the storage period and backup execution time.
 - Storage time: Data and log backups can be retained for 1 to 365 days. Default value: 7 days.
 - Backup execution time: It can be set to any time period in hours.


![](https://qcloudimg.tencent-cloud.cn/raw/951759547d49047b21c54606815e9b8e.png)

