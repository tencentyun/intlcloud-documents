
## Overview
>?To save the storage space, physical and logical backups in TencentDB for MySQL will be compressed with qpress and then packed with xbstream offered by Percona.
>
The open-source Percona XtraBackup can be used to back up and restore databases. This document describes how to use XtraBackup to restore a physical backup file of TencentDB for MySQL instance to a CVM-based self-built database.
>!If you use the TDE or Instant DDL feature, you cannot restore data from a physical backup in a self-built system.
>
- XtraBackup only supports Linux but not Windows.
- For more information about how to restore data in Windows, see [Offline Data Migration > Data Migration with Command Line Tool](https://intl.cloud.tencent.com/document/product/236/8464).

## Prerequisites
- Download and install XtraBackup.
 - For MySQL 5.6 and 5.7, download Percona XtraBackup 2.4.6 or later at [Percona official website](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). For more information on installation, see [Percona XtraBackup 2.4 documentation](https://docs.percona.com/percona-xtrabackup/2.4/installation/yum_repo.html).
 - For MySQL 8.0, download Percona XtraBackup 8.0.22-15 or later at [Percona official website](https://www.percona.com/downloads/Percona-XtraBackup-LATEST/#). For more information on installation, see [Percona XtraBackup 8.0 documentation](https://docs.percona.com/percona-xtrabackup/8.0/installation/yum_repo.html).
- Supported instance architectures: two-node or three-node MySQL
- Instances with TDE enabled cannot be restored from a physical backup.

>?This document takes a CVM instance on CentOS and a MySQL 5.7 instance as an example.
>

## Step 1. [Download the backup file](id:XZBFWJ)
You can download data backups and log backups of TencentDB for MySQL instances in the console.
>?Each IP can have up to 10 download links by default, with a download speed limit of 20–30 Mbps each.

1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the **Backup and Restoration** > **Data Backup List** tab, locate the backup file to be downloaded and click **Download** in the **Operation** column.
3. Copy the download address in the pop-up dialog box, log in to the Linux CVM in the same VPC as the TencentDB instance as instructed in [Customizing Linux CVM Configurations](https://www.tencentcloud.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8), and run `wget` to download the file over the high-speed private network.
>?
>- You can also click **Download** to download it directly. However, this may take a longer time.
>- `wget` command format: wget -c 'backup file download address' -O custom filename.xb 
>
Below is a sample:
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O /data/test.xb
```

## Step 2. Download the backup decryption key (required only if the backup encryption feature is enabled)
You can download data backups and decryption keys of TencentDB for MySQL instances in the console.
>?A decryption key is generated for each database backup separately. If the backup encryption feature is enabled, you need to download and save the backup file together with the decryption key.

1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the **Backup and Restoration** > **Data Backup List** tab, locate the decryption key of the backup file to be downloaded and click **Download Key** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/A8BA028_1.png)

## Step 3. Restore data
### 3.1 Unpack the backup file
Run the `xbstream` command to unpack the backup file to the target directory.
```
xbstream -x --decrypt=AES256 --encrypt-key-file=<backup key file> --parallel=2  -C /data/mysql < /data/test.xb
```
>?
>- The target directory `/data/mysql` is used as an example in this document. You can replace it with the directory you actually use to store the backup file.
>- Replace `/data/test.xb` with your backup file.
>
The unpacking result is as shown below:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/K4wr727_f981522847f38b10bfe0a59c7234b7ba.png">

### 3.2 Decompress the backup file
1. Download qpress by running the following command.
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar
```
>?If an error is displayed during the `wget` download, you can click [here](https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar) to download qpress locally and upload it to the Linux CVM instance. For more information, see [Uploading Files from Linux or MacOS to Linux CVM via SCP](https://intl.cloud.tencent.com/document/product/213/2133).
>
2. Extract the qpress binary files by running the following command.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Then, decompress all `.qp` files in the target directory by running the following command:
```
xtrabackup --decompress --target-dir=/data/mysql
```
>?
>- `/data/mysql` is the target directory where the backup file was previously stored. You can replace it with the directory you actually use.
>- The `--remove-original` option is supported only in Percona Xtrabackup 2.4.6 and later.
>- `xtrabackup` won't delete the original files during decompression by default. If you want to delete them upon the completion of decompression, add the `--remove-original` parameter to the above command.
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

### 3.3 Prepare the backup file
After a backup file is decompressed, perform the `apply log` operation by running the following command.
```
xtrabackup --prepare  --target-dir=/data/mysql
```
If the execution result contains the following output, it means that the `prepare` operation succeeded.
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
		
### 3.4 Modify the configuration file
1. Run the following command to open the `backup-my.cnf` file.
```
vi /data/mysql/backup-my.cnf
```
>?The target directory `/data/mysql` is used as an example in this document. You can replace it with the directory you actually use.
>
2. Given the existing version issues, the following parameters need to be commented out from the extracted `backup-my.cnf` file.
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 

 ![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

### 3.5 Modify file attributes
Modify file attributes and check whether files are owned by the `mysql` user.
```
chown -R mysql:mysql /data/mysql
```
![](https://staticintl.cloudcachetci.com/yehe/backend-news/dk6k301_EeLm919_6.png)

## Step 4. Start the mysqld process and log in for verification
1. Start the mysqld process.
```
mysqld_safe --defaults-file=/data/mysql/backup-my.cnf --user=mysql --datadir=/data/mysql &
```
2. Log in to the MySQL client for verification.
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

## FAQs About Backup
See [FAQs](https://intl.cloud.tencent.com/document/product/236/9036) and [Troubleshooting](https://intl.cloud.tencent.com/document/product/236/34394).

