This document describes how to migrate data from SQL Server databases in other cloud vendors and self-built SQL Server databases to TencentDB for SQL Server in the TencentDB for SQL Server Console.

## Overview
Cold backup migration restores data from .bak files, which is applicable to data migration from SQL Server databases in other cloud vendors and self-built SQL Server databases to TencentDB for SQL Server, and backup can be performed when the system is shut down.

TencentDB for SQL Server supports migrating data to TencentDB for SQL Server via [COS](https://intl.cloud.tencent.com/document/product/436/6222) files or locally uploaded files.

## Notes
- Before migration, make sure that the SQL Server version of the target instance is not lower than that of the source instance.
- The name of the migrated database can’t be the same as that of the TencentDB for SQL Server instance.
- If you choose to restore data by COS files, you need to store backup files to COS. See [Uploading backup file to COS](https://intl.cloud.tencent.com/document/product/238/32558)
- Full backups + log files restoration: The target instance and source instance don’t have to be on the same version, as long as the instance version is high.
- Full backups + differential backups restoration: The target instance and the source instance must be on the same version.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/), click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** and click **Create**.
![](https://main.qcloudimg.com/raw/ce56a4edf2e8f436d0bdfc56cb700e7d.png)
3. On the **Backup Restoration Settings** page, configure backup recovery task, and click **Create Task**.
 - Backup upload method: Local upload and download from COS.
 - Restoration mode: Full backup file, full backups + logs, full backups + differential backups.
![](https://main.qcloudimg.com/raw/b062c9e46e390ba6275bc9adfeb195af.png)
4. On the **Upload Backup File** page, upload backup files, and click **Save**.
 -. **Restoration mode** : When you select full backup file + logs or full backups + differential backups, there will be requirements for file names. You can click **Get Backup Command** to generate the corresponding backup command to generate the backup files that conforms to the file naming conventions.
    - Full backup file restoration: No requirements for backup file name.
    - Full backup file + differential backup restoration: 
      - Requirements for full backup file name: dbname_localtime_1full1_1noreconvery1.bak
       - Requirements for incremental backup file name: dbname_localtime_1diff1_1noreconvery1.bak
      - Requirements for the name of the last incremental backup file: dbname_localtime_1diff1_1reconvery1.bak
    - Full backups + logs restoration
      - Requirements for full backup file name: dbname_localtime_2full2_2noreconvery2.bak
      - Requirements for log name: dbname_localtime_2log2_2noreconvery2.bak
      - Requirements for the name of the last log: dbname_localtime_2log2_2reconvery2.bak
 - **Download Settings**: Support auto-restoration upon upload completion, and starting restoration manually.
    - Auto-restoration upon upload completion: The restoration task will be started immediately after you click **Save**.
    - Start restoration manually: click **Save**, manually start the task on **Backup and Restoration** page, and the uploaded backup files are only saved for 24 hours.
 ![](https://main.qcloudimg.com/raw/e6393af999e08129e2e6fdd098d07261.png)
5. On the **Backup and Restoration** page, you can view backup restoration task.
 - Full backup file restoration: The restoration task will automatically end after it  starts.
 - Full backups + differential backups and full backup file + logs: After full backup restoration is completed, uploading differential backups/logs in the form of subtasks will be supported. When the last file is uploaded successfully, the entire backup restoration task will automatically end.
