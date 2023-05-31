
Data is the core asset of enterprises. As your business develops, your data grows in a large-scale and explosive manner. Business applications require real-time, online, and fast data processing. It is more and more challenging for database Ops engineers to protect the data integrity, as data loss may occur for a variety of causes, such as accidental deletion, system vulnerabilities and viruses, hardware failures, and even natural disasters. Therefore, backup and rollback are of significant importance to databases.

## Backup Overview
TDSQL-C for MySQL supports data backup and binlog backup. A complete data backup supplemented by a follow-up binlog backup allows you to restore the entire TDSQL-C for MySQL cluster or specified databases/tables to any time point.

You can visually query the field information in the data backup list, such as file name/alias, backup time, start time, end time, backup type, backup mode, backup size, status, and operation. You can also query similar fields in the binlog backup list, including file name, binlog backup start time, binlog backup end time, backup size, and operation. This helps you easily view and manage historical backups.

The backup and rollback console UI is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ab95bb9e785013523cde164556287346.png)

### Data backup
Data backup means generating a backup file containing all the data in a cluster at a specific time point. TDSQL-C for MySQL supports logical backup and snapshot backup. The former is a full backup, while the latter is a full + incremental backup.

- **Logical backup**: It supports full backup only, where the logical structure and content of a database are stored as SQL statements. It backs up database objects, including tables, indexes, and stored procedures. This mode features a more refined backup granularity at the database or table level and a lower impact on the performance; however, it is slow and space-intensive.
- **Snapshot backup**: It uses the redirect-on-write (ROW) technology to take snapshots of the disks at the storage layer for backup. It features fast backup in seconds, imperceptibility to the computing layer, and low space usage.
 - **Full backup**: It copies all the data at a specific time point.
 - **Incremental backup**: It backs up only new or modified files based on the last backup.

### Backup types
<table>
<thead><tr><th colspan = "2" style="text-align:center" width="28%">Backup Type</th><th>Strengths/Shortcomings</th><th>Object</th><th>Mode</th><th>Download</th><th>Deletion</th></tr></thead>
<tbody>
<tr>
<td>Logical backup</td><td>Full backup</td><td><li>Strengths: The backup is at the database or table level, with a lower impact on the database performance.<br><li>Shortcomings: The backup task locks the database, takes a long time, and uses a lot of space.</td><td>Objects such as tables, indexes, and stored procedures, as well as the entire cluster</td><td>Manual</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td rowspan="3">Snapshot backup</td><td rowspan="2" >Full backup</td><td rowspan="3" ><li>Strengths: The backup task can be completed in seconds and imperceptible to the business, with a small space used.<br><li>Shortcomings: The backup file cannot be downloaded.</td><td rowspan="3" >The entire cluster</td><td>Manual</td><td>×</td><td>&#10003;</td>
</tr>
<tr><td>Automatic</td><td>×</td><td>×</td></tr>
</tr>
<tr><td>Incremental backup</td><td>Automatic</td><td>×</td><td>×</td></tr>
</tbody></table>

### Binlog backup
<table>
<thead><tr><th colspan = "2" style="text-align:center" width="28%">Backup Type</th><th>Strengths/Shortcomings</th><th>Object</th><th>Mode</th><th>Download</th><th>Deletion</th></tr></thead>
<tbody>
<tr>
<td>Binlog backup</td><td>Incremental backup</td><td><li>Strengths: Incremental data is recorded and can be restored to any time point.<br><li>Shortcomings: The binlog backup task lowers the instance's write performance.</td><td>The entire cluster</td><td>Automatic</td><td>&#10003;</td><td>x</td></tr>
</tbody></table>

A binlog backup is the incremental data generated after all the data in the cluster is backed up to a file at a specific time point. TDSQL-C for MySQL generates a large number of binlogs when executing large transactions or lots of DML operations, which are uploaded to the cloud storage and displayed in the binlog backup list in the console. The binlog backup mode applies to operation log storage.

TDSQL-C for MySQL relies on redo logs rather than binlogs for rollback, so that even if binlog is disabled, data can still be rolled back to any time point, and the instance performance can be increased by over 30%.

## Note
- Only one manual backup task can be performed per hour. Automatic backup tasks are performed according to your configuration, which is once per day by default.
- Manual backup files can be manually deleted from the backup list. They are retained as long as they are not deleted; therefore, regularly delete those no longer needed to free up the space.
- Automatic backups cannot be deleted manually. You can set a retention period so that they will be deleted automatically upon expiration.
- You can query the binlog backup size in the log backup list. The total binlog backup size is the sum of sizes of all binlog backups.

## Rollback Overview
TDSQL-C for MySQL supports data restoration to a specific time point through the rollback feature, minimizing potential system losses.
TDSQL-C for MySQL can roll back databases/tables to the original cluster and roll back an entire cluster (clone) to a new cluster. You can choose different rollback methods based on your business needs.

## Rollback Method
- Rollback by backup file: This method restores the cluster to the data file state of a backup file. The selection range of the backup file is determined by the data backup retention period you set.
- Rollback by time point: This method restores the cluster to any time point within the binlog backup retention period you set.
