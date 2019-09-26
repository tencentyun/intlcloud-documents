## Backup Overview
### Backup Modes
TencentDB for MySQL High-Availability Edition supports **auto backup** and **manual backup** of databases.

### Backup Types
TencentDB for MySQL High-Availability Edition supports two backup types:
- **Physical backup**, which is a full copy of physical data (supported for both auto backup and manual backup).
- **Logical backup**, which backs up SQL statements (only supported for manual backup).

>- To restore a database from a physical backup, you need to use xbstream to decompress the package first. For more information, see [Restoring a Database from a Physical Backup](https://cloud.tencent.com/document/product/236/33363).
>- If the number of tables in a single instance exceeds one million, backup may fail, and database monitoring may be affected. Please control the number of tables in one single instance appropriately and make sure that it is below one million.
>- As the data of tables created by the MEMORY storage engine is stored in the memory, physical backups cannot be created for such tables. To avoid data loss, it is recommended to replace them with InnoDB tables.

| Physical Backup Advantages | Logical Backup Disadvantages |
|---------|---------|
| <li>High backup speed. <li>Streaming backup and compression are supported. <li>High success rate. <li>Simple and efficient restoration. <li>Faster backup-based coupling operations such as adding real-only and disaster recovery instances. <li>1/8 of average time needed for creating a logical backup. <li>10 times faster than logical backups during import. | <li>Long time needed to restore as it takes time to run SQL and build indexes. <li>Low backup speed, especially when there are massive amounts of data. <li>Possible increase in master-slave delay due to the pressure on instances during backup <li>Possible loss of precision information of floating points. <li>Potential backup failures due to wrong views and other problems. <li>Slower backup-based coupling operations such as adding read-only and disaster recovery instances. |

### Backup Objects
| Data Backup | Log Backup |
|---------|---------|
| MySQL v5.5, 5.6, and 5.7 (High-Availability Edition): <li>Auto backup supports full physical backup. <li>Manual backup supports full physical backup, full logical backup, and single-database/table logical backup. <li>Both auto backup and manual backup can be compressed and downloaded. <li>Auto backups cannot be manually deleted, but their retention periods can be set. <li>Manual backups can be manually deleted and will be retained until they are deleted. | MySQL v5.5, 5.6, and 5.7 (High-Availability Edition): <li>Log files occupy the instance's backup capacity. <li>Log files can be downloaded but cannot be compressed. <li>Retention periods can be set for log files. |

## Precautions
- Starting from February 26, 2019, the auto backup feature of TencentDB for MySQL will only support physical backup (default type) and no longer provide logical backup. Existing automatic logical backups will be switched to physical backups automatically.
This will not affect your business access, but may have impact on your auto backup habit. If you need logical backups, you can use the manual backup method in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) or [call the relevant API](http://intl.cloud.tencent.com/document/product/236/15844) to generate logical backups.
- Both logical and physical backup files will be compressed, so some files may be unusable after being downloaded. In that case, you can use the table backup function in manual logical backup. For more information, see [manual backup](#manual-backup).
- Instance backup files occupy backup capacity, which is currently free of charge. If backup capacity is charged, we will inform you in advance. Please develop a backup schedule and plan the backup capacity appropriately to avoid potential extra fees in the future.
- It is recommended to back up your database during off-hours.
- To avoid situations where the required backup files are deleted after the retention period lapses, please download them to the local file system in a timely manner.
- DDL operations are prohibited during the backup process so as to avoid backup failure due to table locking.

## Backing up MySQL Data Automatically
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name on the instance list page to enter the management page, and select **Backup and Restore** > **Auto Backup Settings**.
> If this feature is not displayed in your console, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>
![](https://main.qcloudimg.com/raw/69fed1aac393a518bd8cc2ad1fea550f.png)
2. Select backup parameters in the pop-up window as detailed below and click **OK**:
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Backup initiation time</td>
<td><ul><li>You can customize a time range as needed and are recommended to back up your database during off-hours.
<li>The default backup initiation time is automatically assigned by the system. This is just the start time of the backup process and does not indicate the end time. <br>For example, if the time range is 02:00-06:00, the system will initiate a backup at a point in time during 02:00-06:00, which depends on the backend backup policy and backup system conditions. </td>
</tr>
<tr>
<td>Data backup retention period</td>
<td><ul><li>Data backup files can be retained for 7 (default value) to 732 days (backup capacity is currently available free of charge). <li>If backup capacity is charged, we will inform you in advance.</td>
</tr>
<tr>
<td>Log backup retention period</td>
<td><ul><li>Log backup files can be retained for 7 (default value) to 732 days (backup capacity is currently available free of charge). <strong>The number of days set for log backup retention must be smaller than that for data backup retention.</strong> <li>If backup capacity is charged, we will inform you in advance.</td>
</tr>
</tbody></table>

![](https://main.qcloudimg.com/raw/a371d4ba960264aa5630b59a3bfe5096.png)


<span id = "manual-backup"></span>
## Backing up MySQL Data Manually
The manual backup feature allows you to initiate a backup task manually.
>- Manual backup supports full physical backup, full logical backup, and single-database/table logical backup.
>- Frequent manual backup will increase the backup capacity. Please plan the backup capacity appropriately. If backup capacity is charged, we will inform you in advance.
>- You can delete manual backups to release backup capacity.
>
1. On the instance list page, click an instance name to enter the management page, and select **Backup and Restore** > **Manual Backup**.
>If this feature is not displayed in your console, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>
2. Select backup modes and objects in the pop-up window and click **OK**.
![](https://main.qcloudimg.com/raw/a16e644f51756b6a98597945e45329cd.png)
> For logical single-database/table backup, select the database or table to be backed up in **Select database & table** in the left column and add the selected item to the right column. If you don't have a database, please create a database/table first.
>
![](https://main.qcloudimg.com/raw/76924e2c76ac348b68ed113d679d6907.png)
