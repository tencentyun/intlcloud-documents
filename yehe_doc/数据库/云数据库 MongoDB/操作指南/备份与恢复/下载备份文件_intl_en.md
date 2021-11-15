This document describes how to download backup files of TencentDB for MongoDB through the console and CVM.

## Step 1. Generate a backup file
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb), click an instance ID in the instance list, and enter the instance management page.
2. On the **Backup and Rollback** > **Backup Task List** tab, locate the desired backup and click **Download** in the **Operation** column.
>?You can click **Manual Backup** in the upper right corner to generate a manual backup at the moment.
>
![](https://main.qcloudimg.com/raw/2995c172841a888402275133d31f9d2f.png)
3. In the pop-up dialog box, click **OK**.

## Step 2. Download the backup file
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb), click an instance ID in the instance list, and enter the instance management page.
2. On the **Backup and Rollback** > **File Download List** tab, view the backup file progress.
![](https://main.qcloudimg.com/raw/02d08a9ca234f07c43be2c59f08e187d.png)
3. After the backup file is generated, we recommend you copy the download link, log in to a [(Linux) CVM instance in the same VPC as the TencentDB instance](https://intl.cloud.tencent.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8), and run the `wget` command for high-speed download over the private network.
>?
>- You can click **Download from Internet** in the **Operation** column to download the backup file using your browser.
>- The `wget` command format: `wget -c 'private network address' -O backup.tar`
>

