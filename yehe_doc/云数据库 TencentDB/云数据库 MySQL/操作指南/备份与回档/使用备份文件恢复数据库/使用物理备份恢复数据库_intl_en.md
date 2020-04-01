## Operation Scenarios
The open-source software tool Percona Xtrabackup can be used to back up and restore databases. This document describes how to use XtraBackup to restore a physical backup file of a TencentDB for MySQL instance to a self-built database on another server.

> XtraBackup only supports Linux but not Windows.


## Prerequisites
- Download and install XtraBackup.
XtraBackup can be downloaded at [Percona's official website](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Please select Percona XtraBackup 2.4.6 or higher. For more information on how to install the tool, please see [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
- Supported instance version: TencentDB for MySQL 5.5, 5.6, and 5.7 High-Availability Edition.
- Instances with data encryption enabled cannot be restored from a physical backup.

## Directions
### Step 1. Download the backup file
You can download data backups and log backups of TencentDB for MySQL instances in the console.
>Each IP can have up to 10 download links by default, with a download speed limit of 20–30 Mbps each.
>
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. On the instance management page, click **Backup and Restore** > **Data Backup List**, select the backup to download, and then click **Download** in the "Operation" column.
3. You are recommended to copy the download address in the pop-up dialog box, log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for download over the private network at a higher speed.
>
>- You can also select **Local Download** to download it directly, which takes more time though.
>- `wget` command format: wget -c 'backup file download address' -O custom filename.xb 
>
Below is a sample:
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O ~/test.xb
```

### Step 2. Unpack the backup file
1. Run the xbstream command to unpack the backup file to the target directory.
```
xbstream -x -C /data < ~/test.xb
```
>
>- `/data` is used as an example in this document. You can replace it with a real path according to the actual situation.
>- Replace `~/test.xb` with your backup file.
>
The unpacking result is as shown below:
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

### Step 3. Decompress the backup file
1. Download qpress by running the following command.
```
wget http://www.quicklz.com/qpress-11-linux-x64.tar
```
>If an error is displayed for the `wget` download operation, you can go to [QuickLZ's official website](http://www.quicklz.com/) to download the qpress locally, and then upload it to the Linux CVM instance. For more information, please see [Uploading Files to Linux CVM with SCP](https://intl.cloud.tencent.com/document/product/213/2133).
2. Extract the qpress binary files by running the following command.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Then, decompress all `.qp` files in the target directory by running the following command:
```
xtrabackup --decompress --target-dir=/data
```
>
>- `/data` is the target directory where the backup file was previously stored. You can replace it with a real path according to the actual situation.
>- The `--remove-original` options is supported only in Percona Xtrabackup 2.4.6 and higher.
>- `xtrabackup` won't delete the original files during decompression by default. If you want to delete them upon the completion of decompression, add the `--remove-original` parameter to the above command.
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

### Step 4. Prepare the backup file
After a backup file is decompressed, perform the "apply log" operation by running the following command.
```
xtrabackup --prepare  --target-dir=/data
```
If the execution result contains the following output, it means that the preparation succeeded.
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
	

### Step 5. Modify the configuration file
1. Run the following command to open the `backup-my.cnf` file.
```
vi /data/backup-my.cnf
```
>The target directory `/data` is used as an example in this document. You can replace it with a real path according to the actual situation.
>
2. Given the existing version issues, the following parameters need to be commented in the extracted file `backup-my.cnf`.
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 
 
![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

### Step 6. Modify file attributes
Modify file properties and check whether files are owned by a TencentDB for MySQL user.
```
chown -R mysql:mysql /data
```
![](https://main.qcloudimg.com/raw/2c2bfcad8c8bdac9385e70d975bec56a.png)

### Step 7. Start the `mysqld` process and log in for verification
1. Start the mysqld process.
```
mysqld_safe --defaults-file=/data/backup-my.cnf --user=mysql --datadir=/data &
```
2. Log in to the MySQL client for verification.
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

