## Schedule and Scope of Backup Capacity Billing
Excessive backup capacity will be charged for TencentDB for MySQL instances of High Availability Edition but not Basic Edition.

Schedule:
**TencentDB for MySQL will charge for excessive backup capacity from October 2019 on. The specific schedule will be announced separately.**

## Backup Overview
Backup capacity is used to store backup files of all TencentDB for MySQL instances in a region, including automatic data backups, manual data backups, and log backups.
TencentDB for MySQL offers a certain amount of backup capacity free of charge based on the region, which is equivalent to the sum of storage capacity of all HA instances (including master and disaster recovery instances) in your region.

> Free backup capacity will be provided when you purchase a master or disaster recovery instance but not a read-only instance.

## Backup Pricing
Excessive backup capacity will be charged at 0.0008 CNY/GB/hour in Mainland China. For prices outside Mainland China, see [TencentDB for MySQL Price Calculator](https://buy.cloud.tencent.com/price/cdb/calculator).
If the excessive backup capacity or time period is less than 1 GB or 1 hour, they will be calculated as 1 GB or 1 hour, respectively. TencentDB for MySQL adopts a flexible giveaway policy, so that you generally do not need to pay for the backup capacity for most instances.

## Backup Billing
#### Billing Formula
Free backup capacity in one region = Sum of storage capacity of all TencentDB for MySQL high availability instances in that region

Paid backup capacity in one region = Data backup volume + log backup volume - free backup capacity (all values are for that region)

>TencentDB for MySQL instance backups in the recycle bin will also be calculated for the backup capacity.

#### Billing Example
If you have a running a TencentDB for MySQL high availability instance with a purchased database storage capacity of 500 GB/month in Guangzhou Zone 3 and another such instance with a purchased database storage capacity of 200 GB/month in Guangzhou Zone 4, you will get a free backup capacity of 700 GB/month in the Guangzhou region.

If your data backups reach 800 GB and log backups reach 100 GB, your total backup capacity in Guangzhou will exceed 700 GB, and your hourly paid backup capacity will be 200 GB per hour (800 + 100 - 700 = 200).

## Upgraded Services Available After Backup Billing
> The values listed in the table below are the maximum values supported in the same region under a single Tencent Cloud account.

| Improvement | Before Billing | After Billing |
| ------------------ | -------------- | --------------- |
| Data backup retention period | 30 days | 732 days |
| Log backup retention period | 5 days | 732 days |
| Backup compression rate | General | Ultra-high |
| binlog centralization | Local storage | Centralized storage |

## How to Reduce Backup Costs?
- Delete manual backups that are no longer used (you can do so in the console)
- Reduce the frequency of automatic data backup for non-core businesses (you can reduce the number of days for backup in a week, which should be at least 2 days) 
- Shorten the retention period of data and log backups for non-core businesses (a retention period of 7 days can meet the needs in most cases)

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7-732 days |
| Non-core, non-data businesses | 7 days |
| Archival businesses | 7 days. It is recommended to manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | 7 days. It is recommended to manually back up data based on your actual business needs and delete the backups promptly after use |

