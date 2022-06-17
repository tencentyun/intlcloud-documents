## Overview
The backup space is used to store the backup files (automatic data backups, manual data backups, and log backups) of all TencentDB for MySQL instances in a region.

TencentDB for MySQL offers free-of-charge backup space per region, which equals to the sum of the storage space of all two-node and three-node instances (including the source and disaster recovery instances) in the region. For calculation examples, see [Calculation Formula](#jfgs).
>?
>- Free backup space will be provided when you purchase a source or disaster recovery instance but not a read-only instance.
>- The backup space can be viewed on the database backup page in the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/backup/index).

## Backup Pricing
Usage of backup space that exceeds the free tier will be charged at 0.000113 USD/GB/hour in the Chinese mainland. For prices for regions outside of the Chinese mainland, see [Pricing | TencentDB for MySQL](https://intl.cloud.tencent.com/pricing/cdb/calculator).
If the excessive backup space is less than 1 GB, no fees will be charged. If the time period is less than one hour, it will be calculated as one hour. TencentDB for MySQL adopts a flexible giveaway policy, so you generally don't need to pay for the backup space for most instances.

## Billing Schedule for Backup Space
- Billing officially started from 00:00 on December 2, 2019 for Hong Kong (China), Macao (China), Taiwan (China), and other regions outside the Chinese mainland.
- Billing officially started from 00:00 on December 2, 2019 for Southwest China (Chengdu and Chongqing regions).
- Billing officially started from 00:00 on December 5, 2019 for South China (Guangzhou region).
- Billing officially started from 00:00 on December 9, 2019 for North China (Beijing region).
- Billing officially started at 00:00 on December 10, 2019 for East China (Shanghai region).
- Billing is started by default for regions added after 00:00 on December 10, 2019.


## [Calculation Formula](id:jfgs)
**Free backup space in one region = Sum of storage space of all TencentDB for MySQL two-node and three-node instances in that region**

**Paid backup space in one region = Data backup volume + log backup volume - free backup space (all values are for that region)**

>?Backups of TencentDB for MySQL instances in the recycle bin will also be counted into the total backup space.

**Calculation Example**
If you have a running a TencentDB for MySQL two-node instance with a purchased database storage space of 500 GB/month in Guangzhou Zone 3 and another such instance with a purchased database storage space of 200 GB/month in Guangzhou Zone 4, you will get a free backup space of 700 GB/month in the Guangzhou region.

If your data backups reach 800 GB and log backups reach 100 GB in the current hour, your total backup space used in Guangzhou region will exceed 700 GB, and you will be billed for the excess of 200 GB (800 + 100 - 700 = 200) for the current hour and so on.


## Backup Lifecycle
### Monthly subscribed instance
- Backups are subject to change over the instance lifecycle.
- The backup feature can be used normally within seven days after an instance expires, during which backups beyond the free tier will still be billed.
- From the eighth day after expiration, the instance is isolated into the recycle bin. At this time, automatic backup stops, and rollback and manual backup are prohibited, but backups can still be downloaded (in the [Backup List](https://console.cloud.tencent.com/mysql/backup/list/data)). Excessive backup space will still be billed until the instance is eliminated. You can renew the instance in the recycle bin in the console to recover it.
- After seven days since the instance has been isolated in the recycle bin, the instance is eliminated (i.e., deleted completely) along with all data backups. Save the needed backups in a timely manner.

### [Pay-as-you-go instance](id:anliang_zhouqi)
- Backups are subject to change over the instance lifecycle.
- Backups can work normally within 24 hours after the instance payment becomes overdue.
- After 24 hours since the instance payment has been overdue, the instance is isolated into the recycle bin. At this time, automatic backup stops, and rollback and manual backup are prohibited, but backups can still be downloaded (in the [Backup List](https://console.cloud.tencent.com/mysql/backup/list/data)). Excessive backup space will still be billed until the instance is eliminated. You can renew the instance in the recycle bin in the console to recover it.
- After three days since the instance has been isolated in the recycle bin, the instance is eliminated (i.e., deleted completely) along with all data backups. Save the needed backups in a timely manner.

## Payment Overdue
### Monthly subscribed instance
- If the instance has not expired but your account has overdue payments, the backup service is downgraded, rollback, manual backup, and backup download are prohibited, but automatic back continues, where excessive backup space is still billed.
- If you need to perform rollback, manual backup, or backup download, top up your account to a positive balance.

### Pay-as-you-go instance
After the account has overdue payments, the backup will change with the lifecycle of the instance. For more information, see the backup lifecycle of pay-as-you-go instances as described above.

## Upgraded Services Available After Backup Billing Starts
>? The values listed in the table below are the maximum values supported in the same region under a single Tencent Cloud account.

| Improvement | Before Upgrade | After Upgrade |
| ------------------ | -------------- | --------------- |
| Data backup retention period | 30 days | 1,830 days |
| Log backup retention period | 5 days | 1,830 days |
| Backup compression rate | General | Ultra high |
| Binlog centralization | Local storage | Centralized storage |

## Suggestions for Reducing Backup Costs
- Delete manual backups that are no longer used. You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID or **Manage** in the **Operation** column to access the instance management page, and delete manual backups on the **Backup and Restore** tab. Automatic backups cannot be manually deleted in the console. Instead, they are automatically deleted after they expire.
- Reduce the frequency of automatic data backup for non-core businesses (you can adjust the backup cycle and backup file retention period in the console, which should be at least twice a week).
>?The [rollback feature](https://intl.cloud.tencent.com/document/product/236/7276) relies on the backup cycle and retention days of data backup and log backup (binlog). Reducing the frequency of automatic backup and retention period will affect the rollback time range for instance data. Configure backup appropriately based on your actual needs.
>
- Shorten the retention period of data and log backups for non-core businesses (a retention period of seven days can meet the needs in most cases).

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7–1,830 days |
| Non-core, non-data businesses | Seven days |
| Archival businesses | Seven days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | Seven days. We recommend you manually back up data based on your actual business needs and delete the backups promptly after use |



