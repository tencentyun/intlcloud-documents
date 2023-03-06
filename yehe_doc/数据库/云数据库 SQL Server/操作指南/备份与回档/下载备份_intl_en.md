The TencentDB for SQL Server console provides the list of backup files that can be downloaded over the private or public network. You can use the downloaded backups to restore data from one database to another (such as a self-built one).
This document describes how to download a local or cross-region backup in the console.

## Directions
### Downloading the backup file of a running instance
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click the target instance ID or **Manage** in the **Operation** column to enter the instance management page.
![](https://qcloudimg.tencent-cloud.cn/raw/1b41988a3ab435f3aa4154f293c1558a.png)
3. On the instance management page, select **Backup Management** and view the target backup file in the data or log backup list.
   - To download an archive backup file, click **Download** in the **Operation** column in the backup list. The downloaded backup is a local backup if its region is the same as that of the instance. If not, the downloaded backup is a cross-region backup.![](https://main.qcloudimg.com/raw/30fb714fc7a8751b2833f50a2c0de654.png)
   - To download an unarchived backup file, select **View Details** > **Download** in the **Operation** column in the backup list to download the backup file of each database.
   ![](https://qcloudimg.tencent-cloud.cn/raw/1c00e970360331b3cd7f530f2ba4dcfb.png)
4. In the pop-up window, get the file download address for fast download over the private network by running the `wget` command, or directly click **Download**.
>?
>- We recommend that you copy the private download link, log in to a Linux CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for download over the private network at a higher speed. For more information, see [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
>- The download address is valid for 15 minutes, after which you will need to enter the download page again to get a new one.
>- The URL must be enclosed with quotation marks when the `wget` command is used to download.
>
![](https://main.qcloudimg.com/raw/b7a7289733af5100008952ed1ba3b589.png)


### Downloading the backup file of an isolated instance
You can also download the backup file of an isolated instance.
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select the region at the top, find the target instance, and click **More** > **Download Backup** in the **Operation** column to enter the backup download page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/5fd26f42851c161815be3cc5e24a1ccc.png)
   - To download an archived backup file, click **Download** in the **Operation** column in the backup list, and download the file on the displayed download page.
   - To download unarchived backup files, select **View Details** > **Download** in the **Operation** column to download the backup file of each database.
   ![](https://qcloudimg.tencent-cloud.cn/raw/a96d2310328e0aa4adede1f57d2e7886.png)

