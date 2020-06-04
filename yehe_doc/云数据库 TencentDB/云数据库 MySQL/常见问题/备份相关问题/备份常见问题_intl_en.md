### How is the backup capacity billed?
TencentDB for MySQL offers a certain amount of backup capacity free of charge based on the region, which is equivalent to the sum of storage capacity of all high-availability edition and finance edition instances (including master and disaster recovery instances) in your region.
For pricing of the backup capacity exceeding the free tier, please see [TencentDB for MySQL Price Calculator](https://buy.cloud.tencent.com/price/cdb/calculator).

### How can I reduce the backup capacity costs?
- Delete manual backups that are no longer used (you can do so on the "instance management" > "backup and restore" page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb)). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and retention period in the console, and the frequency should be at least twice a week).
>The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backup and log backup (binlog). Reducing the frequency of automatic backup and retention period will affect the rollback time for instance data. Please configure backup appropriately based on your actual needs.
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of 7 days can meet the needs in most cases).

| Business Scenario             | Recommended Backup Retention Period                                                 |
| -------------------- | ------------------------------------------------------------ |
| Core businesses             | 7-732 days                                              |
| Non-core, non-data businesses | 7 days                                                      |
| Archival businesses             | 7 days. It is recommended to manually back up data based on your actual business needs and delete the backups promptly after use. |
| Testing businesses             | 7 days. It is recommended to manually back up data based on your actual business needs and delete the backups promptly after use. |

### How do I set up automatic backup?
You can set it up on the instance backup and restore page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/4df9e17b3d0d23d3e74f284e1e5efacd.png)

### How do I back up data on my own?
TencentDB for MySQL instances are fully backed up on a daily basis. For more information, see [Backup Mode](https://intl.cloud.tencent.com/document/product/236/32340). You can also back up data through the following ways:
- Use mysqldump.
- Use a third-party tool, such as Navicat Premium.
- [Log in to phpMyAdmin](https://intl.cloud.tencent.com/document/product/236/32341) and click **Export** on the navigation bar at the top.

### How do I restore or migrate a basic edition instance?
- Basic edition can be restored from snapshot backup only. For more information about instance migration, please see [Data Migration with Command Line Tool](https://intl.cloud.tencent.com/document/product/236/8464).

### Why does an error occur when I download data backup files?
You can use the `wget -c 'backup file download address' -O custom filename.xb` command for download. Note that the download address should be placed inside a pair of single quotation marks (') for the program to correctly identify.

### Can I restore the downloaded backups to another TencentDB for MySQL instance?
No. We recommend that you [use DTS to migrate a MySQL instance](https://intl.cloud.tencent.com/document/product/571/34103) to another.

### How do I delete backup data?
- Automatic backup data cannot be deleted manually.
- Manual backup data can be deleted manually in the MySQL console.
 1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click an instance name to enter the management page, and select **Backup and Restore** tab.
 2. Click **Delete** in the "Operation" column in the backup list.

### How do I cancel a backup task?
A running backup task cannot be canceled.

### What should I do if the backup download is slow?
We recommend that you copy the download address on the instance backup and restore page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for download over the private network at a higher speed.
> `wget` command format: wget -c 'backup file download address' -O custom filename.xb

### Can I download or restore backup files that exceed the retention period?
Expired backup sets will be automatically deleted and cannot be downloaded or restored.
- We recommend that you configure a backup retention period based on your business needs or download the backup files in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
- You can also manually back up the instance data in the console, and manual backup files will be retained permanently.
>Manual backup will also take up the backup capacity. Please use the backup capacity reasonably to avoid extra fees.

### Can data and log backup be disabled?
No. However, you can lower the backup frequency and delete manual backup data that is no longer used in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) to reduce the backup capacity usage.

### Why can't I initiate a manual backup task?
Please check the automatic backup time you set. If the instance is performing daily automatic backup, you cannot initiate a manual backup task.


### Why can't I logically back up and download by table?
After the [backup](https://intl.cloud.tencent.com/document/product/236/32340) feature was upgraded, both logical and physical backup adopt the new compression algorithm, so some download-related features may be unavailable for the time being. In this case, you can perform logical backup of tables by selecting **Logical Backup** > **Specify Table** in the manual backup feature and download the completed backup file.

### Why cannot a downloaded backup file be unpacked/decompressed with tar?
>Given that backup files in the new version adopt a new compression algorithm, they cannot be unpacked/decompressed using the original tar tool; instead, xbstream and qpress are required.

1. The downloaded backup file should be unpacked with xbstream (a packing/unpacking tool offered by Percona) first.
```
xbstream -x < test_import_57_backup_20181114115236.xb 
```
Then, a .qb file can be obtained, such as test_import_57_backup_20181114115236.sql.qb.
2. The .qb file needs to be decompressed with qpress.
```
qpress -d test_import_57_backup_20181114115236.sql.qp
```
Then, the complete backup file can be obtained, such as test_import_57_backup_20181114115236.sql.

### How do I download xbstream and qpress?
- xbstream is a subprogram of Percona XtraBackup. Before using it, you need to install Percona XtraBackup with `yum` or binary installation package.
- Download qpress [here](http://www.quicklz.com/) and extract the qpress binary files by running the tar command:
For more information on installation of XtraBackup and qpress, see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910)

### How do I view binlogs in MySQL?
- Download the binlogs from the console to the local file system such as a CVM instance.
- View them using mysqlbinlog. To do so, mysqlbinlog v3.4 or higher is required in MySQL v5.6.

### How do I sync real-time data in two instances with an intra-city active-active solution?
For this purpose, you can purchase [disaster recovery instances](https://intl.cloud.tencent.com/document/product/236/7272) in the TencentDB for MySQL Console.

