## Overview
The backup space is used to store the backup files (automatic data backups, manual data backups, and log backups) of all TencentDB for MySQL instances in a region. TencentDB for MySQL supports transition-to-cold storage, so automatic data backups include non-archive data backups, standard storage backups, and archive storage backups, and log backups include non-archive log backups, standard storage log backups, and archive storage log backups.

- For two-node and three-node instances of local disk edition, TencentDB for MySQL offers free-of-charge backup space per region, which equals to the sum of the storage space of all two-node and three-node instances (including the source and disaster recovery instances) in the region. For calculation examples, see [Calculation Formula](#jfgs).
>?
>- Free backup space will be provided when you purchase a source or disaster recovery instance but not a read-only instance.
>- The backup space of instances of local disk edition can be viewed on the **Database Backup** page in the [TencentDB for MySQL console](https://console.cloud.tencent.com/mysql/backup/index).
>- The free space is not applicable to transition-to-cold storage.

- For single-node instances of cloud disk edition, TencentDB for MySQL offers a free tier of backup space at the instance level, which equals to 200% of the storage space of each instance.
>?The backup space of instances of cloud disk edition can be viewed on the **Backup and Restoration** tab.
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/HMH5870_24.png)

## Free Tier Comparison

| Storage Type | Free Tier | Level |
|---------|---------|---------|
| Cloud disk | 200% of the storage space | Instance level. For example, if the storage space of a single-node instance of cloud disk edition is 50 GB, the instance enjoys a free tier of backup space of 100 GB. | 
| Local disk | 100% of the storage space | Region level. For example, if Tencent Cloud account A has two two-node instances in Beijing region with a storage space of 50 GB and 80 GB respectively, the account enjoys a free tier of backup space of 130 GB in Beijing region. | 


## Backup Pricing of Single-Node Instances of Cloud Disk Edition
Backup space in excess of the free tier is priced at 0.00003676 USD/GB/hour in the Chinese mainland and 0.00004118 USD/GB/hour outside the Chinese mainland.
Single-node instances of cloud disk edition are currently supported in Shanghai, Chengdu, Guangzhou, and Beijing, with more regions to come in the future.

## Backup Pricing of Instances of Local Disk Edition
Backup space in excess of the free tier is priced at 0.000113 USD/GB/hour in the Chinese mainland and 0.000127 USD/GB/hour outside the Chinese mainland.
If the excessive backup space is less than 1 GB, no fees will be charged. If the time period is less than one hour, it will be calculated as one hour. TencentDB for MySQL adopts a flexible giveaway policy, so you generally don't need to pay for the backup space for most instances.

## Notes on Cross-Region Backup and Billing[](id:kdybfjjfsm)
TencentDB for MySQL supports cross-region backup for compliance or disaster recovery. You can enable this feature in the console as instructed in [Cross-Region Backup](https://www.tencentcloud.com/zh/document/product/236/50652). Once enabled, cross-region backup doesn't affect the local default backup, and they can both coexist with their own retention periods. Upon completion, the automatic backup is dumped to the storage device for cross-region backup.

>!Cross-region backup and log files cannot use the free storage space; instead, they use the space in the backup region of the source instance.

Cross-region backup space is priced at 0.000113 USD/GB/hour in the Chinese mainland and 0.000127 USD/GB/hour outside the Chinese mainland.
The cross-region backup feature is currently available in Beijing, Shanghai, Guangzhou, Shenzhen, and Chengdu, with more regions to come in the future.

[](id:BFLLJFSM)

## Transition-to-Cold Storage Billing
TencentDB for MySQL supports transition-to-cold storage for backup files to reduce the backup storage costs. You can configure to transition backup files to standard storage and then to archive storage in the console as instructed in [Configuring Transition-to-Cold Storage](https://www.tencentcloud.com/document/product/236/53949). The prices of these two storage types are as follows:
>!
>- The free space is not applicable to transition-to-cold storage.
>- The archive storage type isn't available yet.

### Standard storage pricing
Standard storage fees are charged in a pay-as-you-go (postpaid) manner at the storage price of the region as listed below:

| Region | Price (USD/GB/Hour) | 
|---------|---------|
| Beijing, Nanjing, Shanghai, Guangzhou | 0.00002651 | 
| Chengdu, Chongqing | 0.00002224 | 
| Virginia | 0.00002808 | 
| Silicon Valley | 0.00002921 | 
| Tokyo, Toronto, Frankfurt | 0.00003325 | 
| Singapore | 0.00003775 | 
| Hong Kong (China), Seoul, Bangkok, São Paulo, Jakarta | 0.00003505 | 
| Shenzhen Finance, Shanghai Finance | 0.0000674 | 

### Archive storage pricing
Archive storage fees are charged in a pay-as-you-go (postpaid) manner at the storage price of the region as listed below:

| Region | Price (USD/GB/Hour) |
|---------|---------|
| Beijing, Nanjing, Shanghai, Guangzhou | 0.00000741 |
| Chengdu, Chongqing, Silicon Valley, Virginia | 0.00000674 |
| Toronto, Frankfurt | 0.00000696 |
| Hong Kong (China), Tokyo, Seoul, Bangkok, São Paulo, Singapore | 0.00000764 |
| Shenzhen Finance | 0.00002247 |

## Billing Schedule for Backup Space
- Billing officially started from 00:00 on December 2, 2019 for Hong Kong (China), Macao (China), Taiwan (China), and other regions outside the Chinese mainland.
- Billing officially started from 00:00 on December 2, 2019 for Southwest China (Chengdu and Chongqing regions), South China (Shenzhen Finance), East China (Shanghai Finance), and North China (Beijing Finance).
- Billing officially started from 00:00 on December 5, 2019 for South China (Guangzhou region).
- Billing officially started from 00:00 on December 9, 2019 for North China (Beijing region).
- Billing officially started at 00:00 on December 10, 2019 for East China (Shanghai region).
- Billing is started by default for regions added after 00:00 on December 10, 2019.

## [Calculation Formula](id:jfgs)
- **Backup space calculation formula for instances of local disk edition**:
 - **Free backup space in one region = Sum of storage space of all TencentDB for MySQL two-node and three-node instances in that region**
 - **Paid backup space in one region = Data backup volume + log backup volume - free backup space (all values are for that region)**

- **Backup space calculation formula for instances of cloud disk edition**:
 - **Free backup space of one instance** = **200% of the storage space of that instance** 
 - **Paid backup space of one instance = data backup volume + log backup volume - free backup space (all values are for that instance)**

>?Backups of TencentDB for MySQL instances in the recycle bin will also be counted into the total backup space.

**Calculation Example**
If you have a running a TencentDB for MySQL two-node instance with a purchased database storage space of 500 GB/month in Guangzhou Zone 3 and another such instance with a purchased database storage space of 200 GB/month in Guangzhou Zone 4, you will get a free backup space of 700 GB/month in the Guangzhou region.

If your data backups reach 800 GB and log backups reach 100 GB in the current hour, your total backup space used in Guangzhou region will exceed 700 GB, and you will be billed for the excess of 200 GB (800 + 100 - 700 = 200) for the current hour and so on.


## Backup Lifecycle
### Monthly subscribed instance
- Backups are subject to change over the instance lifecycle.
- The backup feature can be used normally **within seven days** after an instance expires, during which backups beyond the free tier will still be billed.
- From the eighth day after expiration, the instance is isolated and moved into the recycle bin. At this time, automatic backup stops, and rollback and manual backup are prohibited, but backups can still be downloaded in the [Backup List](https://console.cloud.tencent.com/mysql/backup/list/data) page. Excessive backup space will still be billed until the instance is eliminated. You can renew the instance in the recycle bin in the console to recover it.
- After seven days since the instance has been isolated in the recycle bin, the instance is eliminated (i.e., deleted completely) along with all data backups. Save the needed backups in a timely manner.

### [Pay-as-you-go instance](id:anliang_zhouqi)
- Backups are subject to change over the instance lifecycle.
- Backups can work normally within 24 hours after the instance payment becomes overdue.
- After 24 hours since the instance payment has been overdue, the instance is isolated and moved into the recycle bin. At this time, automatic backup stops, and rollback and manual backup are prohibited, but backups can still be downloaded on the [Backup List](https://console.cloud.tencent.com/mysql/backup/list/data) page. Excessive backup space will still be billed until the instance is eliminated. You can renew the instance in the recycle bin in the console to recover it.
- After three days since the instance has been isolated in the recycle bin, the instance is eliminated (i.e., deleted completely) along with all data backups. Save the needed backups in a timely manner.

## Payment Overdue
### Monthly subscribed instance
- If the instance has not expired but your account has overdue payments, the backup service is downgraded, rollback, manual backup, and backup download are prohibited, but automatic backup continues, where excessive backup space is still billed.
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
- Reduce the frequency of automatic data backup for non-core businesses. You can adjust the backup cycle and backup file retention period in the console, which should be at least twice a week.
>?The rollback feature relies on the backup cycle and retention days of data backups and log backups (binlog). Rollback will be affected if you reduce the automatic backup frequency and retention period. You can select the parameters as needed. For more information, see [Rolling back Databases](https://intl.cloud.tencent.com/document/product/236/7276).
>
- Shorten the retention period of data and log backups for non-core businesses. A retention period of seven days can meet the needs in most cases.
- Configure the transition-to-cold storage policy to transition backup files and reduce the storage costs. For more information, see [Configuring Transition-to-Cold Storage](https://www.tencentcloud.com/document/product/236/53949).

| Business Scenario | Recommended Backup Retention Period |
| -------------------- | ------------------------------------------------------------ |
| Core businesses | 7-1,830 days |
| Non-core, non-data businesses | 7 days |
| Archival businesses | 7 days. We recommend that you manually back up data based on your actual business needs and delete the backups promptly after use |
| Testing businesses | 7 days. We recommend that you manually back up data based on your actual business needs and delete the backups promptly after use |
