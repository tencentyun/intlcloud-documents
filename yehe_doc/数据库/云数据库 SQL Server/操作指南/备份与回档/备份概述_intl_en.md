The backup feature can help you avoid accidental data loss in case of system hardware or instance failure. To protect your assets, TencentDB for SQL Server provides the data backup and restoration feature for you to archive data and restore data to local databases.

This document describes the backup feature.

## Backup purposes
You can restore data from backups after a database or table is deleted maliciously or by mistake. This helps guarantee data security and avoid data loss and corruption.

## Backup billing
Backups include data backups and log backups. For more information on billing, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/238/45849).

## Automatic backup
TencentDB for SQL Server supports automatic backup, including non-archive backup and archive backup. Archive backup is a more flexible backup policy on the basis of non-archive automatic backup and does not need to retain additional new backups. You can set the automatic backup retention policy based on your business needs to easily manage the backup retention period and cycle. You can also flexibly set the number of retained backups for the specified cycle to implement long-term backup storage, or shorten the non-archive backup retention period to reduce storage costs.
- **Non-Archive Backup**: The data backup retention period is customizable between 7 and 1,830 days. The log backup retention period is the same as the data backup retention period by default. You can set the automatic backup cycle. We recommend you back up your data at least twice a week. For more information, see [Setting Non-Archive Backup Retention](https://intl.cloud.tencent.com/document/product/238/45855).
- **Archive Backup**: The archive backup retention period is 365 days by default and customizable between 90 and 3,650 days. It can only be longer than the non-archive backup retention period. The archive backup retention frequency and start time can be customized. For more information, see [Setting Archive Backup Retention](https://www.tencentcloud.com/document/product/238/51892).

## Manual backup
Instance backup and multi-database backup are supported. You can manually create a backup file at any time for any created database. The larger the backup file, the slower the manual backup. Generally, it takes about 5–120 minutes to complete a manual backup. For more information, see [Creating Manual Backup](https://intl.cloud.tencent.com/document/product/238/45854).

## Cross-region backup
You can store backup files in another region, which enhances the regulatory compliance and disaster recovery capabilities and improves the data reliability. After this feature is enabled, cross-region backup will be triggered after the local default automatic backup is completed, that is, the default automatic backup will be dumped to the cross-region backup storage device. The cross-region backup retention period is customizable between 7 and 1,830 days. For more information, see [Cross-Region Backup](https://intl.cloud.tencent.com/document/product/238/49138).

## Data backup
You can back up one, multiple, or all databases in an instance. A backup file is retained for 7 days by default. You can also customize the retention period (3–1,830 days). Once expired, a backup file will be deleted automatically; therefore, download needed backup files to your local system promptly.

## Log backup
The system automatically generates a log backup (log file) every 10 minutes and uploads it to the cloud for storage. You can download such log files.

## Backup policy
Backup policies include instance backup and multi-database backup. The former backs up all databases in an instance, while the latter backs up selected databases.

## Backup task settings
You can configure the global variables of manual and scheduled backups through **Backup Task Settings**. You can set **Upload Backup File** to **Archive file** or **Unarchived files** and select the primary or replica instance for backup. For more information, see [Setting Backup Task](https://intl.cloud.tencent.com/document/product/238/45853).

## Backup file format
The **Upload Backup File** option allows you to specify the format of backup files (**Archive file** or **Unarchived files**). By default, backup files (i.e., .bak files) will be archived into a .tar file and then uploaded to COS. If you select "Unarchived files" as the backup file format, the .bak file of each database in the instance will be directly uploaded to COS without being archived.

## Backup task execution
The **Execute Backup Task** option allows you to decide whether to back up on the primary or replica node. By default, data is backed up on the primary node.

## Viewing and downloading a backup
For easy backup query, management, and analysis, you can [view](https://intl.cloud.tencent.com/document/product/238/45852) and [download](https://intl.cloud.tencent.com/document/product/238/7523) backups in the console. You can also query the information of all backups or backups for today, the past 7, 15, or 30 days, or a custom period, including backup start/end time, name, policy, mode, file format, size, database, and status.

## Viewing the backup space
The backup space occupied by TencentDB for SQL Server instance backup files is allocated by region. It is equivalent to the total storage capacity used by all database backups in a region, including automatic data backups, manual data backups, and log backups.
Increasing the backup retention period or frequency will use more database backup space. You can view the backup space statistics and trends of all instances in each region under your account as well as the real-time backup space statistics of each instance. For more information, see [Viewing Backup Space](https://intl.cloud.tencent.com/document/product/238/45850).
