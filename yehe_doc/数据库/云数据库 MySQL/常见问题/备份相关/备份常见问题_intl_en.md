- **Backup space billing**
 -  [How is the backup space billed?](#bfwt1)
 -  [How do I reduce the backup space costs?](#bfwt2)
- **Database backup**
 - [How do I configure automatic backup?](#bfwt3)
 - [Why can't I initiate a manual backup task?](#bfwt13)
 - [Why can't I logically back up and download by table?](#bfwt14)
 - [How do I back up data on my own?](#bfwt4)
 - [Can I download or restore backup files that exceed the retention period?](#bfwt11)
 - [Can I disable data and log backups?](#bfwt12)
 - [How do I cancel a backup task?](#bfwt9)
 - [Can I delete backups manually?](#bfwt8)
- **Backup and restoration**
 - [How do I download xbstream and qpress?](#bfwt16)
 - [Why can't I unpack/decompress a downloaded backup file with tar?](#bfwt15)
 - [What should I do if the backup download is slow?](#bfwt10)
 - [Why does an error occur when I download data backup files?](#bfwt6)
 - [Can I restore the downloaded backups to another TencentDB for MySQL instance?](#bfwt7)
 - [How do I restore and migrate the backups of basic single-node instances?](#bfwt5)


 [](id:bfwt1)
### How is the backup space billed? 
TencentDB for MySQL offers a certain amount of backup capacity for free based on the region. The capacity is equivalent to the sum of the storage capacity of all two-node and three-node instances (including source instances and disaster recovery instances) in the region.
For prices of backup capacity that exceeds the free tier, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).

[](id:bfwt2)
### How do I reduce the backup space costs?
- Delete manual backups that are no longer used (you can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID/name to access the instance management page, and delete manual backups on the **Backup and Restore** tab). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and backup file retention period in the console, which should be at least twice a week).
>?The rollback feature relies on the backup cycle and retention days of data backups and log backups (binlog). Rollback will be affected if you reduce the automatic backup frequency and retention period. You can select the parameters as needed. For more information, see [Rolling back Database](https://intl.cloud.tencent.com/document/product/236/7276).
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of seven days can meet the needs in most cases).

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7–1,830 days |
| Non-core, non-data businesses | 7 days |
| Archival businesses | 7 days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | 7 days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |

[](id:bfwt3)

### How do I configure automatic backup?
You can configure it on the **Backup and Restoration** tab in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
![](https://qcloudimg.tencent-cloud.cn/raw/053719ca0c4898c87bad068cbf70651c.png)

[](id:bfwt4)
### How do I back up data on my own?
TencentDB for MySQL instances are fully backed up on a daily basis by default. For more information, see [Backing up Database > Backup modes](https://intl.cloud.tencent.com/document/product/236/37796). You can also back up data by using the following methods:
- Use mysqldump.
- Use a third-party tool such as Navicat Premium.
- Log in to phpMyAdmin as instructed in [DMC Management](https://intl.cloud.tencent.com/document/product/236/39353) and click **Export** on the navigation bar at the top.

[](id:bfwt5)
### How do I restore and migrate the backups of basic single-node instances?
Basic single-node instances only support snapshot backups. For more information, see [Offline Migration of Data > Data Migration with Command Line Tool](https://intl.cloud.tencent.com/document/product/236/8464).

[](id:bfwt6)
### Why does an error occur when I download data backup files?
You can use the `wget -c 'backup file download address' -O custom filename.xb` command to download data backup files. Note that the download address should be placed inside a pair of single quotation marks (') to help the program identify it.

[](id:bfwt7)
### Can I restore the downloaded backups to another TencentDB for MySQL instance?
Yes. For detailed directions, see [Restoring Database from Logical Backup](https://intl.cloud.tencent.com/document/product/236/31909).

[](id:bfwt8)
### Can I delete backups manually?
- Automatic backups cannot be deleted manually. You can set the retention period for automatic backups, and they will be deleted automatically when they expire.
- Manual backups can be manually deleted from the backup list. They can be retained permanently as long as they are not deleted.
 1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID/name to access the instance management page, and select the **Backup and Restoration** tab.
 2. Click **Delete** in the **Operation** column in the backup list.

[](id:bfwt9)
### How do I cancel a backup task?
Backup tasks cannot be canceled.

[](id:bfwt10)
### What should I do if the backup download is slow?
We recommend you copy the download address on the **Backup and Restoration** tab in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), log in to a Linux CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for download over the private network at a higher speed.
`wget` command format: wget -c 'backup file download address' -O custom filename.xb

[](id:bfwt11)
### Can I download or restore backup files that exceed the retention period?
Expired backup sets will be automatically deleted and cannot be downloaded or restored.
- We recommend you configure a reasonable backup retention period based on your business needs or download the backup files in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
- You can also manually back up instance data in the console. Manual backups will be retained permanently.
>?Manual backups will also take up the backup space. We recommend you plan the usage of the backup space appropriately to reduce costs.

[](id:bfwt12)
### Can I disable data and log backups?
No. However, you can reduce the backup frequency and delete manual backups no longer used in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) to lower the space usage.

[](id:bfwt13)
### Why can't I initiate a manual backup task?
You need to check the automatic backup time you configured. If the instance is performing the daily automatic backup task, you cannot initiate a manual backup task.

[](id:bfwt14)
### Why can't I logically back up and download by tables?
After the backup feature as described in [Backing up Database](https://intl.cloud.tencent.com/document/product/236/37796) was upgraded, both logical and physical backups adopted the new compression algorithm, making some download features currently unavailable. To perform logical backups by tables, you can select **Logical backup** > **Specify Table** in manual backup and download the completed backup file.

[](id:bfwt15)
### Why can't I unpack/decompress a downloaded backup file with tar?
Because backup files in the latest version adopt a new compression algorithm, they cannot be unpacked/decompressed with the tar tool. Instead, xbstream and qpress are required.
For more information on how to unpack/decompress backup files with xbstream and qpress, see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910) and [Restoring Database from Logical Backup](https://intl.cloud.tencent.com/document/product/236/31909).

[](id:bfwt16)
### How do I download xbstream and qpress?
- xbstream is a subprogram of Percona XtraBackup. To use it, you need to install Percona XtraBackup from binaries or `yum` repositories.
- Extract the qpress binary files by running the tar command after downloading qpress.
For more information on XtraBackup and qpress installation, see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910).

