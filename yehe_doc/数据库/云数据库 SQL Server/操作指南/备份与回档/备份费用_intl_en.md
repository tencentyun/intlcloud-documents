TencentDB for SQL Server backup includes local backup and cross-region backup. The former stores the backup files of all TencentDB for SQL Server instances in a local region, while the latter stores backup files in a non-local region.

When you purchase TencentDB for SQL Server primary instances, you will receive free backup capacity. The backup space range is calculated separately for each region of an account. Excess backup files will be charged if your backup space exceeds the free tier. Note that the free tier is not applicable to cross-region backups, and as long as cross-region backup is enabled for your instances, all the generated cross-region backup files will incur fees.

This document describes backup fees. For more information, see:
- [Backup Space Billing](https://intl.cloud.tencent.com/document/product/238/45849)
- [Cross-Region Backup Billing](https://www.tencentcloud.com/document/product/238/50229)

## Local Backup Billing Mode
Backup space is billed in pay-as-you-go mode. Fees will be charged for actual backup space usage beyond the free tier.

## Local Backup Pricing 

| Chinese Mainland | Hong Kong (China) and Other Countries/Regions |
|---------|---------|
| 0.000113 USD/GB/hour | 0.000127 USD/GB/hour |

>?Billable space of less than 1 GB is not billed, and a billable time period of less than one hour is counted as one hour.

## Cross-Region Backup Billing Mode
Cross-region backup fees consist of **storage** and **traffic** fees:

**Cross-region backup fees** = **cross-region backup storage fees** + **cross-region replication traffic fees**

## Cross-Region Backup Fees

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

