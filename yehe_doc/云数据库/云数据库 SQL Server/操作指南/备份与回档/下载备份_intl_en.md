
## Overview
The TencentDB for SQL Server console provides the list of backup files that can be downloaded over the private or public network. Then, they can be used to restore a database to another database (such as a self-built one).

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Manage Backup** tab, view the list of backup files, and click **Download** to enter the download page.
![](https://main.qcloudimg.com/raw/30fb714fc7a8751b2833f50a2c0de654.png)
3. In the pop-up window, get the private address of the file or click **Download** directly for download.
>?
>- We recommend you copy the download address, log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for download over the private network at a higher speed.
>- The download address is valid for 15 minutes, after which you will need to enter the download page again to get a new download address.
>
![](https://main.qcloudimg.com/raw/b7a7289733af5100008952ed1ba3b589.png)

