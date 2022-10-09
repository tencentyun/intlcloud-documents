## Overview
This document describes how cross-region backup is billed. The [cross-region backup](https://www.tencentcloud.com/document/product/238/49138) feature is used to store backup files in another region. After this feature is enabled, local automatic backup files will be automatically copied to the COS bucket in the destination region.

## Notes on Cross-Region Backup
- Cross-region backup doesn't affect the local default backup, and both coexist after cross-region backup is enabled.
- Cross-region backup will be triggered after the local default automatic backup is complete, that is, the default automatic backup is dumped to the storage device for cross-region backup.
- Backup files in the cross-region backup space include automatic data backups and log backups, that is, local automatic backups are automatically synced to the destination region for storage.
- Cross-region backups and local backups don't share the backup space.
- Free space is unavailable for cross-region backups. As long as cross-region backup is enabled for the instance, all the generated backup files will incur fees.
- Billable space of cross-region backups (for the region of the primary instance) = data backup volume (automatic backups in the destination region) + log backup volume (automatic backups in the destination region).
- Cross-region backups are stored in the destination region, and the backup volume is counted in the backup space for the region of the primary instance. Cross-region backup storage and traffic fees are charged based on the destination region and the linkage between the source and destination regions respectively.

## Cross-Region Backup Pricing
Cross-region backup fees consist of **storage** and **traffic** fees:

**Cross-region backup fees** = **cross-region backup storage fees** + **cross-region replication traffic fees**

For example, if an instance in Hong Kong (China) region is backed up to Beijing region, the cross-region backup will be stored in a COS bucket in Beijing region, the cross-region backup storage fees will be calculated at the storage price for Beijing region, and the cross-region backup traffic fees will be calculated based on the linkage between Hong Kong (China) and Beijing.

### Storage pricing
Cross-region backup storage fees are charged in a pay-as-you-go (postpaid) manner at the storage price of the destination region as indicated below:

| Chinese Mainland and Finance Zones | Hong Kong (China) |
|---------|---------|
| 0.000113 USD/GB/hour | 0.000127 USD/GB/hour |

>?Billable space of less than 1 GB is not billed, and a billable time period of less than one hour is counted as one hour.

### Traffic pricing
Cross-region backup traffic fees are charged based on the linkage between the source and destination regions in a pay-as-you-go (postpaid) manner at the prices as indicated below:

| Source Region of Cross-Region Backup | Destination Region of Cross-Region Backup | Traffic Price (USD/GB/Hour) |
|---------|---------|---------|
| Chinese mainland (Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, and Nanjing) | Chinese mainland (Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, and Nanjing) | 0.09230769 |
| Finance zones (Beijing Finance, Shanghai Finance, and Shenzhen Finance) | Finance zones (Beijing Finance, Shanghai Finance, and Shenzhen Finance) | 0.15384615 |
| Hong Kong (China) | Chinese mainland (Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, and Nanjing) | 0.35384615 |
| Finance zones (Beijing Finance, Shanghai Finance, and Shenzhen Finance) | Chinese mainland (Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, and Nanjing) | 0.12307692 |
| Chinese mainland (Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, and Nanjing) | Finance zones (Beijing Finance, Shanghai Finance, and Shenzhen Finance) | 0.12307692 |

## Cross-Region Backup Lifecycle
The cross-region backups of a running or isolated instance will be billed until it is deactivated.

**Pay-as-you-go instance**

- If cross-region backup is enabled, cross-region backups can be performed normally within 24 hours after the instance expires.
- After 24 hours, the instance will be isolated into the recycle bin. At this point, rollback and manual backup will be prohibited, but automatic backup can still be performed normally. If cross-region backup is enabled, it can also be performed normally, but cross-region backup settings cannot be modified. You can renew the instance in the recycle bin in the console to recover it and its backups and modify cross-region backup settings.
- After three days of isolation in the recycle bin (i.e., on the fifth day after expiration), the instance will be deactivated and terminated, along with all local and cross-region backups. Therefore, you need to save the required backup files promptly.

## Payment Overdue

**Pay-as-you-go instance**
After your account has overdue payments, cross-region backup (if enabled) will change with the lifecycle of the instance. For more information, see the backup lifecycle of pay-as-you-go instances.
