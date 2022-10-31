The TencentDB for MySQL console provides the list of backup files that can be downloaded. You can use the downloaded backups to restore data from one database to another (such as a self-built one).

This document describes how to download a backup file in the console.
>!The download rule varies by region. After the cross-region backup feature is enabled, you need to configure the download rule for each region selected for backup.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb).
2. Select the region at the top, find the target instance, and click the instance ID or **Manage** in the **Operation** column to enter the instance management page.
3. On the instance management page, select **Backup and Restoration** and view the target backup file in the data or log backup list.
![](https://qcloudimg.tencent-cloud.cn/raw/b3f84a061a2500a9d7fcc103ddc56db1.png)
4. Click **Download** in the **Operation** column in the backup list to enter the download page. Then, select the backup file in the target region, click **Copy Download URL** for high-speed download with the `wget` command, or directly click **Download**.
>?
>- We recommend you copy the download address, log in to a Linux CVM instance in the same VPC as the TencentDB instance as instructed in [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/213/10517), and run the `wget` command for download over the private network at a higher speed.
>- The download address is valid for 12 hours, after which you will need to enter the download page again to get a new one.
>- The URL must be enclosed with quotation marks when `wget` is used to download.
>- `wget` command format: `wget -c 'backup file download address' -O custom filename.xb`.
