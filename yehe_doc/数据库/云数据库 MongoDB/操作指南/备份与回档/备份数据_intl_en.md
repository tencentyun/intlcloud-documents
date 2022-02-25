
To avoid data loss caused by system crashes or other problems, TencentDB for MongoDB supports data backup and rollback after system recovery to ensure data integrity.

## Background
**Backup types**
- Auto backup: data is automatically backed up as scheduled according to the system's default backup policy (such as default backup interval and mode).
- Manual backup: you can run a backup task at any time to meet your business Ops and troubleshooting requirements.

**Backup modes**
- Physical backup: in this mode, physical database files in an instance are backed up, which is fast and easy to restore with a high success rate. However, it has no portability, and the backup environment and restoration environment must be completely the same.
- Logical backup: in this mode, the database instance is connected to, and the mongodump tool is used to save the operation logs to a logical backup file to back up the data, which can be restored by replaying the operation logs. This mode is slow but has a high portability. You can restore the logical backup of a database to database on different versions. 

## Use Limits
- Physical backups cannot be used to roll back databases/tables.
- A backup can contain up to 7 days of continuous data; that is, you can roll back data to any time point in the last 7 days.

## Notes
- Instance backup doesn't affect your business.
- Backup files are stored in COS without using the storage space of TencentDB for MongoDB instances. For more information on COS, see [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436). 

## Version Description
<table>
<thead><tr><th>Version</th><th>Instance Type</th><th>Auto Backup</th><th>Manual Backup</th></tr></thead>
<tbody><tr>
<td rowspan="2">3.2</td><th>Replica set</th><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td></tr>
<tr>
<th>Sharded cluster</th><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td></tr>
<tr>
<td rowspan="2">3.6</td><th>Replica set</th><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup</li></ul></td><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup</li></ul></td></tr>
<tr>
<th>Sharded cluster</th><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup</li></ul></td><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup</li></ul></td></tr>
<tr>
<td rowspan="2">4.0</td>
<th>Replica set</th><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup</li></ul></td><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup</li></ul></td></tr>
<tr><th>Sharded cluster</th><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td></tr>
<tr>
<td rowspan="2">4.2</td>
<th>Replica set</th><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td></tr>
<tr>
<th>Sharded cluster</th>
<td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td><td><ul><li>Default backup mode: logical backup</li><li>Supported backup modes: logical backup and physical backup</li></ul></td></tr>
</tbody></table>

## Billing Description
Currently, backup is free of charge. We will notify you when billing for the backup space officially starts.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is in **Running** status.

## Directions
### Adjusting auto backup policy
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. Select the **Backup and Rollback** > **Backup Task List** page.
7. Select the **Auto-Backup Settings** tab and click **Edit**.
8. Edit **Backup Mode**, **Backup Interval**, and **Backup Exception Alert** according to the parameter descriptions in the following table.
9. Click **Save**, and the backup task will start after 1 minute.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Data Backup Retention</td><td>Data backup files can be retained for 7 days by default.</td></tr>
<tr>
<td>Backup Mode</td><td><ul><li>Select a backup mode optionally.</li><li>TencentDB for MongoDB 3.6 and 4.0 replica set instances don't support this parameter.</li></ul></td></tr>
<tr>
<td>Backup Interval</td><td><ul><li>The data is <b>backed up once every 24 hours</b> (i.e., once every day) by default.</li><li>You can choose to <b>back up the data once every 12 hours</b> or <b>24 hours.</b></li></ul></td></tr>
<tr>
<td>Backup Start Time</td>
<td><ul><li>The default start time is 01:00–02:00; that is, the system starts the backup task between 01:00 and 02:00 every day.</li><li>You can select a different time period to start data backup as needed by your business.</li><li>The specific start time varies by the specific scheduling of the backup task.</li></ul></td></tr>
<tr>
<td>Backup Exception Alert</td>
<td><ul><li>It specifies whether to notify users through CM events if an exception occurs while executing a backup task. </li><li>Currently, only users in the allowlist can use the CM events. To get allowed, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>. </li>For more information on the supported TencentDB MongoDB events, see<a href="https://intl.cloud.tencent.com/document/product/248/32823">Product Event List</a>.</ul></td></tr>
</tbody></table>      

### Manual backup
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. In the top-right corner of the **Instance Details** page, click **Manual Backup**.
7. (Optional) In the pop-up window, select a **backup mode**. TencentDB for MongoDB 3.6 and 4.0 replica set instances don't support this parameter.
8. Add remarks and click **OK**.

### Downloading backup file
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. Select the **Backup and Rollback** > **Backup Task List** page.
7. In the **Backup Task List**, find the target file and click **Download** in the **Operation** column.
8. In the **Generate Backup File** pop-up window, read the backup prompt carefully and click **OK**.
9. Select the **File Download List** tab and view the backup task progress.
10. After the task execution is completed, you can back up the data to your local device and view it as follows:
  - Over public network: click **Download from Public Network** in the **Operation** column and directly use the browser to download the backup to your local device.
  - Over private network: copy the private network address and run a `wget` command `wget -c 'private network address' -O backup.tar` in a CVM instance to download the backup at a high speed over the private network. For detailed directions on how to log in to CVM, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).

## Related APIs
| API | Description |
| -------------------------- | ------------------------------------------------------------ |
| DescribeDBBackups          | [Queries instance backup list](https://intl.cloud.tencent.com/document/product/240/40342) |
| CreateBackupDBInstance     | [Backs up instance](https://intl.cloud.tencent.com/document/product/240/37922) |
| DescribeBackupDownloadTask | [Queries backup download task information](https://intl.cloud.tencent.com/document/product/240/40342) |
| CreateBackupDownloadTask   | [Creates backup download task](https://intl.cloud.tencent.com/document/product/240/40343) |

