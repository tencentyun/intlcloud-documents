### How do I back up TencentDB for SQL Server?
TencentDB for SQL Server has rich backup capabilities to guarantee the data security and prevent data loss or corruption. You can manage and view backups on the **Backup Management** page in the [console](https://console.cloud.tencent.com/sqlserver). Specifically, you can configure automatic backup, manual backup, data backup, log backup, backup file format (unarchived files or archive file), instance backup, multi-database backup, and cross-region backup. You can also customize the backup policy, backup retention period (7–1,830 days), and backup cycle. For more information, see [Backup Overview](https://intl.cloud.tencent.com/document/product/238/45857).

### How do I configure automatic backup?
You can do so on the **Backup Management** page in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). For more information, see [Configuring Automatic Backup](https://intl.cloud.tencent.com/document/product/238/45855).

### How do I create a backup manually?
You can do so on the **Backup Management** page in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). For more information, see [Creating Manual Backup](https://intl.cloud.tencent.com/document/product/238/45854).

### How do I view and modify backup policies?
You can do so on the **Backup Management** page in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). For more information, see [Configuring Automatic Backup](https://intl.cloud.tencent.com/document/product/238/45855).

### How long can TencentDB for SQL Server retain a backup?
TencentDB for SQL Server retains an automatic backup for seven days by default, which can be customized.
The validity period is subject to the configured backup retention period. For more information, see [Configuring Automatic Backup](https://intl.cloud.tencent.com/document/product/238/45855). There is no limit on the retention period of manual backups, and you can delete them as needed. For more information, see [Deleting Manual Backup](https://intl.cloud.tencent.com/document/product/238/45851).

[](id:KYSDSCM)
### Can I delete a backup manually?
- Automatic backups cannot be deleted manually. You can set the retention period for automatic backups, and they will be deleted automatically when they expire.
- Manual backups can be manually deleted from the backup list in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). They can be retained permanently as long as they are not deleted.

### Can I disable data and log backups?
No. However, you can lower the backup frequency and delete manual backup files no longer used in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) to reduce the backup space usage.

### Why can't I initiate a manual backup task?
Check the automatic backup time you configured. If the instance is performing the daily automatic backup task, you cannot initiate a manual backup task.

### How do I cancel a backup task?
Backup tasks in TencentDB for SQL Server cannot be canceled.

### Is a database available during the backup time period?
A backup window is a custom time period for daily automatic backup, during which the TencentDB for SQL Server instance will be backed up. Based on such regular backups, TencentDB for SQL Server allows you to roll back the instance to a backup point within the retention period. During the backup window, the business won't be affected, but you cannot restart or manually backup the instance in the TencentDB for SQL Server console.

### How do I back up individual databases in TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the ID of the target instance in the instance list, select the **Backup Management** tab, click **Backup Task Settings**, and set **Upload Backup File** to **Unarchived files**. Then, the .bak file of each database in the instance will be directly uploaded to COS without being archived. For more information, see [Setting Backup Task](https://intl.cloud.tencent.com/document/product/238/45853).

[](id:SLJXBFRW)
### How do I set to perform a backup task on the replica instance in TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the ID of the target instance in the instance list, select the **Backup Management** tab, click **Backup Task Settings**, and set **Execute Backup Task** to **On the replica node**. For more information, see [Setting Backup Task](https://intl.cloud.tencent.com/document/product/238/45853). You can configure this option only for 2017/2019 Cluster Edition instances.

### How do I download backup files of TencentDB for SQL Server?
The TencentDB for SQL Server console provides the list of backup files that can be downloaded over the private or public network.
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the ID of the target instance in the instance list, select the **Backup Management** tab, and click **Download** in the **Operation** column of a backup file in the backup list to get its private/public network download addresses. You can also directly click **Download** to download the file. For more information, see [Downloading Backup](https://intl.cloud.tencent.com/document/product/238/7523).

### Can I use a third-party tool to automatically back up TencentDB for SQL Server?
TencentDB for SQL Server cannot be backed up with third-party tools. For security considerations, third-party tools cannot be granted the permissions of data directories on the physical machine. You can initiate backup tasks only in the console.

### Can I download or restore backup files that exceed the retention period?
Expired backup sets will be automatically deleted and cannot be downloaded or restored.
- We recommend you configure a reasonable backup retention period based on your business needs or download the backup files in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
- You can also manually back up the instance data in the console, and manual backup files will be retained permanently.
>?Manual backups will also take up the backup space. We recommend you plan the usage of the backup space appropriately to reduce costs.

[](id:YGLSLXZ)
### Can I download the backup files of an isolated instance?
Yes.
- A pay-as-you-go instance will be isolated into the recycle bin 24 hours after expiration. At this time, rollback and manual backup will be prohibited, but automatic backup can still be downloaded by clicking **More** in the **Operation** column of the instance. Excessive backup space of the instance will continue to be billed until the instance is eliminated.

### Will backup files still be retained after a TencentDB for SQL Server instance is deleted?
After a TencentDB for SQL Server instance is deleted, all its backup files will be deleted automatically. To retain the data, back up the data first before deleting the instance.

### How is the TencentDB for SQL Server backup space billed?
TencentDB for SQL Server offers a certain amount of backup space free of charge by region, which is equivalent to the sum of storage spaces of all Basic Edition, Dual-Server High Availability Edition, and Cluster Edition primary instances in a region. For the pricing of backup space beyond the free tier, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/238/45849).

### What should I do if the free tier of the backup space is exceeded?
If the size of backup files exceeds the free tier of the backup space, you can increase the storage space or reduce the backup space usage.
Instance backup files will use the backup space. Each TencentDB for SQL Server instance provides a certain free tier of backup space, and excessive usage will incur additional fees.

[](id:JSBFKJKX)
### How do I reduce backup space costs in TencentDB for SQL Server?
- Delete manual backups that are no longer used (on the **Instance Management** > **Backup Management** page in the [TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver) console). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and backup file retention period in the console, which should be at least twice a week).
>?The [rollback feature](https://intl.cloud.tencent.com/document/product/238/7522) relies on the backup cycle and retention period of data backups and log backups, but reducing the frequency and retention period of automatic backups will affect the rollback time range for instance data, you need to configure backup appropriately based on your actual needs.
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of seven days can meet the needs in most cases).

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7–1,830 days |
| Non-core, non-data businesses | Seven days |
| Archival businesses | Seven days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | Seven days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |

### How do I view the backup space usage of TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) and select **Database Backup** to view the backup space statistics and trends of all instances in each region under your account as well as the real-time backup space statistics of each instance. For more information, see [Viewing Backup Space](https://intl.cloud.tencent.com/document/product/238/45850).

[](id:SLRHHDS)
### How do I roll back a TencentDB for SQL Server instance?
The retention period of TencentDB for SQL Server data backups is seven days by default and can be customized. The retention period of log backups is the same as that of data backups. You can roll back the instance data to any time point within the configured backup retention period. For more information, see [Rolling back Database](https://intl.cloud.tencent.com/document/product/238/7522).

### How do I clone a database in a TencentDB for SQL Server instance?
TencentDB for SQL Server provides the database cloning feature for you to quickly clone an existing database to your current instance. You need to specify the new database name during cloning, while other information such as account permissions of the new database is the same as that of the source database. For more information, see [Cloning Database](https://intl.cloud.tencent.com/document/product/238/47426).

### What can I do with downloaded data and log backups?
You can use backup files to restore data to other TencentDB or self-built databases at any time. For more information, see [Cold Backup Migration](https://intl.cloud.tencent.com/document/product/238/39005).

### Can I restore a downloaded backup to another TencentDB for SQL Server instance?
In the TencentDB for SQL Server console, you can use the cold backup migration feature to restore a database to another TencentDB for SQL Server instance from the downloaded backup file. For more information, see [Cold Backup Migration](https://intl.cloud.tencent.com/document/product/238/39005).

### How do I restore a backup of a self-built database to TencentDB for SQL Server?
In the TencentDB for SQL Server console, you can directly upload the backup file of a self-built database or download it from COS to restore it to TencentDB for SQL Server through the cold backup migration feature. For more information, see [Cold Backup Migration](https://intl.cloud.tencent.com/document/product/238/39005).

### Can I restore a full backup of TencentDB for SQL Server to a self-built database?
TencentDB for SQL Server supports full backup. After downloading a backup file, you can restore it to a self-built database as needed. For more information, see [Downloading Backup](https://intl.cloud.tencent.com/document/product/238/7523).

[](id:LZBFYHQB)
### What are the differences between direct backup upload and backup download from COS in cold backup migration?
- Direct backup upload: You can upload a local backup file to COS and download and restore it to TencentDB for SQL Server. Backup files uploaded to COS don't use any backup space. However, they can be retained for only 24 hours and will be deleted automatically after then.
- Backup download from COS: You can download a backup file from your COS bucket and restore it to TencentDB for SQL Server.

### If I directly upload a backup file in cold backup migration, will the file use my backup space?
Backup files uploaded in backup and restoration scenarios are directly uploaded to COS for relay and don't use your backup space. Once successfully uploaded, they will be retained for only 24 hours and will be deleted automatically after then.
