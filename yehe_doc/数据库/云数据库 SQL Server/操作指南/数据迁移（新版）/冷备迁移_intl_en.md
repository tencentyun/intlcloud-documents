This document describes how to migrate data from SQL Server databases of other cloud vendors or self-built SQL Server databases to TencentDB for SQL Server.

## Overview
Cold backup migration is based on data restoration from .bak backups and suitable for use cases where the business can be shut down to back up data. You can use cold backups to migrate data from SQL Server databases of other cloud vendors or self-built SQL Server databases to TencentDB for SQL Server.

TencentDB for SQL Server allows you to upload backups from your local device or upload them to the [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436/6222).

## Notes
- Before migration, please make sure that the SQL Server version of the target instance is the same as or later than that of the source instance.
- The name of the migrated database cannot be the same as that of the target TencentDB for SQL Server database.
- To migrate data using backups in COS, you need to upload backups to COS first. For more information, please see [Same-version Migration > Uploading backup file to COS](https://intl.cloud.tencent.com/document/product/238/32558).

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Backup Restoration** page, click **Create**.
![](https://main.qcloudimg.com/raw/ce56a4edf2e8f436d0bdfc56cb700e7d.png)
3. On the **Backup Restoration Settings** page, configure the backup restoration task, and click **Create Task**.
 - **Backup Upload Method**: you can upload the backup from your local device or download one from COS.
 - **Restoration Method**: full backups, full backups + logs, and full backups + differential backups are supported.
![](https://main.qcloudimg.com/raw/b062c9e46e390ba6275bc9adfeb195af.png)
4. On the **Upload Backup File** page, upload a backup, and click **Save**.
 - **Restoration Method**: if **Full backups + Logs** or **Full backups + Differential backups** is selected as the restoration method, the backup name must follow the naming conventions below. Click **Get Backup Command** to generate a backup command which can be used to create a backup with a name in the correct format.
    - Restoration from full backups: there is no requirement for the backup name format.
    - Restore from full backups + differential backups:
      - Full backup name format: dbname_localtime_1full1_1noreconvery1.bak
       - Incremental backup name format: dbname_localtime_1diff1_1noreconvery1.bak
      - The last incremental backup name format: dbname_localtime_1diff1_1reconvery1.bak
    - Restore from full backups + logs:
      - Full backup name format: dbname_localtime_2full2_2noreconvery2.bak
      - Log name format: dbname_localtime_2log2_2noreconvery2.bak
      - The last log name format: dbname_localtime_2log2_2reconvery2.bak
 - **Download Settings**: auto-restoration upon upload completion and starting restoration manually are supported.
    - Auto-restoration upon upload completion: the restoration task will start right after you click **Save**.
    - Start restoration manually: you need to manually start the restoration task on the **Backup Restoration** page after you click **Save**. Note that backups uploaded are retained for up to 24 hours.
 ![](https://main.qcloudimg.com/raw/e6393af999e08129e2e6fdd098d07261.png)
5. Go back to the **Backup Restoration** page and view the restoration task.
 - Restore from full backups: the restoration task will automatically end after the restoration process is completed.
 - Restore from full backups + differential backups or full backups + logs: after the restoration from full backups is completed, you can upload differential backups or logs to its subtask. After the last file is uploaded to the subtask, the whole restoration task will automatically end after the subtask is completed.
