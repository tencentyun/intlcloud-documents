To avoid data loss or corruption, you can back up a database automatically or manually.

## Backup Overview
### Backup modes
Two-node and three-node TencentDB for MySQL instances support **automatic backup** and **manual backup** of databases.

### Backup types
Two-node and three-node TencentDB for MySQL instances support two backup types:
- **Physical backup**, which replicates full physical data (available for both automatic backup and manual backup).
- **Logical backup**, which backs up SQL statements (only available for manual backup).
>?
>- To restore a database from a physical backup, xbstream is required to decompress backup files first. For more information, see [Restoring Databases from Physical Backups](https://intl.cloud.tencent.com/document/product/236/31910).
>- If the number of tables in a single instance exceeds one million, backup may fail and database monitoring may be affected. Please make sure the number of tables in a single instance is no more than one million.
>- As the data of tables created by the MEMORY storage engine is stored in the memory, physical backups cannot be created for such tables. To avoid data loss, we recommend that you convert them to InnoDB tables.
>- If there are a high number of tables in an instance with no primary key, backup may fail and instance high availability may be affected. Please create primary keys or secondary indexes for such tables.

| Physical Backup Advantages | Logical Backup Disadvantages |
|---------|---------|
| <li>High backup speed. <li>Streaming backup and compression are supported. <li>High success rate. <li>Simple and efficient restoration. <li>Faster backup-based coupling operations such as adding real-only replicas and disaster recovery instances. <li>1/8 of average time needed for creating a logical backup. <li>Ten times faster than logical backups during import. | <li>Long time needed to restore as it takes time to run SQL statements and build indexes. <li>Low backup speed, especially when there are massive amounts of data. <li>Possible increase in source-replica delay due to the pressure on instances during backup. <li>Possible loss of precision information of floating points. <li>Potential backup failures due to wrong views and other problems. <li>Slower backup-based coupling operations such as adding read-only replicas and disaster recovery instances. |

### Backup objects
| Data Backup | Log Backup |
|---------|---------|
| Two-node and three-node TencentDB for MySQL: <li>Automatic backup supports full physical backup. <li>Manual backup supports full physical backup, full logical backup, and single-database/table logical backup. <li>Both automatic and manual backups can be compressed and downloaded. | Two-node and three-node TencentDB for MySQL support binlog backup: <li>Log files occupy the instance's backup space. <li>Log files can be downloaded but cannot be compressed. <li>Retention periods can be set for log files. |

## Notes
- Since February 26, 2019, the automatic backup feature of TencentDB for MySQL only supports physical backup (default type) and no longer provides logical backup. Existing automatic logical backups will be switched to physical backups automatically.
This will not affect your business access, but may impact your automatic backup habit. If you need logical backups, you can use the manual backup feature in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) or call the [CreateBackup API](https://intl.cloud.tencent.com/document/product/236/15844) to generate logical backups.
- Both logical and physical backup files will be compressed, so some files may be unusable after being downloaded. In that case, you can use the table backup feature in manual logical backup. For more information, see [Backing up MySQL Data Manually](#manual-backup).
- Instance backup files occupy backup space. We recommend that you plan the usage of backup space appropriately. Usage of backup space that exceeds the free tier will incur fees. For more information, please see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).
- We recommend that you back up your data during off-peak hours.
- We recommend that you download the backup files locally before they are deleted after the retention period ends.
- Do not perform DDL operations during the backup process to avoid backup failure due to table locking.
- Single-node TencentDB for MySQL instances cannot be backed up.

## Backing up MySQL Data Automatically
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID on the instance list page to access the instance’s management page, and select **Backup and Restore** > **Auto Backup Settings**.
![](https://main.qcloudimg.com/raw/69fed1aac393a518bd8cc2ad1fea550f.png)
2. Select backup parameters in the pop-up window (details are shown as below) and click **OK**:
>?
>- The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backups and log backups (binlog). Rollback will be affected if you reduce the automatic backup frequency and retention period. Please select the parameters as needed.
>For example, if the backup cycle is set as Monday and Thursday and the retention period is set as seven days, you can roll a database back to any point of time in the past seven days (which is the actual retention days of data backups and log backups).
>- Automatic backups cannot be deleted manually. You can set the retention period for automatic backups, and the backups will be deleted automatically when they expire.
>
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Backup Schedule</td><td>To ensure data security, please back up your data at least twice a week. All seven days of the week will be selected by default.</td></tr>
<tr>
<td>Backup Start Time</td><td><ul><li>The default backup start time is automatically assigned by the system. <li>You can set a start time as needed. We recommend that you set it to off-peak hours. This is just the start time of the backup process and does not indicate the end time. <br>For example, if the backup start time is set to 02:00-06:00, the system will initiate a backup at a point in time during 02:00-06:00, which depends on the backend backup policy and backup system conditions.</td></tr>
<tr>
<td>Data Backup Retention Time</td><td>Data backup files can be retained for 7 (default value) to 732 days.</td></tr>
<tr>
<td>Log Backup Retention Time</td><td>Log backup files can be retained for 7 (default value) to 732 days. <strong>The number of days set for log backup retention cannot exceed that for data backup retention.</strong></td></tr>
</tbody></table>
<img src="https://main.qcloudimg.com/raw/a371d4ba960264aa5630b59a3bfe5096.png"  style="margin:0;">

## [Backing up MySQL Data Manually](id:manual-backup)
The manual backup feature allows you to initiate a backup task manually.
>?
>- Manual backup supports full physical backup, full logical backup, and single-database/table logical backup.
>- Manual backups can be manually deleted from the backup list in the console. You can delete manual backups that are no longer in use to free up space. Manual backups can be retained permanently as long as they are not deleted.
>- When the instance is performing daily automatic backup, no manual backup tasks can be initiated.
>
1. On the instance list page, click an instance ID to access the instance’s management page, and select **Backup and Restore** > **Manual Backup**.
2. Select the backup mode and object in the pop-up window and click **OK**.
![](https://main.qcloudimg.com/raw/a16e644f51756b6a98597945e45329cd.png)
>?For single-database/table logical backup, select the database or table to be backed up in **Select database & table** in the left column and add the selected item to the right column. If you don't have a database, please create a database/table first.
>
![](https://main.qcloudimg.com/raw/76924e2c76ac348b68ed113d679d6907.png)

## FAQs
#### 1. Can I download or restore backup files that exceed the retention period?
Expired backup sets will be deleted automatically and cannot be downloaded or restored.
- We recommend that you configure a backup retention period based on business needs or download the backup files locally via the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
- You can also manually back up instance data in the console. Manual backups will be retained permanently.
>?Manual backups will also take up the backup space. We recommend that you plan the usage of backup space appropriately to reduce cost.

#### 2. Can I delete backups manually?
- Automatic backups cannot be deleted manually. You can set the retention period for automatic backups, and the backups will be deleted automatically when they expire. 
- Manual backups can be manually deleted from the backup list in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). Manual backups can be retained permanently as long as they are not deleted.

#### 3. Can I disable data and log backups?
No. However, you can reduce the backup frequency and delete manual backups no longer used via the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) to lower the capacity usage.

#### 4. How can I reduce the backup capacity costs?
- Delete manual backups that are no longer used (you can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID to access the instance’s management page, and delete manual backups on the **Backup and Restore** tab). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and retention period in the console, and the frequency should be at least twice a week).
>?The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backups and log backups (binlog). Rollback will be affected if you reduce the automatic backup frequency and retention period. Please select the parameters as needed.
>
- Reduce the retention period of data and log backups for non-core businesses (a 7-day retention period can meet the requirements of most scenarios).

| Business Scenario             | Recommended Backup Retention Period                                                 |
| -------------------- | ------------------------------------------------------------ |
| Core businesses             | 7-732 days                                              |
| Non-core and non-data businesses | 7 days                                                      |
| Archive businesses             | 7 days. We recommend that you manually back up data based on your business needs and delete the backups promptly after use |
| Testing businesses | 7 days. We recommend that you manually back up data based on your actual business needs and delete the backups promptly after use |

