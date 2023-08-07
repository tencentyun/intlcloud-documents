To avoid data loss or corruption, you can back up a database automatically or manually.

## Backup Overview
### Backup modes
TencentDB for MySQL single-node (cloud disk), two-node (local disk), and three-node (local disk) instances support **automatic backup** and **manual backup** of databases.

### Backup types
**TencentDB for MySQL two-node and three-node instances support two backup types:**
- **Physical backup**: A full copy of physical data (supports both automatic backup and manual backup).
- **Logical backup**:The backup of SQL statements (supports only manual backup).
>?
>- To restore a database from a physical backup, you need to use xbstream to decompress the package first. For more information, see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910).
>- If the number of tables in a single instance exceeds one million, backup may fail and database monitoring may be affected. Make sure that the number of tables in a single instance is below one million.
>- As the data of tables created by the MEMORY storage engine is stored in the memory, physical backups cannot be created for such tables. To avoid data loss, we recommend that you replace them with InnoDB tables.
>- If there are a high number of tables without a primary key in the instance, backup may fail, and the high availability of the instance may be affected. You need to create a primary key or secondary index for such tables in time.

| Physical Backup Advantages | Logical Backup Disadvantages |
|---------|---------|
| <li>High backup speed. <li>Streaming backup and compression are supported. <li>High success rate. <li>Simple and efficient restoration. <li>Faster backup-based coupling operations such as adding real-only instances and disaster recovery instances. <li>1/8 of average time needed for creating a logical backup. <li>Ten times faster than logical backups during import. | <li>Long time needed to restore as it takes time to run SQL statements and build indexes. <li>Low backup speed, especially when there are massive amounts of data. <li>Possible increase in source-replica delay due to the pressure on instances during backup. <li>Possible loss of precision information of floating points. <li>Potential backup failures due to wrong views and other problems. <li>Slower backup-based coupling operations such as adding read-only instances and disaster recovery instances. </li> |

**TencentDB for MySQL single-node instances of cloud disk edition support **snapshot backup**:**
**Snapshot backup** backs up data by creating snapshots for disks at the storage layer and is supported for both automatic and manual backups.

| Snapshot Backup Advantages | Snapshot Backup Disadvantages |
|---------|---------|
| <li>High backup speed. <li>Small size. | Cannot be downloaded. |


### Backup objects
 | Data Backup | Log Backup |
|---------|---------|
 | TencentDB for MySQL two-node and three-node instances: <li>Automatic backup supports full physical backup. <li>Manual backup supports full physical backup, full logical backup, and single-database/table logical backup. <li>Both automatic and manual backups can be compressed and downloaded. <br>Single-node instances of cloud disk edition:<li>Automatic backup supports full snapshot backup. <li>Manual backup supports full snapshot backup. <li>Both automatic and manual backups cannot be downloaded. | TencentDB for MySQL single-node (cloud disk edition), two-node, and three-node instances support binlog backup:<li>Log files occupy the instance's backup space. <li>Log files can be downloaded but cannot be compressed. <li>Retention periods can be set for log files. </li> |

## Note
- Since February 26, 2019, the automatic backup feature of TencentDB for MySQL only supports physical backup (default type) and no longer provides logical backup. automatically. Existing automatic logical backups will be switched to physical backups 
This will not affect your business access, but may have impact on your habit of automatic backup. If you need logical backups, you can use the manual backup option in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) or call the [CreateBackup](https://intl.cloud.tencent.com/document/product/236/15844) API to generate logical backups.
- Instance backup files occupy backup space. We recommend that you plan the usage of backup space appropriately. Usage of backup space that exceeds the free tier will incur fees. For more information, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).
- We recommend that you back up your database during off-peak hours.
- To avoid situations where the required backup files are deleted after the retention period lapses, you need to download them to the local file system in a timely manner.
- Do not perform DDL operations during the backup process to avoid backup failure due to table locking.
- TencentDB for MySQL single-node instances cannot be backed up.

## [Backing up MySQL Data Automatically](id:ZDBFSJ)
### Configuring automatic backup
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID on the instance list page to enter the management page, and select **Backup and Restoration** > **Auto-Backup Settings**.
![](https://qcloudimg.tencent-cloud.cn/raw/da6aad42478cbbddba52d02b1d677238.png)
2. Select backup parameters in the pop-up window as detailed below and click **OK**:
>?
> - The rollback feature as described in [Rolling back Databases](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backups and log backups (binlog). Rollback will be affected if you reduce the automatic backup frequency and retention period. You can select the parameters as needed.
> For example, if the backup cycle is set as Monday and Thursday and the retention period is set as seven days, you can roll a database back to any point of time in the past seven days, which is the actual retention days of data backups and log backups.
> - Automatic backups cannot be deleted manually. You can set the retention period for automatic backups, and the backups will be deleted automatically when they expire.
> - Increasing the retention period of data and log backups may cause additional backup space fees.
> - Shortening the retention period of log backups may affect the data rollback cycle of the instance.

In **Auto-Backup Settings**, you can enable periodic archive for data backups. The settings with periodic archive not enabled are non-archive backup settings. The following describes the parameters for **non-archive backup** and **archive backup**.

### Non-archive backup settings
![](https://qcloudimg.tencent-cloud.cn/raw/9c018f548a012b427daf0227f2a93642.png)

| Parameter | Description |
|---------|---------|
| Backup Start Time | <li>The default backup start time is automatically assigned by the system. <li>You can set a backup start time range as needed. We recommend that you set it to off-peak hours. This is just the start time of the backup process and does not indicate the end time. <br>For example, if the backup start time is set to 02:00-06:00 AM, the system will initiate a backup at a point in time during this period of time, which depends on the backend backup policy and backup system conditions. </br>
| Data Backup Retention Period | <li>For TencentDB for MySQL two-node and three-node instances, data backup files can be retained for 7 (default) to 1,830 days and will be automatically deleted upon expiration. <li>For TencentDB for MySQL single-node instances of cloud disk edition, data backup files can be retained for 7 (default) to 30 days and will be automatically deleted upon expiration. |
| Backup Cycle | **Configuration rules**: <li>By week: 7 days from Monday to Sunday are selected by default, and you can customize the backup time; however, to ensure your data security, we recommend that you configure to back up at least twice a week. <li>By month: To protect your data security, the interval between any two adjacent backup dates in a month cannot exceed 2 days; for example, if you choose to back up on the 1st day of a month, the next backup date cannot be the 5th day (with the 2nd, 3rd, and 4th days skipped). <dx-alert infotype="explain" title="">|
| If you choose to back up by month, to avoid the case of no backup for many consecutive days, the following dates cannot be skipped:  27/28/1, 28/29/1, 29/30/1, 28/1/2, 29/1/2, 30/1/2. ||
|</dx-alert> ||
|Transition-to-Cold Storage (optional)| Select the target data backup transition-to-cold storage policy and specify the number of days: <li>Standard storage days: Specify the number of days after which to transition a generated data backup to standard storage. <li>Archive storage days: Specify the number of days after which to transition a generated data backup to archive storage. <br>For more information on transition-to-cold storage, see [Configuring Transition-to-Cold Storage](https://www.tencentcloud.com/document/product/236/53949). Note that the archive storage type isn't available yet. |
| Log Backup Retention Period | <li>For TencentDB for MySQL two-node and three-node instances, log backup files can be retained for 7 (default) to 1,830 days and will be automatically deleted upon expiration. <li>For TencentDB for MySQL single-node instances of cloud disk edition, log backup files can be retained for 7 (default) to 30 days and will be automatically deleted upon expiration. |
|Transition-to-Cold Storage (optional) | Select the target binlog backup transition-to-cold storage policy and specify the number of days: <li>Standard storage days: Specify the number of days after which to transition a generated binlog backup to standard storage. <li>Archive storage days: Specify the number of days after which to transition a generated binlog backup to archive storage. <br>For more information on transition-to-cold storage, see [Configuring Transition-to-Cold Storage](https://www.tencentcloud.com/document/product/236/53949). Note that the archive storage type isn't available yet. |


### [Archive backup settings](id:DQBFBL)
>?
>- You cannot configure archive backup for single-node instances of cloud disk edition.
>- Archive backup retention period can only be longer than non-archive backup retention period.

![](https://qcloudimg.tencent-cloud.cn/raw/78c89e11aa7acab08de33b2f609fc56e.png)

| Parameter | Description |
|---------|---------|
| Backup Start Time | <li>The default backup start time is automatically assigned by the system. <li>You can set a backup start time range as needed. We recommend that you set it to off-peak hours. This is just the start time of the backup process and does not indicate the end time. <br>For example, if the backup start time is set to 02:00-06:00 AM, the system will initiate a backup at a point in time during this period of time, which depends on the backend backup policy and backup system conditions. </br>
| Data Backup Retention Period | For TencentDB for MySQL two-node and three-node instances, data backup files can be retained for 7 (default) to 1,830 days and will be automatically deleted upon expiration. |
| Backup Cycle | **Configuration rules**: <li>By week: 7 days from Monday to Sunday are selected by default, and you can customize the backup time; however, to ensure your data security, we recommend that you configure to back up at least twice a week. <li>By month: To protect your data security, the interval between any two adjacent backup dates in a month cannot exceed 2 days; for example, if you choose to back up on the 1st day of a month, the next backup date cannot be the 5th day (with the 2nd, 3rd, and 4th days skipped). <dx-alert infotype="explain" title="">|
| If you choose to back up by month, to avoid the case of no backup for many consecutive days, the following dates cannot be skipped: 27/28/1, 28/29/1, 29/30/1, 28/1/2, 29/1/2, 30/1/2. ||
|</dx-alert>||
| Archive Backup Retention Period | Data backup files can be retained for 90 to 3,650 days (1,080 days by default) and will be automatically deleted upon expiration. |
| Archive Backup Retention Policy | You can set the number of backups by month, quarter, or year. | |
| Start Time | The time to start archive backup. | |
|Transition-to-Cold Storage (optional)| Select the target data backup transition-to-cold storage policy and specify the number of days: <li>Standard storage days: Specify the number of days after which to transition a generated data backup to standard storage. <li>Archive storage days: Specify the number of days after which to transition a generated data backup to archive storage. <br>For more information on transition-to-cold storage, see [Configuring Transition-to-Cold Storage](https://www.tencentcloud.com/document/product/236/53949). Note that the archive storage type isn't available yet. |
| Log Backup Retention Period | Log backup files can be retained for 7 (default) to 1,830 days and will be automatically deleted upon expiration. |
|Transition-to-Cold Storage (optional) | Select the target binlog backup transition-to-cold storage policy and specify the number of days: <li>Standard storage days: Specify the number of days after which to transition a generated binlog backup to standard storage. <li>Archive storage days: Specify the number of days after which to transition a generated binlog backup to archive storage. <br>For more information on transition-to-cold storage, see [Configuring Transition-to-Cold Storage](https://www.tencentcloud.com/document/product/236/53949). Note that the archive storage type isn't available yet. |

### Viewing the retention plan
After you select an archive backup retention policy in the backup settings, you can click **View Retention Plan** to preview it.
- Blue dates are for non-archive backups.
- Red dates are for archive backups.
- You can click **Non-archive Backup** or **Archive Backup** to hide corresponding dates for easier preview.
- The backup plan preview is currently for backups for the year to come and is for reference only.

Example 1: The backup cycle is Monday, Wednesday, Friday, and Sunday, with one backup retained for each month starting from January 11, 2022.
![](https://qcloudimg.tencent-cloud.cn/raw/9815814482b467916689b36d7f7b523b.png)
Example 2: The backup cycle is Monday, Wednesday, and Friday, with three backups retained for each quarter starting from January 11, 2022.
![](https://qcloudimg.tencent-cloud.cn/raw/9815814482b467916689b36d7f7b523b.png)
Example 3: Show only archive backups.
![](https://qcloudimg.tencent-cloud.cn/raw/ec59982c8f84ae59e652f5efdfb65996.png)


## [Backing up MySQL Data Manually](id:manual-backup)
The manual backup feature allows you to initiate a backup task manually.
>?
>- For TencentDB for MySQL two-node and three-node instances, manual backup supports full physical backup, full logical backup, and single-database/table logical backup.
>- For TencentDB for MySQL two-node and three-node instances, manual backups can be manually deleted from the backup list in the console. You can delete manual backups that are no longer in use to free up space. Manual backups can be retained as long as they are not deleted until the database instance is deactivated.
>- For TencentDB for MySQL single-node instances of cloud disk edition, manual backup supports full snapshot backup.
>- For TencentDB for MySQL single-node instances of cloud disk edition, manual backups cannot be deleted.
>- When the instance is performing daily automatic backup, no manual backup tasks can be initiated.

**Directions for TencentDB for MySQL two-node and three-node instances**
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID on the instance list page to enter the management page, and select **Backup and Restoration** > **Manual Backup**.
2. Select backup modes and objects in the pop-up window, enter an alias, and click **OK**.
![](https://main.qcloudimg.com/raw/a16e644f51756b6a98597945e45329cd.png)
>?For single-database/table logical backup, select the database or table to be backed up in **Select databases and tables** in the left column and add the selected item to the right column. If you don't have a database, create a database or table first.
>
![](https://main.qcloudimg.com/raw/76924e2c76ac348b68ed113d679d6907.png)

**Directions for TencentDB for MySQL single-node instances of cloud disk edition**
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the target instance ID on the instance list page to enter the management page, and select **Backup and Restoration** > **Manual Backup**.
2. Enter an alias and click **OK**.

## FAQs
#### 1. Can I download or restore backup files that exceed the retention period?
Expired backup sets will be automatically deleted and cannot be downloaded or restored.
- We recommend that you configure a reasonable backup retention period based on your business needs or download the backup files in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). Note that the backup files of single-node instances of cloud disk edition cannot be downloaded.
- You can also manually back up instance data in the console. Manual backups will be retained permanently.
>?Manual backups will also take up the backup space. We recommend that you plan the usage of the backup space appropriately to reduce costs.

#### 2. Can I delete backups manually?
- You can't delete automatic backups manually, but you can set the retention period for them so that they are deleted automatically upon expiration. 
- For two-node and three-node instances, manual backups can be manually deleted from the backup list in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). Manual backups are retained permanently as long as they are not deleted. For single-node instances of cloud disk edition, manual backups cannot be deleted.

#### 3. Can I disable data and log backups?
No. However, you can reduce the backup frequency and delete unnecessary manual backups in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) to lower the space usage. Note that the manual backups of single-node instances of cloud disk edition cannot be deleted.

#### 4. How do I reduce the backup space costs?
- Delete manual backups that are no longer used. You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID/name to access the instance management page, and delete manual backups on the **Backup and Restore** tab. Note that the manual backups of single-node instances of cloud disk edition cannot be deleted. 
- Reduce the frequency of automatic data backup for non-core businesses. You can adjust the backup cycle and retention period in the console, and the frequency should be at least twice a week.
>?The rollback feature relies on the backup cycle and retention days of data backups and log backups (binlog). Rollback will be affected if you reduce the automatic backup frequency and retention period. You can select the parameters as needed. For more information, see [Rolling back Databases](https://intl.cloud.tencent.com/document/product/236/7276).
>
- Shorten the retention period of data and log backups for non-core businesses. A retention period of seven days can meet the needs in most cases.
- Configure the transition-to-cold storage policy to transition backup files and reduce the storage costs. For more information, see [Configuring Transition-to-Cold Storage](https://www.tencentcloud.com/document/product/236/53949).

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7–3,650 days. We recommend that you enable archive backup to periodically retain backup files in the long term. |
| Non-core, non-data businesses | 7 days |
| Archive businesses | 7 days. We recommend that you manually back up data based on your actual business needs and delete the backups promptly after use. |
| Testing businesses | 7 days. We recommend that you manually back up data based on your actual business needs and delete the backups promptly after use. |

