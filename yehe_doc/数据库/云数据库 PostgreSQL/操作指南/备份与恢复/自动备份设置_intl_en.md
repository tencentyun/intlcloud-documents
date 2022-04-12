This document describes how to modify the automatic backup settings in the TencentDB for PostgreSQL console. TencentDB for PostgreSQL will automatically back up data based on the default or configured backup settings.

## Notes
- Back up your data during off-peak hours.
- Backup may take a long time if the data volume is large.
- Download required backup files to your local file system promptly before they expire.
- The backup mode is physical backup, while logical backup is not supported currently.

## Directions
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql). In the instance list, select a region and click an instance ID to enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** tab and click **Auto-Backup Settings**.
![](https://qcloudimg.tencent-cloud.cn/raw/5628a31be8b3d5c9179858801d0f0ba4.png)
3. In the **Backup Settings** pop-up window, complete the data backup settings and click **OK**.
 - **Backup Start Time**: You can select the default time (i.e., when the resources are idle) or specify a time. Backups are initiated within this time window. If a backup fails to start as configured, it will not be retried, and another backup will be initiated in the next time window.
 - **Data Backup Retention Period**: You can specify a time range of 3–7 days after which the backup set will be automatically deleted. Data can only be restored to a specific point in time within the retention period.
 - **Backup Cycle**: Any day between Monday and Sunday can be selected.
![](https://qcloudimg.tencent-cloud.cn/raw/2e36218ca2f1afc36e3b3fe2ec9235b2.png)
4. When "Configured backup settings successfully" is displayed in the top-right corner, the automatic backup settings are completed.
![](https://qcloudimg.tencent-cloud.cn/raw/c7116fdb64295e99ef9fe4ce17908a50.png)
