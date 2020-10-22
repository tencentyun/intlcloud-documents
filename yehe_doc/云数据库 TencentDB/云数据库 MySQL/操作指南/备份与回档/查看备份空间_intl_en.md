This document describes how to view the MySQL instance backup capacity and free tier in the console.

## Operation Scenarios
The backup space occupied by TencentDB for MySQL instance backup files is allocated by region. It is equivalent to the total storage capacity used by all MySQL database backups in a region, including automatic data backups, manual data backups, and log backups. Increasing the backup retention time or manual backup frequency will use more database backup storage capacity.

## Directions
1. Log in to the [MySQL Console](https://console.cloud.tencent.com/cdb) and select **Database Backup** on the left sidebar.
2. Select a region at the top to view its backup information on the **Overview** tab, including total backup, backup trend, and real-time backup statistics.
 - Total Backup: this section displays the size and quantity of all, data, and log backups as well as the free tier occupied by all the backups. 
>?
>- Green: the total backup space used does not exceed the free tier.
>- Orange: the total backup space used has exceeded the free tier and incurred fees. For more information, please see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).
>
![](https://main.qcloudimg.com/raw/e9489e74614d7708d357de6943837c3c.png)
 - Backup Trend: this section displays the trends of each backup count.
 - Real-Time Backup Statistics: this section displays the names/IDs (you can click a name/ID to enter the instance details page), backup space values (which can be sorted by backup size), and data/log backups of instances in the selected region. You can search for an instance by name/ID in the search box in the top-right corner.
![](https://main.qcloudimg.com/raw/0587e4f22b33960c349b2e2dbbe81d10.png)
3. The **Backup List** tab contains the data backup list and the log backup list, both of which support filtering by time period and fuzzy search by instance name/ID. You can click an instance name/ID in the list to enter the instance details page.
![](https://main.qcloudimg.com/raw/bf90904f3170c4bc0316a64c9492f3ed.png)
 - **Data backup list**
    - Filtering by information field is supported:
Type: all, logical cold backup, physical cold backup.
Backup Mode: all, auto, manual.
Backup Method: currently, only full backup is supported.
    - Backups can be sorted by backup time, task start time, task end time, and backup size.
    - Click **Details** in the "Operation" column to enter the instance backup and restoration page, where you can click **Download** to download backups. Only manual backups can be deleted.
 - **Log backup list**
    - Backups can be sorted by log data start time and log data end time.
    - Click **Details** in the "Operation" column to enter the instance backup and restoration page, where you can click **Download** to download logs.

## FAQ
#### How is the usage of backup space in excess of the free tier charged? How can I reduce backup costs?
For more information, please see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).
