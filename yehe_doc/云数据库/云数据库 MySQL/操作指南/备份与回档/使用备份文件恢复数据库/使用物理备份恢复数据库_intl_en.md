
## Overview
>?To save storage capacity, physical and logical backups in TencentDB for MySQL will be compressed with qpress and then packed with xbstream offered by Percona.
>
The open-source Percona XtraBackup can be used to back up and restore databases. This document describes how to use XtraBackup to restore a physical backup file of TencentDB for MySQL instance to a self-built database on CVM.
- XtraBackup only supports Linux but not Windows.
- For more information about how to restore data in Windows, please see [Offline Migration of Data > Data Migration with Command Line Tool](https://intl.cloud.tencent.com/document/product/236/8464).


## Prerequisites
- Download and install XtraBackup.
XtraBackup can be downloaded at [Percona's official website](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Please select Percona XtraBackup v2.4.6 or later. For more information on installation, please see [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
- Supported instance architectures: two-node or three-node MySQL
- Instances with data encryption enabled cannot be restored from a physical backup.

## Directions
>?This document takes a CVM instance running CentOS and a MySQL v5.7 instance as an example.
>
### Step 1. Download the backup file
You can download data backups and log backups of TencentDB for MySQL instances in the console.
>?Each IP can have up to 10 download links by default, with a download speed limit of 20–30 Mbps each.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Backup and Restore** > **Data Backup List** tab, locate the backup file to be downloaded and click **Download** in the **Operation** column.
3. We recommend you copy the download link in the pop-up dialog box, log in to a [(Linux) CVM instance in the same VPC as the TencentDB instance](https://intl.cloud.tencent.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8), and run the `wget` command for download over the private network at a higher speed.
>?
>- You can also click **Download** to download it directly, which may take longer.
>- `wget` command format: wget -c 'backup file download address' -O custom filename.xb 
>
Example:
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O ~/test.xb
```

### Step 2. Restore data
#### 2.1 Unpack the backup file
Run the xbstream command to unpack the backup file to the target directory.
```
xbstream -x -C /data < ~/test.xb
```
>?
>- `/data` is used as an example in this document. You can replace it with a real path according to the actual situation.
>- Replace `~/test.xb` with your backup file.
>
The unpacking result is as shown below:
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

#### 2.2 Decompress the backup file
1. Download qpress by running the following command:
```
wget http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?If an error is displayed during the `wget` download, you can go to [QuickLZ's official website](http://www.quicklz.com/) to download qpress locally and upload it to the Linux CVM instance. For more information, please see [Uploading Files via SCP to a Linux CVM from Linux](https://intl.cloud.tencent.com/zh/document/product/213/2133).
2. Extract the qpress binary files by running the following command.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Decompress all `.qp` files in the destination directory by running the following qpress command:
```
xtrabackup --decompress --target-dir=/data
```
>?
>- `/data` is the target directory where the backup file was previously stored. You can replace it with a real path according to the actual situation.
>- The `--remove-original` option is supported only in Percona Xtrabackup v2.4.6 and later.
>- `xtrabackup` won't delete the original files during decompression by default. If you want to delete them upon the completion of decompression, add the `--remove-original` parameter to the above command.
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

#### 2.3 Prepare the backup file
After a backup file is decompressed, you need to execute the "apply log" operation by running the following command.
```
xtrabackup --prepare  --target-dir=/data
```
If the execution result contains the following output, it means that the preparation succeeded.
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
	
	
#### 2.4 Modify the configuration file
1. Run the following command to open the `backup-my.cnf` file.
```
vi /data/backup-my.cnf
```
>?The target directory `/data` is used as an example in this document. You can replace it with a real path according to the actual situation.
>
2. Given the existing version issues, the following parameters need to be commented out from the extracted file `backup-my.cnf`.
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 

![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

#### 2.5 Modify file attributes
Modify file attributes and check whether files are owned by the `mysql` user.
```
chown -R mysql:mysql /data
```
![](https://mc.qcloudimg.com/static/img/efbdeb20e1b699295c6a4321943908b2/4.png)

### Step 3. Start the mysqld process and log in for verification
1. Start the mysqld process.
```
mysqld_safe --defaults-file=/data/backup-my.cnf --user=mysql --datadir=/data &
```
2. Log in to the client for verification.
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

## Backup FAQs
See [Common Issues](https://intl.cloud.tencent.com/document/product/236/9036) and [Failure Reasons](https://intl.cloud.tencent.com/document/product/236/34394).


