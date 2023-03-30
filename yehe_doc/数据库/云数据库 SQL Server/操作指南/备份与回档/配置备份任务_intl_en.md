Backup task settings include global variables of manual and scheduled backup, such as the backup file format and backup task execution option.
This document describes how to configure a backup task in the console.

>?Only two-node 2017/2019 instances support configuring backup task execution options.


## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://qcloudimg.tencent-cloud.cn/raw/ca70f964e8a1fd762347335071e14aed.png)
3. On the **Backup Management** tab, click **Backup Task Settings**.
4. Specify configuration items in the pop-up window and click **Save**.
   - **Upload Backup File**: You can specify the format of backup files (**Archive file** or **Unarchived files**). By default, backup files (i.e., .bak files) will be archived into a .tar file and then uploaded to COS. If you select **Unarchived files** as the backup file format, the .bak file of each database in the instance will be directly uploaded to COS without being archived.
   - **Execute Backup Task**: You can decide whether to back up on the primary or replica node. By default, data is backed up on the primary node.

