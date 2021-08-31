## Overview
Backup space is used to store backup files of all TencentDB for MySQL instances in a region, including automatic data backups, manual data backups, and log backups.

TencentDB for MySQL offers a certain amount of backup space free of charge based on the region, which is equivalent to the sum of storage capacity of all High-Availability Edition and Finance Edition instances (including master and disaster recovery instances) in your region.
>?
>- Free backup space will be provided when you purchase a master or disaster recovery instance but not a read-only instance.
>- The backup space can be viewed on the database backup page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/backup).

## Backup Pricing
Excessive backup space will be charged at 0.000127 USD/GB/hour in Mainland China. For prices outside Mainland China, please see [TencentDB for MySQL Price Calculator](https://buy.cloud.tencent.com/price/cdb/calculator).
If the excessive backup space is less than 1 GB, no fees will be charged. If the time period is less than 1 hour, it will be calculated as 1 hour. TencentDB for MySQL adopts a flexible giveaway policy, so that you generally do not need to pay for the backup space for most instances.

## Billing Schedule for Backup Space
- Billing officially started from 00:00 on December 2, 2019 for Hong Kong (China), Macao (China), Taiwan (China), and other regions outside Mainland China.
- Billing officially started from 00:00 on December 2, 2019 for Southwest China (Chengdu and Chongqing regions).
- Billing officially started from 00:00 on December 5, 2019 for South China (Guangzhou region).
- Billing officially started from 00:00 on December 9, 2019 for North China (Beijing region).
- Billing officially started at 00:00 on December 10, 2019 for East China (Shanghai region).
- Billing is started by default for regions added after 00:00 on December 10, 2019.


## Calculation Formula

**Free backup space in one region = Sum of storage capacity of all TencentDB for MySQL High-Availability Edition and Finance Edition instances in that region**

**Paid backup space in one region = Data backup volume + log backup volume - free backup space (all values are for that region)**

>?TencentDB for MySQL instance backups in the recycle bin will also be counted into the backup space.

**Calculation example**
If you have a running a TencentDB for MySQL High-Availability Edition instance with a purchased database storage capacity of 500 GB/month in Guangzhou Zone 3 and another such instance with a purchased database storage capacity of 200 GB/month in Guangzhou Zone 4, you will get a free backup space of 700 GB/month in the Guangzhou region.

If your data backups reach 800 GB and log backups reach 100 GB, your total backup capacity in Guangzhou will exceed 700 GB, and your hourly paid backup capacity will be 200 GB per hour (800 + 100 - 700 = 200), and so on.

## Backup Lifecycle

<span id = "anliang_zhouqi"></span>
### Pay-as-You-Go instance
- Backups are subject to change over the instance lifecycle.
- Backups can work normally within 24 hours after an instance expires.
- After 24 hours, the instance will be isolated into the recycle bin. At this time, automatic backup will stop, and rollback and manual backup will be prohibited; however, backups can still be downloaded (on the [Backup List](https://console.cloud.tencent.com/cdb/backup) page). Excessive backup space of the instance will not be billed. You can renew the instance in the recycle bin in the console to recover it.
- After three days in the recycle bin, the instance will be deactivated and terminated, along with all data backups. Please save the needed backups in a timely manner.

## Notes on Overdue Payment

### Pay-as-You-Go instance
After the account becomes overdue, the backup will change with the lifecycle of the instance. For more information, please see the backup lifecycle of pay-as-you-go instances as described above.


## Upgraded Services Available After Backup Billing Starts
>?Listed below are maximum values supported in the same region under a single Tencent Cloud account.

| Improvement | Before Upgrade | After Upgrade |
| ------------------ | -------------- | --------------- |
| Data backup retention period | 30 days | 732 days |
| Log backup retention period | 5 days | 732 days |
| Backup compression rate | General | Ultra-high |
| binlog centralization | Local storage | Centralized storage |

## Suggestions for Reducing Backup Costs
- Delete manual backups that are no longer used (you can do so on the instance management > backup and restore page in the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). Automatic backups will be automatically deleted upon expiration but cannot be manually deleted in the console). 
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup frequency and backup file retention period in the console, which should be at least twice a week).
>?The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup frequency and retention days of data backup and log backup (binlog). Reducing the frequency of automatic backup and retention period will affect the rollback time range for instance data. Please configure backup appropriately based on your actual needs.
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of 7 days can meet the needs in most cases)

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7–732 days |
| Non-core, non-data businesses | 7 days |
| Archival businesses | 7 days. You are recommended to manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | 7 days. You are recommended to manually back up data based on your actual business needs and delete the backups promptly after use |


