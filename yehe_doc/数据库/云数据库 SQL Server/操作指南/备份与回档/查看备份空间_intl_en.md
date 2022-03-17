This document describes how to view the backup space in the console.

## Overview
The backup space occupied by TencentDB for SQL Server instance backup files is allocated by region. It is equivalent to the total storage capacity used by all database backups in a region, including automatic data backups, manual data backups, and log backups.
Increasing the backup retention period or frequency will use more database backup space. You can view the backup space statistics and trends of all instances in each region under your account as well as the real-time backup space statistics of each instance.

## Viewing Total Backups
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. On the left sidebar, select **Database Backup**.
3. On the **Database Backup** page, select a region to view the total backups on the **Overview** tab, including the used backup space and numbers of all backups, data backups, and log backups in the region.
![](https://qcloudimg.tencent-cloud.cn/raw/f4e0c1edddfa628009eb6642f8e81482.png)
>?
>- If the value of the total backups is displayed in green, the total backup space used does not exceed the free tier.
>- If the value of the total backups is displayed in orange, the total backup space used has exceeded the free tier and incurred fees.

## Viewing Real-Time Backup Statistics
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. On the left sidebar, select **Database Backup**.
3. On the **Database Backup** page, select a region to view the real-time backup statistics at the bottom of the **Overview** tab, including the instance ID/name, backup space, data backups, log backups, automatic backups, and manual backups.
![](https://qcloudimg.tencent-cloud.cn/raw/90f8494adce2e4d09f544a32470a9cd1.png)
>?On the backup statistics page, you can search for an instance by instance ID to view its real-time backup statistics. You can also perform various operations such as sorting statistical fields by space size, refreshing the statistics page, and downloading data.
![](https://qcloudimg.tencent-cloud.cn/raw/1bf6258e6937995769dc51d9f60c6f38.png)

