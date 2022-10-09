TencentDB for SQL Server automatically backs up data based on the default backup settings. You can modify the automatic or manual backup settings in the console. You can also view the backup files and relevant information in the backup list.
This document describes how to view backup files in the console.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://qcloudimg.tencent-cloud.cn/raw/2289c7168a54e8f6de512dfd41f1255a.png)
3. On the **Backup Management** tab, view backup tasks in the data or log backup list.
   - The data backup list displays the backup start/end times, name, policy, file format, and size, database, region, status, and operations (download, restore, delete).
![](https://qcloudimg.tencent-cloud.cn/raw/d3b940edb74ff7b6c4211346b77e5d57.png)
   - The log backup list displays the file name, log data start/end times, backup size, backup region, and operation (download).
![](https://qcloudimg.tencent-cloud.cn/raw/87a60099a91eb9a7788079f83ef28972.png)
   - You can filter backup files by time (last hour, last 24 hours, today, last 7 days, last 30 days, or custom time period).
![](https://qcloudimg.tencent-cloud.cn/raw/5696c1da3100f8969d8559a2a6966f48.png)
   - You can search for **data backup files** in the search box on the right by backup name, database name, backup policy, backup mode, or backup file format.
![](https://qcloudimg.tencent-cloud.cn/raw/a9880e958a13887899aeeab42f7ba6e3.png)

## FAQs
#### 1. Can I download or restore backup files that exceed the retention period?
Expired backup sets will be automatically deleted and cannot be downloaded or restored.
- We recommend you configure a reasonable backup retention period based on your business needs or download the backup files in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
- You can also manually back up the instance data in the console, and manual backup files will be retained permanently.
>?Manual backups will also take up the backup space. We recommend you plan the usage of the backup space appropriately to reduce costs.

#### 2. Can I delete backups manually?
- Automatic backups cannot be deleted manually. You can set the retention period for automatic backups, and they will be deleted automatically upon expiration. If [Cross-Region Backup](https://www.tencentcloud.com/document/product/238/49138) is enabled, you can also set the retention period for cross-region backup files, which will be deleted automatically upon expiration.
- Manual backups can be manually deleted from the backup list in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). If they are not manually deleted, they will be retained for the same period as automatic backups.

#### 3. Can I disable data and log backups?
No. However, you can lower the backup frequency and delete manual backup files that are no longer used in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) to reduce the backup space usage.

#### 4. How do I reduce the backup space costs?
- Delete manual backups that are no longer used (on the **Instance Management** > **Backup Management** page in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver)). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and backup file retention period in the console, which should be at least twice a week).
>?The rollback feature as described in [Rolling back Database](https://intl.cloud.tencent.com/document/product/238/7522) relies on the backup cycle and retention days of data backups and log backups. Rollback will be affected if you reduce the automatic backup frequency and retention period. You can select the parameters as needed.
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of seven days can meet the needs in most cases).

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7–1,830 days |
| Non-core, non-data businesses | 7 days |
| Archival businesses | 7 days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | 7 days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |

#### 5. Can I download the backup files of an isolated instance?
Yes.
- A pay-as-you-go instance will be isolated into the recycle bin 24 hours after expiration. At this time, rollback and manual backup will be prohibited, but automatic backup can still be downloaded by clicking **More** in the **Operation** column of the instance. Excessive backup space of the instance will continue to be billed until the instance is eliminated.
