TencentDB for SQL Server supports automatic backup (including non-archive backup and archive backup) and manual backup.
This document describes how to configure archive backup retention in the console.
<dx-accordion>
::: Notes for automatic backup settings
- Backup files are stored in a separate backup space and do not occupy the local disk space of the instance.
- Do not perform DDL operations during the backup process to avoid backup failure due to table locking.
- Back up your data during off-peak hours.
- Backup may take a long time if the data volume is large.
:::
::: Description of automatic backup settings
- Increasing the retention period of data and log backups may cause additional backup space fees.
- Shortening the retention period of log backups may affect the data rollback cycle of the instance.
- The free tier for backups is limited, and any excess will be billed on a pay-as-you-go basis.
- Local backups are included in the free tier, while cross-region backups are not, that is, cross-region backups incur fees.
- Periodic archive takes affect only for local backups but not [cross-region backups](https://www.tencentcloud.com/document/product/238/49138), which will be retained for the period configured in the cross-region backup settings.
:::
::: Differences between non-archive backup and archive backup
**Differences**
Archive backup is a more flexible backup policy on the basis of non-archive automatic backup. It supports setting the number of retained backups by month, quarter, or year and does not need to retain additional new backups. However, its retention period is different from (longer than) that of non-archive backup.
**Example**
If the non-archive backup cycle in the automatic backup settings of instance A is Monday, Tuesday, and Wednesday, the archive backup retention policy is monthly, and the number of backups to be retained is 2, then the instance will still be automatically backed up every Monday, Tuesday, and Wednesday in the month, but the backup retention period will vary by archive backup policy. Among these backups, non-archive backups will be retained for the configured data backup retention period, while archive backups will be retained for the configured archive backup retention period. For example, if the system performs archive backup on a certain Wednesday, then the backup generated on the day will be retained for the archive backup retention period rather than in two copies for different retention periods.
</dx-alert>
:::
</dx-accordion>

## Enabling archive backup retention[](id:KQDQBL)
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/L8XN327_11.png)
3. On the instance management page, select **Backup Management** and click **Auto-Backup Settings**.
4. In the pop-up window, set the following configuration items, read and select **Backup Space Billing Notes**, and click **Save**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HVym110_12.png)

| Parameter | Description | 
|---------|---------|
| Start Time | You can set a start time as needed. We recommend that you set it to a value during off-peak hours. This is just the start time of the backup process and does not indicate the end time. <br>For example, if the time range is set to 01:00–02:00 AM, the system will initiate a backup at a time point during 01:00–02:00 AM, which depends on the backend backup policy and backup system conditions. |
| Data Backup Retention Period | It is 7 days by default and customizable between 7 and 1,830 days. Expired backup sets will be automatically deleted. |
| Backup Cycle | You can select any time between Monday and Sunday for backup. <dx-alert infotype="explain" title="Note">To ensure the continuity between the data backup retention period and backup cycle: <li>If the backup retention period is set to a value smaller than 7 days, the backup cycle will be daily, with Monday through Sunday being selected by default. </li><li>If the backup retention period is set to a value equal to or greater than 7 days, at least two backups will be required every week. If you select only one, you cannot click **Save**.</li></dx-alert> |
| Next Time | Set the time when the configured backup cycle will start. |
| Periodic Archive | Toggle on **Periodic Archive** and configure backup retention as follows. |
| Archive Backup Retention Period | It is 365 days by default and customizable between 90 and 3,650 days. Expired backup sets will be automatically deleted. <dx-alert infotype="explain" title="Note">The archive backup retention period should be longer than the non-archive backup retention period.</dx-alert> |
| Archive Backup Retention Policy | You can set the number of retained backups by month, quarter, or year. <dx-alert infotype="explain" title="Note">The maximum number of retained backup varies by time range and should not be exceeded. <li>If the number is 1, the first valid backup in the current cycle will be retained. </li><li>If the number is 2, the first and middle valid backups in the current cycle will be retained. </li><li>If the number is above 2, valid backups in the current cycle will be retained by the average time interval.</li></dx-alert> |
| Start Date | The time to start archive backup. |
| Log Backup Retention Period | It is the same as the non-archive data backup retention period by default and cannot be changed. Expired backup sets will be automatically deleted. |
| Log Backup Frequency | Backup is performed once every 10 minutes by default. |

## Modifying periodic archive
After periodic archive is enabled, you can modify the retention policy by setting parameters as instructed in [Enabling periodic archive](#KQDQBL).
>?
>- Modifying the archive backup retention period will affect the retention period of historical archive backups and cause expired backups to be cleared.
>- Modifying the archive backup retention policy will affect only new but not previously retained archive backups.
>- Modifying the start time will affect only new but not previously retained archive backups.

## Disabling period archive
>?
>- After it is disabled, no new archive backups will be generated.
>- After it is disabled, existing archive backups will be retained and automatically deleted upon expiration according to the original policy. You can also clear them by modifying the archive backup retention period.
>
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
3. On the instance management page, select **Backup Management** and click **Auto-Backup Settings**.
4. Toggle off **Periodic Archive**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8H7s750_13.png)

## Viewing the retention plan
After setting the archive backup retention policy and start time, you can click **View Retention Plan** next to the start time to preview the backup plan.
![](https://qcloudimg.tencent-cloud.cn/raw/9b7c21feff9bf1409c80f745fbf1d370.png)
- Blue dates are for non-archive backups.
- Red dates are for archive backups.
- You can click **Non-archive Backup** or **Archive Backup** to hide corresponding dates for easier preview.
- The backup plan preview is currently for backups for the year to come and is for reference only.

Example 1: Retaining one backup per month starting from December 1, 2022, with the backup cycle being Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, and Sunday.
Example 2: Retaining one backup per month starting from November 22, 2022, with the backup cycle being Monday, Wednesday, Friday, and Sunday.
Example 3: Retaining four backups per quarter starting from November 22, 2022, with the backup cycle being Monday, Wednesday, and Friday.
Example 4: Showing only dates in the archive backup retention plan.
