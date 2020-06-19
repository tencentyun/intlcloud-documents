### How is backup capacity billed?
TencentDB for MySQL offers a certain amount of backup capacity free of charge based on the region, which is equivalent to the sum of storage capacity of all high-availability edition and finance edition instances (including master and disaster recovery instances) in the region.
For pricing details about backup capacity exceeding the free tier, see [TencentDB for MySQL Price Calculator](https://buy.cloud.tencent.com/price/cdb/calculator).

### How can I reduce the backup capacity cost?
- Delete manual backups that are no longer used (you can do so via "Instance Management" > "Backup and Restore" page in [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb)). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and retention period in the console, and the frequency should be at least twice a week).
>The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backup and log backup (binlog). The rollback time for instance data will be affected if you reduce the automatic backup frequency and retention period. Please configure them properly as needed.
>
- Reduce the retention period of data and log backups for non-core businesses (7-day retention period can meet the requirements in most scenarios).

| Business Scenario             | Recommended Backup Retention Period                                                 |
| -------------------- | ------------------------------------------------------------ |
| Core businesses             | 7-732 days                                              |
| Non-core and non-data businesses | 7 days                                                      |
| Archive businesses             | 7 days. We recommend that you manually back up data based on business needs and delete it promptly after use. |
| Testing businesses             | 7 days. We recommend that you manually back up data based on business needs and delete it promptly after use. |

### How do I configure automatic backup?
You can configure it on the instance backup and restore page in [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/4df9e17b3d0d23d3e74f284e1e5efacd.png)

### How do I back up data on my own?
TencentDB for MySQL instances are fully backed up on a daily basis. For more information, see [Backup Mode](https://intl.cloud.tencent.com/document/product/236/32340). You can also back up data by the following methods:
- Use mysqldump.
- Use a third-party tool, such as Navicat Premium.
- [Log in to phpMyAdmin](https://intl.cloud.tencent.com/document/product/236/32341) and click **Export** on the navigation bar at the top.

### How do I restore or migrate a basic edition instance backup?
- Basic edition instance only supports snapshot backup. For more information, please see [Data Migration with Command Line Tool](https://intl.cloud.tencent.com/document/product/236/8464).

### Why does an error occur when I download data backup files?
You can use the `wget -c 'backup file download address' -O custom filename.xb` command for download. Note that the download address should be placed inside a pair of single quotation marks (') for the program to identify.

### Can I restore the downloaded backups to another TencentDB for MySQL instance?
No. We recommend that you [use DTS to migrate a MySQL instance](https://intl.cloud.tencent.com/document/product/571/34103).

### How do I delete backup data?
- Automatic backup data cannot be deleted manually.
- Manual backup data can be deleted manually in the MySQL console.
 1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name to enter the management page, and select the **Backup and Restore** tab.
 2. Click **Delete** in the "Operation" column in the backup list.

### How do I cancel a backup task?
A running backup task cannot be canceled.

### What should I do if the backup download is slow?
We recommend that you copy the download address on the instance backup and restore page in [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for high-speed download over the private network.
> `wget` command format: wget -c 'backup file download address' -O custom filename.xb

### Can I download or restore backup files that exceed the retention period?
Expired backup sets will be deleted automatically and cannot be downloaded or restored.
- We recommend that you configure a backup retention period based on business needs or download the backup files locally via [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
- You can also manually back up instance data in the console. Manual backup will be retained permanently.
>Manual backup will also take up the backup capacity. Please use the backup capacity properly to avoid extra fees.

### Can I disable data and log backups?
No. However, you can reduce the backup frequency and delete manual backup no longer used via [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) to lower the capacity usage.

### Why cannot I initiate a manual backup task?
Please check the automatic backup time you configured. If the instance is performing the daily automatic backup, you cannot initiate a manual backup task.


### Why cannot I logically back up and download by tables?
After the [backup](https://intl.cloud.tencent.com/document/product/236/32340) feature was upgraded, both logical and physical backup adopt the new compression algorithm, and some download features may be currently unavailable. To perform logical backups by tables, you can select **Logical backup** > **Specify table** in manual backup and download the completed backup file.

### Why cannot a downloaded backup file be unpacked/decompressed with tar?
>Because backup files in the latest version adopt a new compression algorithm, they cannot be unpacked/decompressed using the original tar tool. Instead, xbstream and qpress are required.

For details about how to unpack/decompress with xbstream and qpress, please see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910) and [Restoring Database from Logical Backup](https://intl.cloud.tencent.com/document/product/236/31909).
qpress -d test_import_57_backup_20181114115236.sql.qp
```
The complete backup file can be obtained, such as test_import_57_backup_20181114115236.sql.

### How do I download xbstream and qpress?
- xbstream is a subprogram of Percona XtraBackup. To use it, you need to install Percona XtraBackup from binaries or `yum` repositories.
- Download qpress [here](http://www.quicklz.com/) and extract the qpress binary files by running the tar command:
For more information on XtraBackup and qpress installation, see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910)

### How do I view binlogs in MySQL?
- Download binlogs from the console locally to, for example, the CVM instance.
- View them using the mysqlbinlog command. For the local server to view binlogs, MySQL v5.6 requires mysqlbinlog v3.4 or higher.

### How do I sync real-time data in two instances with an intra-city active-active architecture configured?
You can purchase [disaster recovery instances](https://intl.cloud.tencent.com/document/product/236/7272) in the TencentDB for MySQL Console.

