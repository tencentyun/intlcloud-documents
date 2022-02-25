## Overview
The backup space is used to store the backups of all TencentDB for MySQL instances in a region. These backups can be automatic, manual, and log backups.

TencentDB for MySQL offers a certain amount of backup capacity for free based on the region. The capacity is equivalent to the sum of the storage capacity of all two-node and three-node instances (including source and disaster recovery instances) in the region. For calculation examples, see [Calculation Formula](#jfgs).
>?
>- Free backup space is provided when purchasing a source or disaster recovery instance but will not be available in case of a read-only instance.
>- The backup capacity can be viewed on the database backup page in the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/backup/index).

## Backup Pricing
Usage of backup capacity that exceeds the free tier will be charged at 0.000127 USD/GB/hour in the Chinese mainland. For prices for regions outside of the Chinese mainland, see [TencentDB for MySQL Price Calculator](https://buy.intl.cloud.tencent.com/price/cdb/calculator).
If the excessive backup capacity is less than 1 GB, no fees will be charged. If the time period is less than 1 hour, it will be calculated as 1 hour. TencentDB for MySQL adopts a flexible giveaway policy, so that you generally do not need to pay for the backup capacity for most instances.

## Billing Schedule for Backup Capacity
- Billing officially started from 00:00 on December 2, 2019 for Hong Kong (China), Macao (China), Taiwan (China), and other regions outside the Chinese mainland.
- Billing officially started from 00:00 on December 2, 2019 for Southwest China (Chengdu and Chongqing regions).
- Billing officially started from 00:00 on December 5, 2019 for South China (Guangzhou region).
- Billing officially started from 00:00 on December 9, 2019 for North China (Beijing region).
- Billing officially started at 00:00 on December 10, 2019 for East China (Shanghai region).
- Billing is started by default for regions added after 00:00 on December 10, 2019.


## [Calculation Formula](id:jfgs)
**Free backup capacity in one region = Sum of storage capacity of all TencentDB for MySQL two-node and three-node instances in that region**

**Paid backup capacity in one region = Data backup volume + log backup volume - free backup capacity (all values are for that region)**

>?Backups of TencentDB for MySQL instances in the recycle bin will also be counted into the total backup capacity.

**Calculation Example**
If you have a running a TencentDB for MySQL two-node instance with a purchased database storage capacity of 500 GB/month in Guangzhou Zone 3 and another such instance with a purchased database storage capacity of 200 GB/month in Guangzhou Zone 4, you will get a free backup capacity of 700 GB/month in the Guangzhou region.

Usage of backup capacity that exceeds the free tier are calculated on an hourly basis according to the following rule. For example, if your data backups reach 800 GB and log backups reach 100 GB, your total backup capacity usage in Guangzhou will exceed 700 GB, and your hourly billable backup capacity will be 200 GB (800 + 100 - 700 = 200).


## Backup Lifecycle
### [Pay-as-You-Go instance](id:anliang_zhouqi)
- Backups are subject to change over the instance lifecycle.
- Backups can work normally within 24 hours after the instance payment becomes overdue.
- After 24 hours since the instance payment has been overdue, the instance is isolated into the recycle bin. At this time, automatic backup stops, and rollback and manual backup are prohibited, but backups can still be downloaded (on the [Backup List](https://console.cloud.tencent.com/mysql/backup/list/data). Excessive backup capacity will still be billed until the instance is eliminated. You can renew the instance in the recycle bin in the console to recover it.
- After three days since the instance has been isolated in the recycle bin, the instance is eliminated (i.e., deleted completely) along with all data backups. Please save the needed backups in a timely manner.

## Payment Overdue
### Pay-as-You-Go instance
After the account falls into arrears, the backup will change with the lifecycle of the instance. For more information, see backup lifecycle of pay-as-you-go instances as described above.

## Upgraded Services Available After Backup Billing Starts
>? The values listed in the table below are the maximum values supported in the same region under a single Tencent Cloud account.

| Improvement | Before Upgrade | After Upgrade |
| ------------------ | -------------- | --------------- |
| Data backup retention period | 30 days | 1,830 days |
| Log backup retention period | 5 days | 1,830 days |
| Backup compression rate | General | Ultra-High |
| binlog centralization | Local storage | Centralized storage |

## Suggestions for Reducing Backup Costs
- Delete the manual backups which are no longer needed. You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID or **Manage** in the **Operation** column to access the instance management page, and delete manual backups on the **Backup and Restoration** tab. Automatic backups cannot be manually deleted in the console. Instead, they are automatically deleted after they expire.
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and retention period in the console, and the frequency should be at least twice a week).
>?The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backups and log backups (binlog). Rollback will be affected if you reduce the automatic backup frequency and retention period. Please select the parameters as needed.
>
- Reduce the retention period of data and log backups for non-core businesses (a 7-day retention period can meet the requirements of most scenarios).

| Business Scenario             | Recommended Backup Retention Period                                                 |
| -------------------- | ------------------------------------------------------------ |
| Core businesses             | 7-1,830 days                                              |
| Non-core and non-data businesses | 7 days                                                      |
| Archive businesses             | 7 days. We recommend that you manually back up data based on your business needs and delete the backups promptly after use |
| Testing businesses | 7 days. We recommend that you manually back up data based on your actual business needs and delete the backups promptly after use |

