## Operation Scenarios
The backup capacity occupied by TencentDB for MySQL instance backup files is allocated by region. It is equivalent to the total storage capacity used by all MySQL database backups in a region, including automatic data backups, manual data backups, and log backups. Increasing the backup retention time or manual backup frequency will use more database backup storage capacity.

This document describes how to view the MySQL instance backup capacity and free tier in the console.


## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and select **Database Backup** on the left sidebar.
![](https://main.qcloudimg.com/raw/c8951ac6272e3c7e8a579369fa527ebf.png)
2. Select a region at the top to view its backup overview and list.

### Overview Page
The overview page is divided into three sections: total backups, backup trend, and backup statistics.
- Total backups: This section displays the size and quantity of all, data, and log backups as well as the free tier and paid capacity.
>
>- Green: The total backup capacity used does not exceed the free tier.
>- Orange: The total backup capacity used has exceeded the free tier and incurred fees.
>
![](https://main.qcloudimg.com/raw/e9489e74614d7708d357de6943837c3c.png)
- Backup trend: This section displays the trends of each backup count.
- Backup statistics: This section displays the names/IDs of instances in the current region as well as the size and quantity of all, data, log, automatic, and manual backups.
Click an instance name/ID to enter the instance details page; the backup capacity can be sorted by backup size; you can search for a backup by instance name/ID in the search box in the top-right corner.
![](https://main.qcloudimg.com/raw/0587e4f22b33960c349b2e2dbbe81d10.png)

### Backup list
The backup list can be divided into data backups and log backups. You can click an instance name/ID in the list to enter the instance details page. The backup list supports filtering by time period and fuzzy search by instance name/ID.
![](https://main.qcloudimg.com/raw/bf90904f3170c4bc0316a64c9492f3ed.png)
**Data backup list**
- Filtering by information field is supported:
Type: All, logical cold backup, physical cold backup.
Backup mode: All, automatic, manual.
Backup method: Currently, only full backup is supported.
- Backups can be sorted by backup time, task start time, task end time, and backup size.
- Click **Details** in the "Operation" column to enter the instance backup and restoration page, where you can click **Download** to download backups. Only manual backups can be deleted.

**Log backup list**
- Log backups are calculated based on the end time of logs.
- Backups can be sorted by log data start time and end time.
- Click **Details** in the "Operation" column to enter the instance backup and restoration page, where you can click **Download** to download logs.


