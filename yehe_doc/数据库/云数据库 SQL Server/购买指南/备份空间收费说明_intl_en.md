
## Overview
Backup space is used to store the backup files of all TencentDB for SQL Server instances in a region, including automatic data backups, manual data backups, and log backups.

**Backup space range**
The backup space of an account is used to store the backup files of all TencentDB for SQL Server (Basic Edition/High Availability Edition/Cluster Edition) instances in a region. It is calculated separately for each region; that is, the backup files of all instances in the Beijing and Shanghai regions are calculated in two different resource pools.

**Backup space composition**
Backup files in backup space include automatic data backups, manual data backups, and log backups.

**Total size of backup files**
Total size of backup files in one region = Data backup volume (automatic + manual) + log backup volume (all values are for the region)

**Free backup space**
TencentDB for SQL Server offers a certain amount of backup space free of charge by region, which is equivalent to the sum of storage spaces of all Basic Edition, High Availability Edition, and Cluster Edition primary instances in a region. For calculation examples, see [Backup Space Calculation Formula](#bfkjjsgs).

>?
>- Free backup space is only available when you purchase a primary instance.
>- The backup space can be viewed on the database backup page in the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).

## Backup Pricing
Backups beyond the free tier (100% disk storage) are pay-as-you-go by region at 0.0001261 USD/GB/hour in the Chinese mainland and 0.0001418 USD/GB/hour outside the Chinese mainland.
>?Billable space of less than 1 GB is not billed, and a billable time period of less than one hour is counted as one hour.

## Billing Schedule for Backup Space
Billing will officially start at 00:00 on June 1, 2022 for backups beyond the free tier.

## [Backup Space Calculation Formula](id:bfkjjsgs)
**Free backup space in one region = Sum of the 100% disk storage space (billable space) of all TencentDB for SQL Server instances in the region
Billable backup space in one region = Data backup volume (automatic + manual) + log backup volume - free backup space (all values are for the region)**

>!
>- Backup fees are subject to the backup size but not the storage space usage, as backups do not occupy the storage space.
>- When analyzing the backup fees, you need to check the backup size rather than the storage space usage.
>- The backups of isolated instances will also be counted into the backup space.

**Calculation example**
If you have a running TencentDB for SQL Server Cluster Edition instance with a purchased database storage space of 500 GB/month in Beijing Zone 5 and another such instance with 200 GB/month in Beijing Zone 3, you will get a free backup space of 700 GB/month in the Beijing region.

If your data backups reach 800 GB and log backups reach 100 GB in the current hour, your total backup space used in the Beijing region will exceed 700 GB, and you will be billed for the excess of 200 GB (800 + 100 - 700 = 200) for the current hour and so on.

## Backup Lifecycle
The backups of a running or isolated instance will be billed until it is deactivated.

**Pay-as-you-go instance**
- Backups are subject to change over the instance lifecycle.
- The backup feature can be used normally within 24 hours after an instance expires, during which backups beyond the free tier will still be billed.
- After 24 hours, the instance will be isolated into the recycle bin. At this point, rollback and manual backup will be prohibited, but automatic backup can still be performed, and you can still download backups (by clicking **More** > **Backup Download** in the **Operation** column of the instance in the console). You can renew the instance in the recycle bin in the console to recover it.
- After three days of isolation in the recycle bin (i.e., on the fifth day after expiration), the instance will be deactivated and terminated, along with all data backups. Therefore, you need to save the required backup files promptly.

## Payment Overdue
**Pay-as-you-go instance**
- After your account has overdue payments, the backup will change with the lifecycle of the instance. For more information, see the backup lifecycle of pay-as-you-go instances.

## Upgraded Services Available After Backup Billing Starts
| Improvement | Before Upgrade | After Upgrade |
|---------|---------|---------|
| Data backup retention period | Seven days by default. | Customizable between 3 and 1,830 days. |
| Data backup cycle | Once every 24 hours by default. | It is once every 24 hours by default if the data backup retention period is less than seven days. It is customizable if the data backup retention period is greater than or equal to seven days; however, to ensure the backup continuity, you need to set two or more backups every week. |
| Log backup | Log backups cannot be viewed or downloaded. | Log backups can be viewed and downloaded. The log backup retention period is the same as the configured data backup retention period, and the log backup frequency is once every 30 minutes. |
| All-instance-level backup statistics overview | Not supported. | It is supported and makes it easier for you to view the backup space statistics and trends of all instances in each region under your account, free tier usages, as well as the real-time backup space statistics of each instance, including: <li>Total backups: Displays the statistics and overview of all backups, data backups, and log backups.<br><li>Real-time backup statistics: Displays the real-time size statistics of the backup space of each instance in each dimension. |
| Isolated instance | Backups cannot be viewed or downloaded. | Backups can be viewed and downloaded. |
| Single-database backup optimization | 	/ | <li>Databases can be searched for by name.<li>Single-database backups can be sorted by size in ascending or descending order.<li>The size of single-database backup files can be displayed in an aggregated manner. |
| Backup list optimization | 	/ | <li>Backups can be filtered and viewed by time period, including all, today, past seven days, past 15 days, past 30 days, and custom time period.<li>Backups can be displayed as and searched for by files.</li> |

## Suggestions for Reducing Backup Costs
- Delete manual backups that are no longer used (on the **Instance Management** > **Backup Management** page in the [TencentDB for SQL Server](https://console.cloud.tencent.com/sqlserver)). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and backup file retention period in the console, which should be at least twice a week).
>?The [rollback feature](https://intl.cloud.tencent.com/document/product/238/7522) relies on the backup cycle and retention period of data backups and log backups, but reducing the frequency and retention period of automatic backups will affect the rollback time range for instance data, you need to configure backup appropriately based on your actual needs.
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of 7 days can meet the needs in most cases)

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7–1,830 days |
| Non-core, non-data businesses | Seven days |
| Archival businesses | Seven days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | Seven days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |


