## Operation Scenarios
The open-source software tool Percona Xtrabackup can be used to back up and restore databases. This document describes how to use XtraBackup to restore a logical backup file of a TencentDB for MySQL instance to a self-built database on another server.

> XtraBackup only supports Linux but not Windows.

## Prerequisites
- Download and install XtraBackup.
  XtraBackup can be downloaded at [Percona's official website](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Please select Percona XtraBackup 2.4.6 or higher. For more information on how to install the tool, please see [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
- Supported instance version: TencentDB for MySQL 5.5, 5.6, and 5.7 High-Availability Edition.

## Directions
### Step 1. Download the backup file
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
2. On the instance management page, click **Backup and Restore** > **Data Backup List**, select the backup to download, and then click **Download** in the "Operation" column.
3. You are recommended to copy the download address in the pop-up dialog box, log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for download over the private network at a higher speed.
>
>- You can also select **Local Download** to download it directly, which takes more time though.
>- `wget` command format: wget -c 'backup file download address' -O custom filename.xb
>
Below is a sample:
```
wget -c 'https://mysql-database-backup-bj-118.cos.ap-beijing.myqcloud.com/12427%2Fmysql%2F42d-11ea-b887-6c0b82b%2Fdata%2Fautomatic-delete%2F2019-11-28%2Fautomatic%2Fxtrabackup%2Fbk_204_10385%2Fcdb-1pe7bexs_backup_20191128044644.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3D1%26q-sign-time%3D1574269%3B1575417469%26q-key-time%3D1575374269%3B1517469%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dfb8fad13c4ed&response-content-disposition=attachment%3Bfilename%3D%2141731_backup_20191128044644.xb%22&response-content-type=application%2Foctet-stream' -O test0.xb
```

### Step 2. Unpack the backup file
Unpack the backup file with xbstream.
```
xbstream -x < test0.xb
```
>- Replace `test0.xb` with your backup file.
>
The unpacking result is as shown below:
![](https://main.qcloudimg.com/raw/61b53f4f54ffd2fbe7c0d1b3423255b0.png)

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
3. Decompress the backup file with qpress.
```
qpress -d cdb-jp0zua5k_backup_20191202182218.sql.qp .
```
>Find the backup file with `.sql.qp` extension by decompression time and replace `cdb-jp0zua5k_backup_20191202182218` with its filename.
>
The decompressing result is as shown below:
![](https://main.qcloudimg.com/raw/355557bc949fd86af8346d8a44dc4551.png)

### Step 4. Import into the database
Import the file into the database by running the following command:
```
mysql -uroot -P3306 -h127.0.0.1 -p < cdb-jp0zua5k_backup_20191202182218.sql
```
>
>- Importing into a local MySQL instance with port 3306 is used as an example in this document. You can replace it according to the actual situation.
>- Replace `cdb-jp0zua5k_backup_20191202182218.sql` with the .sql file actually extracted by qpress.
