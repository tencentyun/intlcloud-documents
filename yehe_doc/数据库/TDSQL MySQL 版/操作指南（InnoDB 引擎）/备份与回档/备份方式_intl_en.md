
TDSQL for MySQL supports full backup and incremental backup.

## Backup Type
### Full backup
You can set the backup retention period for full backups, which is seven days by default.

### Incremental backup
Incremental backup is implemented based on binlogs, which are generated in real time. The binlogs use a certain amount of disk capacity, and are periodically uploaded to the TencentDB backup system.

## Custom Backup Time
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/dcdb) and click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Shard Management** tab and click a shard ID to enter the shard management page.
3. Select **Backup and Restoration** > **Backup and Log Settings** set the storage time.
Storage Time: Data and log backups can be retained for one to seven (default) days.
>?TDSQL for MySQL's backup feature will be commercialized in June 2022. You will be able to set more backup and log storage days then.
>
![](https://main.qcloudimg.com/raw/d72b61166d73b64ccb50f108d92a8cda.png)

