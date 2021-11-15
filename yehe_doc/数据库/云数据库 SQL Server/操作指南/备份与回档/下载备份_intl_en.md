
## Overview
The TencentDB for SQL Server console provides the list of backup files that can be downloaded over the private or public network. They may then be used to restore data from one database to another (such as a self-built one).

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the **Backup Management** tab, view the backup list.
 - To download an archived backup file, locate the backup record in the backup list, click **Download** in the **Operation** column, and download the file on the displayed download page.
![](https://main.qcloudimg.com/raw/30fb714fc7a8751b2833f50a2c0de654.png)
 - To download unarchived backup files, click the backup record in the backup list to expand the nested list, click **Download** in the **Operation** column, and download the backup file of each database on the displayed download page.
3. Get the download address of the backup file in the pop-up dialog box.
>?
>- Copy the private network **download address**, [log in to the Linux CVM in the same VPC as the TencentDB instance](https://intl.cloud.tencent.com/document/product/213/10517), and run `wget` to download the file over the high-speed private network.
>- The download address is valid for 15 minutes, after which you will need to enter the download page again to get a new one.
>
![](https://main.qcloudimg.com/raw/b7a7289733af5100008952ed1ba3b589.png)


