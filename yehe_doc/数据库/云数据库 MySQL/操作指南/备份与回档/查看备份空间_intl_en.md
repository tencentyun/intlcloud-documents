
This document describes how to view the TencenDB for MySQL instance backup space and free tier in the console.

## Overview
- For two-node and three-node instances of local disk edition, the backup space occupied by TencentDB for MySQL instance backup files is allocated by region. It is equivalent to the total storage capacity used by all database backups in a region, including automatic data backups, manual data backups, and log backups. Increasing the backup retention period or manual backup frequency will use more database backup space.

- For single-node instances of cloud disk edition, the backup space occupied by TencentDB for MySQL instance backup files is allocated by instance. The free backup space of one instance is equivalent to 200% of its storage space.

## Viewing the backup space and free tier of an instance of local disk edition
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and select **Database Backup** on the left sidebar.
2. Select a region at the top to view its backup information on the **Overview** tab, including total backup, backup trend, and real-time backup statistics.
 - Total Backup: This section displays the size and quantity of all backups, data backups, and log backups as well as the free tier occupied by all the backups. 
>?
>- Green: The total backup space used does not exceed the free tier.
>- Orange: The total backup space used has exceeded the free tier and incurred fees. For more information, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).
>
![](https://main.qcloudimg.com/raw/e9489e74614d7708d357de6943837c3c.png)
 - Backup Trend: This section displays the trends of all backups, data backups, and log backups as well as the free space.
 - Real-Time Backup Statistics: This section displays the instance IDs/names (you can click an ID/name to enter the instance details page), backup space (which can be sorted by size), and data/log backups in the selected region. You can search for an instance by ID/name in the search box in the top-right corner.
3. Select **Backup List** at the top, where the backup list is divided into data backups and log backups. Click an instance name in the list to enter the instance details page. The backup list supports filtering by time period and fuzzy search by instance ID/name.
![](https://main.qcloudimg.com/raw/0587e4f22b33960c349b2e2dbbe81d10.png)
 - **Data Backup List**
    - Filtering by information field is supported:
    Type: All, logical cold backup, physical cold backup.
    Backup Mode: **All**, **Automatic**, **Manual**.
    Backup Method: Currently, only full backup is supported.
    - Backups can be sorted by backup time, task start time, task end time, or backup size.
    - Click **Details** in the **Operation** column to enter the **Backup and Restoration** tab, where you can click **Download** to download backups. Only manual backups can be deleted.
 - **Log Backup List**
    - Backups can be sorted by log data start time or end time.
    - Click **Details** in the **Operation** column to enter the **Backup and Restoration** tab, where you can click **Download** to download logs.

## Viewing the backup space and free tier of an instance of cloud disk edition
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the ID of the target instance or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Backup and Restoration** to view the used backup space and free space of the instance.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nYt7569_45.png)

## FAQs
#### How will I be charged for backup space beyond the free tier? How can I reduce the costs of backup space?
For more information, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).
