This document describes how to restore data from a logical backup file.

## Overview
>?To save storage space, TDSQL-C for MySQL backup files will be compressed with qpress and then packed with xbstream offered by Percona.

TDSQL-C for MySQL supports logical backup. You can manually generate and download logical backup for the entire cluster or specified databases/tables. This document describes how to restore data from a logical backup file on Linux.

## Directions
### Step 1. Download the backup file
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
2. On the cluster management page, select **Backup Management** > **Data Backup List**, find the target backup, and click **Download** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/7701c1990a4c0d0aa06747ec0d49cd7e.png)
3. Copy the download address in the pop-up window, log in to a Linux CVM instance in the same VPC as the TencentDB instance as instructed in [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517), and run the `wget` command for download over the private network.
>?
>- You can also click **Download** to download it directly. However, this may take longer.
>- wget command format: wget -c "<backup download address>" -O <custom filename>.xb
>

The `wget` command format is as follows:
```
wget -c "backup file download address" -O custom filename.xb
```

### Step 2. Unpack the backup file
Unpack the backup file with xbstream.
>?xbstream can be downloaded at [Percona's official website](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Select Percona XtraBackup v2.4.6 or later. For more information on installation, see [Installing Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI).
>
```
xbstream -x < test0.xb
```
>?Replace `test0.xb` with your backup file name.
>
The unpacking result is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/6526474a34d9fd576588052f9c22915e.png)

### Step 3. Decompress the backup file
1. Download qpress by running the following command.
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?If an error is displayed during the `wget` download, you can go to [QuickLZ's official website](http://www.quicklz.com/) to download qpress locally and upload it to the Linux CVM instance. For more information, see [Uploading Files from Linux or MacOS to Linux CVM via SCP](https://intl.cloud.tencent.com/document/product/213/2133).
>
2. Extract the qpress binary files by running the following command:
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. Decompress the backup file with qpress.
```
qpress -d <backup file>.sql.qp .
```

### Step 4. Import the backup file into the target database
Import the .sql file into the target database by running the following command:
```
mysql -u<account name> -P<port> -h<target database's private network address> -p < <.sql file compressed with qpress>
```

