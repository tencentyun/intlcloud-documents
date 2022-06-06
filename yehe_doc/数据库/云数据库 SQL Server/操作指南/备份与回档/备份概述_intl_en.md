The backup feature can help you avoid accidental data loss in case of system hardware or instance failure. To protect your assets, TencentDB for SQL Server provides the data backup and restoration feature for you to archive data and restore data to local databases.

This document describes the backup feature.

## Backup Purposes
You can restore data from backups after a database or table is deleted maliciously or by mistake. This helps guarantee data security and avoid data loss and corruption.

## Backup Billing
Backups include data backups and log backups. For more information on billing, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/238/45849).

## Automatic Backup
TencentDB for SQL Server supports automatic backup settings. A data backup can be retained for up to 1,830 days. You can set the automatic backup cycle. We recommend you back up your data at least twice a week.
You can restore data to any time point within the backup retention period as needed. Automatic backups cannot be deleted manually and will be deleted automatically when they expire. For more information, see [Configuring Automatic Backup](https://intl.cloud.tencent.com/document/product/238/45855).

## Manual Backup
Instance backup and multi-database backup are supported. You can manually create a backup file at any time for any created database. The larger the backup file, the slower the manual backup. Generally, it takes about 5–120 minutes to complete a manual backup. For more information, see [Creating Manual Backup](https://intl.cloud.tencent.com/document/product/238/45854).

## Data Backup
You can back up one, multiple, or all databases in an instance. A backup file is retained for seven days by default. You can also customize the retention duration (3–1,830 days). Once expired, a backup file will be deleted automatically; therefore, download needed backup files to your local system promptly.

## Log Backup
The system automatically generates a log backup (log file) every 30 minutes and uploads it to the cloud for storage. You can download such log files.

## Backup Policy
Backup policies include instance backup and multi-database backup. The former backs up all databases in an instance, while the latter backs up selected databases.

## Backup Task Settings
You can configure the global variables of manual and scheduled backups through **Backup Task Settings**. You can set **Upload Backup File** to **Archive file** or **Unarchived files** and select the primary or replica instance for backup. For more information, see [Configuring Backup Task](https://intl.cloud.tencent.com/document/product/238/45853).

## Backup File Format
The **Upload Backup File** option allows you to specify the format of backup files (**Archive file** or **Unarchived files**). By default, backup files (i.e., .bak files) will be archived into a .tar file and then uploaded to COS. If you select "Unarchived files" as the backup file format, the .bak file of each database in the instance will be directly uploaded to COS without being archived.

## Backup Task Execution
The **Execute Backup Task** option allows you to decide whether to back up on the primary or replica node. By default, data is backed up on the primary node.

## Viewing and Downloading Backup
For easy backup query, management, and analysis, you can [view](https://intl.cloud.tencent.com/document/product/238/45852) and [download](https://intl.cloud.tencent.com/document/product/238/7523) backups in the console. You can also query the information of all backups or backups for today, the past 7, 15, or 30 days, or a custom period, including backup start/end time, name, policy, mode, file format, size, database, and status.

## Viewing Backup Space
The backup space occupied by TencentDB for SQL Server instance backup files is allocated by region. It is equivalent to the total storage capacity used by all database backups in a region, including automatic data backups, manual data backups, and log backups.
Increasing the backup retention period or frequency will use more database backup space. You can [view the backup space statistics](https://intl.cloud.tencent.com/document/product/238/45850) and trends of all instances in each region under your account as well as the real-time backup space statistics of each instance.

