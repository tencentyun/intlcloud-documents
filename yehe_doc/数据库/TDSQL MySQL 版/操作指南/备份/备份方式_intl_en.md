TDSQL for MySQL supports full backups and incremental backups.

## Backup Type
### Full backup
You can set the start time and retention period for full backups. The retention period is 7 days by default.

### Incremental backup
Incremental backup is implemented based on binlogs, which are generated in real time. The binlogs use a certain amount of disk capacity, and are periodically uploaded to the TencentDB backup system.

## Custom Backup Time
1. Log in to the [TDSQL for MySQL Console](https://console.cloud.tencent.com/dcdb) and click the instance ID or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Shard Management** and click the shard ID to enter the shard management page.
3. Select **Backup and Restore** > **Backup and Log Settings** and click the icon as shown below to set the storage period.
 - Storage time: data and log backups can be retained for 1 to 7 days. Retention time is set to 7 days by default.
![](https://main.qcloudimg.com/raw/d72b61166d73b64ccb50f108d92a8cda.png)

