### Why can't I logically back up and download by database or table?
After the [backup](https://intl.cloud.tencent.com/document/product/236/7513) feature was upgraded, both logical and physical backup files adopt the new compression algorithm, so some download-related features may be unavailable for the time being. In this case, you can perform logical backup of databases or tables in a sharding manner by selecting **Logical Backup** > **Specify Table** in the manual backup feature and download the completed backup file.

### Can data and log backup be disabled in TencentDB for MySQL?
No.
- Data backups can be retained for 7-732 days. The option for reducing backup frequency will be available after backup becomes a paid service, so that you can reduce the capacity occupied by backup files.
- Log backups can be retained for 7-732 days and the retention period cannot be longer than that of data backups.
>Billing for excessive backup capacity space successively started from 00:00 on December 2, 2019. For more information, please see [Backup Capacity Billing Description](https://intl.cloud.tencent.com/document/product/236/32344). Please develop a backup schedule and plan the backup capacity appropriately to avoid potential extra fees.

### Why cannot a downloaded backup file be decompressed/unpacked with tar?
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
For more information on installation of xtrabackup and qpress, please see [Restoring Database from Physical Backup File](https://intl.cloud.tencent.com/document/product/236/31910).

### How do I manually set up MySQL backup?
You can back up your MySQL data by offline migrating the data to the local file system. For more information, please see [Migrating Data Offline](https://intl.cloud.tencent.com/document/product/236/8464).


### How do I back up data on my own?
TencentDB for MySQL instances are fully backed up on a daily basis. You can also proactively back up your data using the multi-threaded quick import/export tool provided by TencentDB or using mysqldump. For more information, please see [Backup Mode](https://intl.cloud.tencent.com/document/product/236/7513).

### How do I view binlogs in MySQL?
- Download the binlogs from the console to the local file system such as a CVM instance.
- View them using mysqlbinlog. To do so, mysqlbinlog 3.4 or higher is required in MySQL 5.6.

### How do I achieve sync of real-time data in two TencentDB for MySQL instances in a local dual-backup architecture?
For this purpose, you can purchase [disaster recovery instances](https://intl.cloud.tencent.com/document/product/236/7272) in the TencentDB for MySQL Console.

