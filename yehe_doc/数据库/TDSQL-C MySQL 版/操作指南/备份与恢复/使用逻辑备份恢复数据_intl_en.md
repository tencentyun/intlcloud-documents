This document describes how to restore data from a logical backup file.

## Overview
>?To save storage space, TDSQL-C for MySQL backup files will be compressed with qpress and then packed with xbstream offered by Percona.

TDSQL-C for MySQL supports logical backup. You can manually generate and download logical backup for the entire cluster or specified databases/tables. Taking Linux as an example, the following describes how to restore data from a logical backup file.

## Directions
### Step 1. Download the backup file
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
2. On the cluster management page, select **Backup Management** > **Data Backup List**, find the target backup, and click **Download** in the **Operation** column.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9i8N093_33.png)
3. Copy the download address in the pop-up window, log in to a Linux CVM instance as instructed in [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8), and run the `wget` command for fast download.
>?
>- After copying the download address, log in to a Linux CVM instance as instructed in [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8) and run the `wget` command for download.
> - If the cluster and CVM instance are in the same region, the `wget` command can be used for fast download over the private network, no matter whether they are in the same or different VPCs.
>  - If the cluster and CVM instance are in different regions, fast download over the private network is not supported, and the public IP must be enabled for the CVM instance before the `wget` command can be used for download.
>- You can also click **Download** to download it directly. However, this may take a longer time.
>
The `wget` command format is as follows:
```
wget -c "<backup download address>" -O <custom filename>.xb
```

### Step 2. Unpack the backup file
Unpack the backup file with xbstream.
>? xbstream can be downloaded at [Percona's official website](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Select Percona XtraBackup v2.4.6 or later. For more information on installation, see [Installing Percona XtraBackup on Red Hat Enterprise Linux and CentOS](https://docs.percona.com/percona-xtrabackup/2.4/installation/yum_repo.html).
>
```
xbstream -x < test0.xb  -P
```
>?Replace `test0.xb` with your backup file name.
>
The unpacking result is as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VkG7203_34.png)

### Step 3. Decompress the backup file
1. Download qpress by running the following command.
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar
```
>?If an error is displayed during the `wget` download, you can click [here](https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar) to download qpress locally and upload it to the Linux CVM instance. For more information, see [Uploading Files from Linux or MacOS to Linux CVM via SCP](https://intl.cloud.tencent.com/document/product/213/2133).
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
