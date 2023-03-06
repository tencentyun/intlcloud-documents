This document describes how to migrate data from SQL Server databases in other cloud vendors and self-built SQL Server databases to TencentDB for SQL Server in the TencentDB for SQL Server Console.

## Overview
Cold backup migration restores data from .bak, .tar, or .zip files, which is applicable to data migration from SQL Server databases in other cloud vendors and self-built SQL Server databases to TencentDB for SQL Server, and backup can be performed when the system is shut down.

TencentDB for SQL Server supports migrating data to TencentDB for SQL Server via [COS] (https://intl.cloud.tencent.com/document/product/436/6222) files or locally uploaded files.

>! To restore backups with .zip and .tar files, you need to ensure that the decompressed files are in the same path folder as the zip and tar files before decompression. If they are in the path folder of the next layer, they cannot be parsed.

## Use Limits
- Before migration, make sure that the version of the target SQL Server instance is not lower than that of the source instance.
- The name of the migrated database can’t be the same as that of the TencentDB for SQL Server instance.
- If you choose to restore data by COS files, you need to store backup files to COS. See [Same-Version Migration > Uploading the Backup File to COS](https://intl.cloud.tencent.com/document/product/238/32558)
- Full backups + log files restoration: The target instance and source instance don’t have to be on the same version, as long as the instance version is high.
- Full backups + differential backups restoration: The target instance and the source instance must be on the same version.

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/), and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** and click **Create**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vy7u130_1.png)
3. On the backup restoration creation tab, complete **Backup Restoration Settings**, and click **Create Task**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cwWv383_2.png)

| Parameter | Description |
|---------|---------|
| Task Name | The task name can contain up to 60 letters, digits, or underscores. |
| Backup upload method | Local upload and download from COS. |
| Restoration mode | Full backup file, full backups + logs, full backups + differential backups. |

>? To cancel the creation of backup restoration task, click **Cancel**, and then the task record will not be retained in the backup restoration task list.

4. On the backup restoration creation tab, upload the backup file, and click **Save**.
Backup upload method falls into the following 2 types based on step 3.
<dx-tabs>
::: Direct backup upload
![](https://staticintl.cloudcachetci.com/yehe/backend-news/sMUL636_3.png)

| Parameter | Description |
|---------|---------|
| Restoration mode | When you select full backup file + logs or full backups + differential backups, there will be requirements for file names. You can click **Get Backup Command** to generate the corresponding backup command to generate the backup files that conform to the file naming conventions.<ul><li>Full backup file restoration: No requirements for backup file name.<li>Full backup file + differential backup restoration:<br>Requirements for full backup file name: dbname_localtime_1full1_1noreconvery1.bak<br>Requirements for incremental backup file name: dbname_localtime_1diff1_1noreconvery1.bak<br>Requirements for the name of the last incremental backup file: dbname_localtime_1diff1_1reconvery1.bak<li>Full backups + logs restoration <br>Requirements for full backup file name: dbname_localtime_2full2_2noreconvery2.bak<br>Requirements for log name: dbname_localtime_2log2_2noreconvery2.bak<br>Requirements for the name of the last log: dbname_localtime_2log2_2reconvery2.bak</ul> |
| Backup upload | Click **Upload** to import the backup file locally |
| Database renaming | It is optional. Once enabled, the original database name in the backup file will be reset and then designated as the new database name after it is restored to the cloud database, and you need to enter these two names.<dx-alert infotype="explain" title="">
- Up to 5 databases can be renamed.
- If there is a database that is not renamed in the original database, it will remain unchanged after the backup restoration task is completed.
</dx-alert>|
| Download setting | Support auto-restoration upon upload completion, and starting restoration manually.<ul><li>Auto-restoration upon upload completion: Click **Save** to enable restoration task.<li>Start restoration manually: Click **Save**, manually start the task on **Backup and Restoration** page, and the uploaded backup files are only saved for 24 hours.</ul>|

>?On the backup file upload page, you can click **Previous** to review and edit the backup restoration settings.
>- Return to backup restoration settings page, click **Next** to upload the backup file if no more operation is needed. To cancel the task, click **Cancel**.
>- Return to backup restoration settings page, you can click **Edit** to edit the task name, backup upload method, and restoration mode. After you click **Edit**, the upload page content of the backup file in step 2 will be cleared, but you can click **Create Task** to enter the next step for resetting.
>
>:::
::: Download File from COS

| Parameter | Description |
|---------|---------|
| Restoration mode | When you select full backup file + logs or full backups + differential backups, there will be requirements for file names. You can click **Get Backup Command** to generate the corresponding backup command to generate the backup files that conform to the file naming conventions.<ul><li>Full backup file restoration: No requirements for backup file name.<li>Full backup file + differential backup restoration:<br>Requirements for full backup file name: dbname_localtime_1full1_1noreconvery1.bak<br>Requirements for incremental backup file name: dbname_localtime_1diff1_1noreconvery1.bak<br>Requirements for the name of the last incremental backup file: dbname_localtime_1diff1_1reconvery1.bak<li>Full backups + logs restoration <br>Requirements for full backup file name: dbname_localtime_2full2_2noreconvery2.bak<br>Requirements for log name: dbname_localtime_2log2_2noreconvery2.bak<br>Requirements for the name of the last log: dbname_localtime_2log2_2reconvery2.bak</ul> |
| Original COS file link | Paste original COS file link |
| Database renaming | It is optional. Once enabled, the original database name in the backup file will be reset and then designated as the new database name after it is restored to the cloud database, and you need to enter these two names.<dx-alert infotype="explain" title="">
- Up to 5 databases can be renamed.
- If a database in the original database was not renamed, its name will remain unchanged after the backup restoration task is completed.
</dx-alert>|

>?On the backup file upload page, you can click **Previous** to review and edit the backup restoration settings.
>- Return to backup restoration settings page, click **Next** to upload the backup file if no more operation is needed. To cancel the task, click **Cancel**.
>- Return to backup restoration settings page, you can click **Edit** to edit the task name, backup upload method, and restoration mode. After you click **Edit**, the the content of the backup file upload page in step 2 will be cleared, but you can click **Create Task** to enter the next step for resetting.
>
>:::
</dx-tabs>

5. View backup restoration task in the task list
 - Full backup file restoration: The restoration task will automatically end after it starts.
 - Full backups + differential backups and full backup file + logs: After full backup restoration is completed, uploading differential backups/logs in the form of subtasks will be supported. When the last file is uploaded successfully, the entire backup restoration task will automatically end.

## Best Practices
TencentDB for SQL Server supports cross-account backup restoration; that is, you can get the backup file download URL of an instance under account A, and then restore data under account B. The following describes how to do this.
>!
>- After getting the backup file download URL of an instance under account A, perform backup restoration under account B. The two accounts need to be in the same region.
>- This backup restoration mode currently supports backup files in .bak format.
>- To use intra-region cross-account backup restoration, the form of the backup file obtained in the console must be unarchived file.
>- .tar and .zip files will be supported for backup restoration in January 2023, subject to change as displayed in the console.
>- Currently, the backup file download URL needs to be decoded as detailed [below](#jmcz).

#### Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/) with account A, and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **Backup Management** tab and click **View Details** in the **Operation** column of the target unarchived file in the data backup list.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HJuf508_4.png)
3. Click **Download** in the pop-up window and copy the download URL.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/kF8R259_5.png)
4. Click [Decode Online](http://www.ab173.com/enc/urlencode.php) and decode the copied URL on the page redirected to.
>?Only the first part of the download URL needs to be decoded.
>**Sample**: Suppose a download URL is:
>`https://sqlserver-bucket-bj-1258415541.cos.ap-beijing.myqcloud.com/1312368346%2fsqlserver%2fmssql-8e5hjaiq%2fbackup%2fautoed_instance_58013012_AdventureWorksDW2012_2022_12_29023915.bak?**********`
>You only need to select the URL part until `.bak?` for decoding. Then, combine the output string with the second part of the URL to get the final URL for cross-account backup restoration.
>For the above sample URL, take the following part for decoding:
>`https://sqlserver-bucket-bj-1258415541.cos.ap-beijing.myqcloud.com/1312368346%2fsqlserver%2fmssql-8e5hjaiq%2fbackup%2fautoed_instance_58013012_AdventureWorksDW2012_2022_12_29023915.bak?`
>It is decoded to:
>`https://sqlserver-bucket-bj-1258415541.cos.ap-beijing.myqcloud.com/1312368346/sqlserver/mssql-8e5hjaiq/backup/autoed_instance_58013012_AdventureWorksDW2012_2022_12_29023915.bak?`
>Then, the final URL for cross-account backup restoration is as follows:
>`https://sqlserver-bucket-bj-1258415541.cos.ap-beijing.myqcloud.com/1312368346/sqlserver/mssql-8e5hjaiq/backup/autoed_instance_58013012_AdventureWorksDW2012_2022_12_29023915.bak?**********`
5. Copy the URL for cross-account backup restoration, log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/) with account B, and click an instance ID in the instance list to enter the instance management page.
6. On the instance management page, select the **Backup and Restoration** and click **Create**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dS9u451_7.png)
7. In the pop-up window, configure the following items and click **Create Task**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wRC7329_8.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Task name</td>
<td>Enter the task name, which can contain up to 60 letters, digits, or underscores.</td></tr>
<tr>
<td>Backup Upload Method</td>
<td>Select **Download File from COS**.</td></tr>
<tr>
<td>Restoration Mode</td>
<td>Select **Full Backup File**.</td></tr>
</tbody></table>
8. In the **Upload Backup File** window, paste the URL and click **Save**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/zuCV574_9.png)
9. Go to the **Backup and Restoration** tab, find the backup task you just created, and click **Start** in the **Operation** column.
10. In the backup and restoration list, check the migration task status. When it becomes **Migration succeeded**, the cross-account backup restoration is completed.
