TencentDB for TDSQL supports full backup and incremental backup.

## Backup Type
### Full backup
You can set the start time and retention period for full backups. By default, the backup starts at 00:00–05:00 AM, during which the performance is relatively low. The retention period is 7 days by default.

### Incremental backup
Incremental backup is implemented based on binlogs, which are generated in real time. The binlogs use a certain amount of disk capacity, and are periodically uploaded to the TencentDB backup system.

## Custom Backup Time
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb) and click the instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Shard Management** and click the shard ID to enter the shard management page.
3. Select **Backup and Restore** > **Backup and Log Settings** and click the icon as shown below to set the storage period.
 - Backup cycle: the backup task is performed every day by default.
 - Storage time: the max number of days to retain data backups and log backups ranges from 1 to 7 (by default).
![](https://main.qcloudimg.com/raw/041408599f01dd7d464c9884858985cd.png)

