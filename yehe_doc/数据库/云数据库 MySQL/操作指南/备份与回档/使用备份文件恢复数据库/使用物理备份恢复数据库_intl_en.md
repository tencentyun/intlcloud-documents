
## Overview
>?In order to save the storage capacity, physical and logical backups in TencentDB for MySQL are to be compressed with qpress and then packed with xbstream offered by Percona.
>
The open-source Percona XtraBackup can be used to back up and restore databases. This document describes how to use XtraBackup to restore a physical backup file of TencentDB for MySQL instance to a self-built database on CVM.
- XtraBackup only supports the Linux operating system.
- For more information about how to restore data in Windows, see [Offline Migration of Data > Data Migration with Command Line Tool](https://intl.cloud.tencent.com/document/product/236/8464).

## Prerequisites
- Download and install XtraBackup.
 - For MySQL 5.6 and 5.7, download Percona XtraBackup 2.4.6 or above at [Percona's official website](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). For more information on installation, see [Percona XtraBackup 2.4 documentation](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
 - For MySQL 8.0, download Percona XtraBackup 8.0.22-15 or above at [Percona's official website](https://www.percona.com/downloads/Percona-XtraBackup-LATEST/#). For more information on installation, see [Percona XtraBackup 8.0 documentation](https://www.percona.com/doc/percona-xtrabackup/8.0/installation.html).
- Supported instance architectures: two-node or three-node MySQL
- Instances with data encryption enabled cannot be restored from a physical backup.

## Directions
>?This document takes a CVM instance running CentOS and a MySQL v5.7 instance as an example.
>
### Step 1. Download the backup file
You can download data backups and log backups of TencentDB for MySQL instances in the console.
>?Each IP can have up to 10 download links by default, with a download speed limit of 20–30 Mbps each.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the **Backup and Restore** > **Data Backup List** tab, locate the backup file to be downloaded and click **Download** in the **Operation** column.
3. Copy the download address in the pop-up dialog box, [log in to the Linux CVM in the same VPC as the TencentDB instance](https://intl.cloud.tencent.com/document/product/213/10517), and run `wget` to download the file over the high-speed private network.
>?
>- You can also click **Download** to download it directly. However, this may take longer.
>- `wget` command format: wget -c 'backup file download address' -O custom filename.xb 
>
The example is as follows:
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O /data/test.xb
```

### Step 2. Restore data
#### 2.1 Unpack the backup file
Run the `xbstream` command to unpack the backup file to the target directory.
```
xbstream -x --parallel=2  -C /data/mysql < /data/test.xb
```
>?
>- The target directory `/data/mysql` is used as an example in this document. You can replace it with the directory you actually use to store the backup file.
>- Replace `/data/test.xb` with your backup file.
>
The unpacking result is as shown below:
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

#### 2.2 Decompress the backup file
1. Download qpress by running the following command:
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10. http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?If an error is displayed during the `wget` download, you can go to [QuickLZ's official website](http://www.quicklz.com/) to download qpress locally and upload it to the Linux CVM instance. For more information, see [Uploading Files from Linux or MacOS to Linux CVM via SCP](https://intl.cloud.tencent.com/document/product/213/2133).
>
2. Extract the qpress binary files by running the following command.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Decompress all `.qp` files in the destination directory by running the following qpress command:
```
xtrabackup --decompress --target-dir=/data/mysql
```
>?
>- `/data/mysql` is the target directory where the backup file was previously stored. You can replace it with the directory you actually use.
>- The `--remove-original` option is supported only in Percona Xtrabackup v2.4.6 and later.
>- `xtrabackup` won't delete the original files during decompression by default. If you want to delete them upon the completion of decompression, add the `--remove-original` parameter to the above command.
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

#### 2.3 Prepare the backup file
After a backup file is decompressed, you need to execute the "apply log" operation by running the following command.
```
xtrabackup --prepare  --target-dir=/data/mysql
```
If the execution result contains the following output, it means that the preparation succeeded.
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
		
#### 2.4 Modify the configuration file
1. Run the following command to open the `backup-my.cnf` file.
```
vi /data/mysql/backup-my.cnf
```
>?The target directory `/data/mysql` is used as an example in this document. You can replace it with the directory you actually use.
>
2. Given the existing version issues, the following parameters need to be commented out from the extracted file `backup-my.cnf`.
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 

 ![](https://qcloudimg.tencent-cloud.cn/raw/6d56154cb19d16b56520199290a0c574.png)

#### 2.5 Modify file attributes
Modify file attributes and check whether files are owned by the `mysql` user.
```
chown -R mysql:mysql /data/mysql
```
![](https://qcloudimg.tencent-cloud.cn/raw/12fbe7f70fefa19fd7af5ac2f95bfdb8.png)

### Step 3. Start the mysqld process and log in for verification
1. Start the mysqld process.
```
mysqld_safe --defaults-file=/data/mysql/backup-my.cnf --user=mysql --datadir=/data/mysql &
```
2. Log in to the client for verification.
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

## Backup FAQs
See [Common Issues](https://intl.cloud.tencent.com/document/product/236/9036) and [Failure Reasons](https://intl.cloud.tencent.com/document/product/236/34394).
