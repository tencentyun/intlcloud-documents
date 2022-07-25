The TDSQL-C for MySQL console provides the list of logical backup files that can be downloaded. They may then be used to restore data from one database to another (such as a self-built database or a database provided by another cloud vendor).

## File Types Supported for Download, Decompression, and Deletion
<table>
<thead><tr><th>Category</th><th colspan = "2" style="text-align:center" width="30%">Backup Type</th><th>Method</th><th>Download</th><th>Decompression Required After Download</th><th>Deletion</th></tr></thead>
<tbody>
<tr>
<td>Data backup</td><td>Logical backup</td><td>Full backup</td><td>Manual</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td></tr>
<tr>
<td>Binlog backup</td><td>Binlog backup</td><td>Incremental backup</td><td>Automatic</td><td>&#10003;</td><td>&#10003;</td><td>x</td></tr>
</tbody></table>

## Downloading a Data Backup File
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select **Backup Management** > **Data Backup List** to view the backup file.
![](https://qcloudimg.tencent-cloud.cn/raw/06a7cf2e29d6b8f9a405aacb283109d6.png)
4. In the **Operation** column of a data backup file, click **Download**.
5. In the pop-up window, click **Copy** to get the file download address for fast download over the private network by running the `wget` command, or directly click **Download**.
>?
>- After copying the download address, log in to a Linux CVM instance in the same VPC as the TencentDB instance as instructed in [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517), and run the `wget` command for download over the private network.
>- The download address is valid for 12 hours, after which you will need to enter the download page again to get a new one.
>- The URL must be enclosed with quotation marks when wget is used to download.
>- wget command format: wget -c "<backup download address>" -O <custom filename>.xb
>
![](https://qcloudimg.tencent-cloud.cn/raw/7788dee12af0c071308e9e6bf47fd551.png)

## Downloading a Binlog Backup File
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select **Backup Management** > **Binlog Backup List** to view the backup file.
![](https://qcloudimg.tencent-cloud.cn/raw/1b5e24ffd6c59da5fe29c3b732384d21.png)
4. In the **Operation** column of a binlog backup file, click **Download**.
5. In the pop-up window, click **Copy** to get the file download address for fast download over the private network by running the `wget` command, or directly click **Download**.
>?
>- After copying the download address, log in to a Linux CVM instance in the same VPC as the TencentDB instance as instructed in [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517), and run the `wget` command for download over the private network.
>- The download address is valid for 12 hours, after which you will need to enter the download page again to get a new one.
>- The URL must be enclosed with quotation marks when wget is used to download.
>- wget command format: wget -c "<backup download address>" -O <custom filename>.xb
>
![](https://qcloudimg.tencent-cloud.cn/raw/7788dee12af0c071308e9e6bf47fd551.png)

## Decompressing a File
To save storage space, TDSQL-C for MySQL data and binlog backup files will be compressed with qpress and then packed with xbstream offered by Percona. Therefore, downloaded backup files can be imported to the target database only after being unpacked and decompressed.
### Unpacking a backup file
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

### Decompressing a backup file
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

