
To avoid data loss caused by system crashes or other problems, TencentDB for MongoDB supports data backup and rollback after system recovery to ensure data integrity.

## Background
**Backup types**
- Automatic backup: Data is automatically backed up as scheduled based on the system's default backup policy (such as default backup interval and mode).
- Manual backup: You can run a backup task at any time to meet your business Ops and troubleshooting requirements.

**Backup modes**
- Physical backup: In this mode, physical database files in an instance are backed up, which is fast and easy to restore with a high success rate. However, it has no portability, and the backup environment and restoration environment must be completely the same.
- Logical backup: In this mode, the database instance is connected to, and the mongodump tool is used to save the operation logs to a logical backup file to back up the data, which can be restored by replaying the operation logs. This mode is slow but has a high portability. You can restore the logical backup of a database to database on different versions. 

## Use limits
- Physical backups cannot be used to roll back databases tables.
- A backup can contain up to 7 days of continuous data; that is, you can roll back data to any time point in the last 7 days.

## Instructions
- Instance backup doesn't affect your business.
- Backup files are stored in COS without using the storage space of TencentDB for MongoDB instances. For more information on COS, see [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436). 

## Version overview
<table>
<thead><tr><th>Version</th><th>Instance Type</th><th>Automatic Backup</th><th>Manual Backup</th></tr></thead>
<tbody><tr>
<td rowspan="2">v3.2</td>
<td>Replica set</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td></tr>
<tr>
<td>Sharded cluster</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td></tr>
<tr>
<td rowspan="2">v3.6</td>
<td>Replica set</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup</li></ul></td></tr>
<tr>
<td>Sharded cluster</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup</li></ul></td></tr>
<tr>
<td rowspan="2">v4.0</td>
<td>Replica set</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td></tr>
<tr>
<td>Sharded cluster</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td></tr>
<tr>
<td rowspan="2">v4.2</td>
<td>Replica set</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td></tr>
<tr>
<td>Sharded cluster</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td></tr>
<tr>
<td rowspan="2">v4.4</td>
<td>Replica set</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td></tr>
<tr>
<td>Sharded cluster</td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td>
<td><ul><li>Default backup mode: Logical backup</li><li>Supported backup modes: Logical backup and physical backup</li></ul></td></tr>
</tbody></table>

## Billing
Currently, backup is free of charge. We will notify you when billing for the backup space officially starts.

## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded cluster instance is in **Running** status.

## Adjusting the automatic backup policy
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. Select the **Backup and Rollback** > **Backup Task List** page.
7. Select the **Auto-Backup Settings** tab and click **Edit**.
8. Edit **Backup Mode**, **Backup Interval**, and **Backup Exception Alert** based on the parameter descriptions in the following table.
9. Click **Save**, and the backup task will start after one minute.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Data Backup Retention</td><td>Data backup files can be retained for seven days by default.</td></tr>
<tr>
<td>Backup Mode</td><td><ul><li>Select a backup mode optionally.</li><li>TencentDB for MongoDB 3.6 replica set instances don't support this parameter.</li></ul></td></tr>
<tr>
<td>Backup Interval</td><td><ul><li>The data is <b>backed up once every 24 hours</b> (i.e., once every day) by default.</li><li>You can choose to <b>back up the data once every 12 hours</b> or <b>24 hours.</b></li></ul></td></tr>
<tr>
<td>Backup Start Time</td>
<td><ul><li>The default start time is 01:00–02:00; that is, the system starts the backup task between 01:00 and 02:00 every day.</li><li>You can select a different time period to start data backup as needed by your business.</li><li>The specific start time varies by the specific scheduling of the backup task.</li></ul></td></tr>
</tbody></table>      

## Manual backup
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. In the top-right corner of the **Instance Details** page, click **Manual Backup**.
7. (Optional) In the pop-up window, select the **Backup Mode**. TencentDB for MongoDB 3.6 replica set instances don't support this parameter.
8. Add remarks and click **OK**.

## Downloading a backup file
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. Select the **Backup and Rollback** > **Backup Task List** page.
7. In the **Backup Task List**, find the target file and click **Download** in the **Operation** column.
8. In the **Generate Backup File** pop-up window, read the backup prompt carefully and click **OK**.
9. Select the **File Download List** tab and view the backup task progress.
10. After the task execution is completed, you can back up the data to your local device and view it as follows:
  - Over public network: Click **Download from Public Network** in the **Operation** column and directly use the browser to download the backup to your local device.
  - Over private network: Copy the private network address and run a `wget` command `wget -c 'private network address' -O backup.tar` in a CVM instance to download the backup at a high speed over the private network. For detailed directions on how to log in to CVM, see [Customizing Linux CVM Configurations](www.tencentcloud.com/document/product/213/10517).

## Related APIs
| API | Description |
| -------------------------- | ------------------------------------------------------------ |
| DescribeDBBackups          | [Queries instance backup list](https://intl.cloud.tencent.com/document/product/240/40342) |
| CreateBackupDBInstance     | [Backs up instance](https://intl.cloud.tencent.com/document/product/240/37922) |
| DescribeBackupDownloadTask | [Queries backup download task information](https://intl.cloud.tencent.com/document/product/240/40342) |
| CreateBackupDownloadTask   | [Creates backup download task](https://intl.cloud.tencent.com/document/product/240/40343) |

