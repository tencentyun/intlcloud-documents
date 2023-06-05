
TDSQL-C for MySQL automatically backs up data based on the default backup settings. You can modify the automatic or manual backup settings in the console. You can also view the backup files and relevant information in the backup list.

This document describes how to view the list of backup files in the console.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top of the page and click the ID or **Manage** in the **Operation** column of the target cluster to enter the cluster management page.
3. On the **Backup Management** tab, view backup tasks in the data or binlog backup list.
![](https://qcloudimg.tencent-cloud.cn/raw/56ebf1af8b6614df60964cbbf62c3e05.png)
  - Information in the data backup list: File name/alias, backup time, start time, end time, backup type, backup mode, backup size, status, and operation.
  - Information in the binlog backup list: File name, binlog backup start time, binlog backup end time, backup size, and operation.
  - You can filter backup files by time (all, today, yesterday, past 7 or 30 days, or custom time period).
  - You can search for backup files in the search box on the right by file name, alias, backup mode, and backup type.
![](https://qcloudimg.tencent-cloud.cn/raw/e9de4591697baa5956ec53d643db16dd.png)

## FAQs
#### Can I download or restore backup files that exceed the retention period?
Expired backup files (including data and binlog backup files) will be automatically deleted and cannot be downloaded or restored.
- You can download logical (full) and snapshot (full) backup files in the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
- You can manually back up data in the console. Manual backup files will be retained in the backup list as long as they are not manually deleted.
>?Backups will take up the backup space. We recommend that you plan the usage of the backup space appropriately to reduce costs.

#### Can I delete backups manually?
- Automatic backups cannot be deleted manually. They will be automatically deleted after the retention period ends, which is 7 days and can be customized as needed. For more information, see [Setting Backup Retention Period](https://www.tencentcloud.com/document/product/1098/48396). 
- Manual backups can be manually deleted from the backup list in the TDSQL-C for MySQL console.

#### How can I reduce the backup capacity cost?
- Delete manual backups that are no longer used as instructed in [Deleting Backup](https://www.tencentcloud.com/document/product/1098/48394).
- Reduce the automatic backup retention period as needed to implement the regular deletion of automatic backups. For more information, see [Setting Backup Retention Period](https://www.tencentcloud.com/document/product/1098/48396).

