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
![](https://staticintl.cloudcachetci.com/yehe/backend-news/TkW7474_9.png)
4. In the **Operation** column of a data backup file, click **Download**.
5. In the pop-up window, click **Copy** to get the file download address for fast download by running the `wget` command, or directly click **Download**.
>?
>- After copying the download address, log in to a Linux CVM instance as instructed in [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8) and run the `wget` command for download.
> - If the cluster and CVM instance are in the same region, the `wget` command can be used for fast download over the private network, no matter whether they are in the same or different VPCs.
>  - If the cluster and CVM instance are in different regions, fast download over the private network is not supported, and the public IP must be enabled for the CVM instance before the `wget` command can be used for download.
>- The download address is valid for 12 hours, after which you will need to enter the download page again to get a new one.
>- The URL must be enclosed with quotation marks when the `wget` command is used to download.
>- wget command format: wget -c "<backup download address>" -O <custom filename>.xb
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/7LTa589_10.png)

## Downloading a Binlog Backup File
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster, and click the cluster ID or **Manage** in the **Operation** column to enter the cluster management page.
3. On the cluster management page, select **Backup Management** > **Binlog Backup List** to view the backup file.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Y6Kv945_11.png)
4. In the **Operation** column of a data backup file, click **Download**.
5. In the pop-up window, click **Copy** to get the file download address for fast download by running the `wget` command, or directly click **Download**.
>?
>- After copying the download address, log in to a Linux CVM instance as instructed in [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8) and run the `wget` command for download.
> - If the cluster and CVM instance are in the same region, the `wget` command can be used for fast download over the private network, no matter whether they are in the same or different VPCs.
>  - If the cluster and CVM instance are in different regions, fast download over the private network is not supported, and the public IP must be enabled for the CVM instance before the `wget` command can be used for download.
>- The download address is valid for 12 hours, after which you will need to enter the download page again to get a new one.
>- The URL must be enclosed with quotation marks when the `wget` command is used to download.
>- wget command format: wget -c "<backup download address>" -O <custom filename>.xb
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/zYYE823_12.png)

## Decompressing a File
To save storage space, TDSQL-C for MySQL data and binlog backup files will be compressed with qpress and then packed with xbstream offered by Percona. Therefore, downloaded backup files can be imported to the target database only after being unpacked and decompressed.

### Unpacking a backup file
Unpack the backup file with xbstream.
>? xbstream can be downloaded at [Percona's official website](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/). Select Percona XtraBackup v2.4.6 or later. For more information on installation, see [Installing Percona XtraBackup on Red Hat Enterprise Linux and CentOS](https://docs.percona.com/percona-xtrabackup/2.4/installation/yum_repo.html).
>
```
xbstream -x < test0.xb  -P
```
>?Replace `test0.xb` with your backup file name.
>
The unpacking result is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/cca5598d0c99ccb9804af38bb44ca5e2.png)

### Decompressing a backup file
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

