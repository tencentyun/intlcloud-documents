## Overview
You can download TencentDB cold backup data and binlogs in the TencentDB for TDSQL Console.

## Directions
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb) and click the instance name or **Manage** in the "Operation" column to enter the instance management page.
2. Select **Shard Management** and click the shard ID to enter the shard management page.
3. Go to the **Backup and Restore** tab and select **Cold Backup List** or **Binlog List** and click **Download** in the "Operation" column.
4. A VPC address is provided in the download dialog box that pops up. You can click **Copy** to get the address.
>
>- The address is valid for 15 minutes. After it expires, refresh the page to get a new one. Access the VPC address in the VPC network.
>- We recommend that you copy the download address, log in to a (Linux) CVM instance in the same VPC as the TencentDB instance, and run the `wget` command for download.
>
![](https://main.qcloudimg.com/raw/f60b0938aa7bfea7597ff25ca01fcad3.png)


