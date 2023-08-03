## Overview
>?To save the storage space, physical and logical backups in TencentDB for MySQL will be compressed with qpress and then packed with xbstream offered by Percona.

TencentDB for MySQL supports logical backup as described in [Backing up Databases](https://intl.cloud.tencent.com/document/product/236/37796). In the console, you can manually create logical backup files of an entire instance or specified databases/tables and download them. This document describes how to manually restore data from logical backup files.

- The restoration method described in this document only applies to Linux.
- For more information about how to restore data in Windows, see [Offline Data Migration > Data Migration with Command Line Tool](https://www.tencentcloud.com/document/product/236/8464).
- Supported instance architectures: two-node or three-node MySQL

## Directions
### Step 1. Download the backup file
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the **Backup and Restoration** > **Data Backup List** tab, locate the backup file to be downloaded and click **Download** in the **Operation** column.
3. We recommend that you copy the download link in the pop-up dialog box, log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for download over the private network at a higher speed. For more information, see [Customizing Linux CVM Configurations](https://www.tencentcloud.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)
>?
>- You can also click **Download** to download it directly. However, this may take a longer time.
>- `wget` command format: wget -c 'backup file download address' -O custom filename.xb
>
Below is a sample:
```
wget -c 'https://mysql-database-backup-bj-118.cos.ap-beijing.myqcloud.com/12427%2Fmysql%2F42d-11ea-b887-6c0b82b%2Fdata%2Fautomatic-delete%2F2019-11-28%2Fautomatic%2Fxtrabackup%2Fbk_204_10385%2Fcdb-1pe7bexs_backup_20191128044644.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3D1%26q-sign-time%3D1574269%3B1575417469%26q-key-time%3D1575374269%3B1517469%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dfb8fad13c4ed&response-content-disposition=attachment%3Bfilename%3D%2141731_backup_20191128044644.xb%22&response-content-type=application%2Foctet-stream' -O test0.xb
```

### Step 2. Unpack the backup file
Unpack the backup file with xbstream.
>? xbstream can be downloaded at [Percona official website](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Select Percona XtraBackup 2.4.6 or later. For more information on installation, see [Installing Percona XtraBackup on Red Hat Enterprise Linux and CentOS](https://docs.percona.com/percona-xtrabackup/2.4/installation/yum_repo.html).
>
```
xbstream -x < test0.xb
```
>?Replace `test0.xb` with your backup file.
>
The unpacking result is as shown below:
![](https://main.qcloudimg.com/raw/61b53f4f54ffd2fbe7c0d1b3423255b0.png)

### Step 3. Decompress the backup file
1. Download qpress by running the following command.
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar
```
>? If an error is displayed during the `wget` download, you can click [here](https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar) to download qpress locally and upload it to the Linux CVM instance. For more information, see [Uploading Files from Linux or MacOS to Linux CVM via SCP](https://www.tencentcloud.com/document/product/213/2133).
>
2. Extract the qpress binary files by running the following command.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Decompress the backup file with qpress.
```
qpress -d cdb-jp0zua5k_backup_20191202182218.sql.qp .
```
>?Find the backup file with `.sql.qp` extension by decompression time and replace `cdb-jp0zua5k_backup_20191202182218` with its filename.
>
The decompressing result is as shown below:
![](https://main.qcloudimg.com/raw/355557bc949fd86af8346d8a44dc4551.png)

### Step 4. Import the backup file into the target database
Import the .sql file into the target database by running the following command:
```
mysql -uroot -P3306 -h127.0.0.1 -p < cdb-jp0zua5k_backup_20191202182218.sql
```
>?
>- This document takes importing into a local MySQL instance with port 3306 as an example. You can replace it as needed.
>- Replace `cdb-jp0zua5k_backup_20191202182218.sql` with the .sql file extracted by qpress.

