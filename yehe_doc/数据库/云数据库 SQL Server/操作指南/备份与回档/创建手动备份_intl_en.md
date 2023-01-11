TencentDB for SQL Server supports automatic backup and manual backup. This document describes how to create a manual backup in the console.
>!
>- Backup files are stored in a separate backup space and do not occupy the local disk space of the instance.
>- Do not perform DDL operations during the backup process to avoid backup failure caused by table locking.
>- Back up your data during off-peak hours.
>- Backup may take a long time if the data volume is large.
>- We recommend you not modify the restoration mode for Basic Edition instances, which is **full** mode by default. If you modify it to the **simple** mode, the log chain will be broken and manual backup will fail.

## Prerequisites
Before performing manual backup, make sure that you have created a database. For more information, see [Creating Database](https://intl.cloud.tencent.com/document/product/238/35780).

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://qcloudimg.tencent-cloud.cn/raw/e89f412c5ff806dfdc55258022f61c25.png)
3. On the **Backup Management** tab, click **Manual Backup**.
4. In the pop-up window, enter the backup name, select the backup policy, and click **OK**.
   - **Backup Name**: Set the manual backup name, which can contain up to 128 letters, digits, or underscores.
   - **Backup Policy**:
     - Instance backup: Backs up all databases in the entire instance.
     - Multi-database backup: Backs up selected databases.
>!The time it takes to complete the backup is subject to the backup file size and ranges from around 5 to 120 minutes.
>
![](https://qcloudimg.tencent-cloud.cn/raw/02705d60644483f18ec698da844bc814.png)
5. After the manual backup is completed, you can query it in the backup list on the **Backup Management** tab.
