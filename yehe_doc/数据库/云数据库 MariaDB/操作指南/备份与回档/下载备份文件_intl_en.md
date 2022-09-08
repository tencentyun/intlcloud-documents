
You can download the cold backup data and binlogs in the TencentDB for MariaDB console.

## Downloading a cold backup or binlog
1. Log in to the [TencentDB for MariaDB console] (https://console.cloud.tencent.com/mariadb). Click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. Select **Backup and Restoration** > **Cold Backup List** or **Binlog List**
3. Select the file to be downloaded and click **Download** in the **Operation** column.
4. In the pop-up dialog box, click **Get Download Address** to get the download address in a VPC.
5. Log in to CVM (Linux system) under the VPC where the database resides as instructed in [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517) and run the `wget` command to download the file.
>?
>- Command syntax: `wget -c 'download address'`
>- The download address can only be used in a VPC and is valid for 15 minutes. If it expires, you can refresh the page to get a new one.
>
![](https://main.qcloudimg.com/raw/c4dd3fd398fe0367dd4c7b9a4fc3dea4.png)

## Downloading a slow log
1. Log in to the [TencentDB for MariaDB console] (https://console.cloud.tencent.com/mariadb). Click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. Select **Performance Optimization** > **Slow Log** tab
3. Select the file to be downloaded and click **Download** in the **Operation** column.
>?If the file size is 0 KB, no slow query record is available for download.
4. In the pop-up dialog box, click **Get Download Address** to get the download address in a VPC.
5. Log in to CVM (Linux system) under the VPC where the database resides as instructed in [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517) and run the `wget` command to download the file.
>?
>- Command syntax: `wget -c 'download address'`
>- The download address can only be used in a VPC and is valid for 15 minutes. If it expires, you can refresh the page to get a new one.
>
