## Overview
Backup capacity is used to store backup files of all TencentDB for MySQL instances in a region, including automatic data backups, manual data backups, and log backups.

TencentDB for MySQL offers a certain amount of backup capacity free of charge based on the region, which is equivalent to the sum of storage capacity of all high-availability instances (including master and disaster recovery instances) in your region.
>
>- Free backup capacity will be provided when you purchase a master or disaster recovery instance but not a read-only instance.
>- The backup capacity can be viewed on the database backup page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/backup).

## Backup Pricing
Excessive backup capacity will be charged at  0.000127 USD/GB/hour in Mainland China.
If the excessive backup capacity is less than 1 GB, no fees will be charged. If the time period is less than 1 hour, it will be calculated as 1 hour. TencentDB for MySQL adopts a flexible giveaway policy, so that you generally do not need to pay for the backup capacity for most instances.

## Billing Schedule for Backup Capacity
- Billing officially started from 00:00 on December 2, 2019 for Hong Kong (China), Macao (China), Taiwan (China), and other regions outside Mainland China.
- Billing officially started from 00:00 on December 2, 2019 for Southwest China (Chengdu and Chongqing regions).
- Billing officially started from 00:00 on December 5, 2019 for South China (Guangzhou region).
- Billing officially started from 00:00 on December 9, 2019 for North China (Beijing region).
- Billing officially started at 00:00 on December 10, 2019 for East China (Shanghai region).


## Calculation Formula

**Free backup capacity in one region = Sum of storage capacity of all TencentDB for MySQL high-availability instances in that region**

**Paid backup capacity in one region = Data backup volume + log backup volume - free backup capacity (all values are for that region)**

>TencentDB for MySQL instance backups in the recycle bin will also be calculated for the backup capacity.

**Calculation example**
If you have a running a TencentDB for MySQL high-availability instance with a purchased database storage capacity of 500 GB/month in Guangzhou Zone 3 and another such instance with a purchased database storage capacity of 200 GB/month in Guangzhou Zone 4, you will get a free backup capacity of 700 GB/month in the Guangzhou region.

If your data backups reach 800 GB and log backups reach 100 GB, your total backup capacity in Guangzhou will exceed 700 GB, and your hourly paid backup capacity will be 200 GB per hour (800 + 100 - 700 = 200).

## Backup Lifecycle

<span id = "anliang_zhouqi"></span>
### Pay-as-you-go instance
- Backups are subject to change over the instance lifecycle.
- Backups can work normally within two hours after an instance expires.
- After two hours, the instance will be isolated into the recycle bin. At this time, automatic backup will stop, and rollback and manual backup will be prohibited; however, backups can still be downloaded (on the [Backup List](https://console.cloud.tencent.com/cdb/backup) page). Excessive backup capacity will still be billed. You can renew the instance in the recycle bin in the console to recover it.
- After one day, the instance will be deactivated and terminated, along with all data backups. Please save the needed backups timely.

## Arrears Description

### Pay-as-you-go instance
After the account falls into arrears, the backup will change with the lifecycle of the instance. For more information, please see the backup lifecycle of pay-as-you-go instances as described above.


## Upgraded Services Available After Backup Billing Starts
>Listed below are maximum values supported in the same region under a single Tencent Cloud account.

| Improvement | Before Upgrade | After Upgrade |
| ------------------ | -------------- | --------------- |
| Data backup retention period | 30 days | 732 days |
| Log backup retention period | 5 days | 732 days |
| Backup compression rate | General | Ultra-high |
| binlog centralization | Local storage | Centralized storage |

## Suggestions for Reducing Backup Costs
- Delete manual backups that are no longer used (you can do so in the console) 
- Reduce the frequency of automatic data backup for non-core businesses (you can reduce the number of days for backup in a week, which should be at least 2 days)
>The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backup and log backup (binlog). Reducing the frequency of automatic backup and retention period will affect the rollback feature for instance data. Please configure backup appropriately based on your actual needs.
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of 7 days can meet the needs in most cases)

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7-732 days |
| Non-core, non-data businesses | 7 days |
| Archival businesses | 7 days. It is recommended to manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | 7 days. It is recommended to manually back up data based on your actual business needs and delete the backups promptly after use |

