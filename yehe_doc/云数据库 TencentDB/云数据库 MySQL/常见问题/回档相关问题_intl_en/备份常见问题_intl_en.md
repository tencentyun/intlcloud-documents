### How is the backup capacity billed?
TencentDB for MySQL offers a certain amount of backup capacity free of charge based on the region, which is equivalent to the sum of storage capacity of all high-availability instances (including master and disaster recovery instances) in your region.
For pricing of excessive backup capacity, please see [TencentDB for MySQL Price Calculator](https://buy.cloud.tencent.com/price/cdb/calculator).

### How can I reduce the backup capacity costs?
- Delete manual backups that are no longer used (you can do so on the instance management > backup and restore page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb)). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup frequency and backup file retention period in the console, which should be at least twice a week).
>The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backup and log backup (binlog). Reducing the frequency of automatic backup and retention period will affect the rollback feature for instance data. Please configure backup appropriately based on your actual needs.
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of 7 days can meet the needs in most cases)

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7–732 days |
| Non-core, non-data businesses | 7 days |
| Archival businesses | 7 days. It is recommended to manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | 7 days. It is recommended to manually back up data based on your actual business needs and delete the backups promptly after use |

### How do I set up automatic backup?
You can set it up on the instance backup and restore page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/fc742f1fbf657be3b5138a521ae9cbda.png)

### How do I delete backup data?
- Automatic backup data cannot be deleted manually.
- Manual backup data can be deleted manually on the instance backup and restore page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).

### How do I cancel a manual backup task?
A running backup task cannot be canceled.

### What should I do if the backup file download is slow?
You are recommended to copy the download address on the instance backup and restore page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for download over the private network at a higher speed.
>- `wget` command format: wget -c 'backup file download address' -O custom filename.xb

### Can I download or restore backup files that exceed the retention period?
Expired backup sets will be automatically deleted and cannot be downloaded or restored.
- You are recommended to configure a reasonable backup retention period based on your business needs or download the backup files in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
- You can also manually back up the instance data in the console, and manual backup files will be retained permanently.
>Manual backup will also take up the backup capacity. Please use the backup capacity reasonably to avoid extra fees.

### Can data and log backup be disabled?
No. However, you can lower the backup frequency and delete manual backup data that is no longer used in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) to reduce the backup capacity.

### Why can't I initiate a manual backup task?
Please check the automatic backup time you set. If the instance is performing daily automatic backup, you cannot initiate a manual backup task.

### Why can't I logically back up and download by database or table?
After the [backup](https://intl.cloud.tencent.com/document/product/236/32340) feature was upgraded, both logical and physical backup files adopt the new compression algorithm, so some download-related features may be unavailable for the time being. In this case, you can perform logical backup of databases or tables in a sharding manner by selecting **Logical Backup** > **Specify Table** in the manual backup feature and download the completed backup file.

### Why can't a downloaded backup file be decompressed/unpacked with tar?
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
For more information on installation of xtrabackup and qpress, please see [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910).

### How do I back up data on my own?
TencentDB for MySQL instances are fully backed up on a daily basis. You can also proactively back up your data using the multi-threaded quick import/export tool provided by TencentDB or using mysqldump. For more information, please see [Backup Mode](https://intl.cloud.tencent.com/document/product/236/32340).

### How do I view binlogs in MySQL?
- Download the binlogs from the console to the local file system such as a CVM instance.
- View them using mysqlbinlog. To do so, mysqlbinlog 3.4 or higher is required in MySQL 5.6.

### How do I achieve sync of real-time data in two TencentDB for MySQL instances in a local dual-backup architecture?
For this purpose, you can purchase [Disaster Recovery Instance](https://intl.cloud.tencent.com/document/product/236/7272) in the TencentDB for MySQL Console.

