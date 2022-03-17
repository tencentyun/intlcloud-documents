TencentDB for SQL Server supports automatic backup and manual backup.
This document describes how to configure automatic backup in the console.
>!
>- Backup files are stored in a separate backup space and do not occupy the local disk space of the instance.
>- Do not perform DDL operations during the backup process to avoid backup failure caused by table locking.
>- Back up your data during off-peak hours.
>- Backup may take a long time if the data volume is large.

## Notes on Backup
1. Increasing the retention period of data and log backups may cause additional backup space fees.
2. Shortening the retention period of log backups may affect the data rollback cycle of the instance.
3. The free tier for backups is limited, and any excess will be billed on a pay-as-you-go basis.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://qcloudimg.tencent-cloud.cn/raw/cbf37d2a491b4f8ba2089edb597ee4d1.png)
3. On the instance management page, select **Backup Management** and click **Auto-Backup Settings**.
4. In the pop-up window, read and select **Backup Space Billing Description** and click **Save**.
   - **Start Time**: It is customizable and recommended to be within off-peak hours.
For example, if the time range is set to 01:00–02:00, the system will initiate a backup at a time point during 01:00–02:00, which depends on the backend backup policy and backup system conditions.
   - **Data Backup Retention Period**: It is seven days by default and customizable.
   - **Backup Cycle**: Any time between Monday and Sunday can be selected for backup.
>!To ensure the continuity between the start time and data retention period:
>- If the backup retention period is set to a value smaller than seven days, the backup cycle will be daily, with Monday through Sunday being selected by default.
>- If the backup retention period is set to a value equal to or greater than seven days, at least two backups will be required every week. If you select only one, you cannot click **Save**.
   - **Next Time**: Set the time when the configured backup cycle will start.
   - **Log Backup Retention Period**: It is the same as the data backup retention period by default and cannot be changed. Expired backup sets will be automatically deleted.
   - **Log Backup Frequency**: Backup is performed once every 30 minutes by default.
![](https://qcloudimg.tencent-cloud.cn/raw/66d0f3a95e970e0246d02aabf1967066.png)


