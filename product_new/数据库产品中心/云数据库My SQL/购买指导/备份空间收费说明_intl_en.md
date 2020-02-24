## Overview
Backup capacity is used to store backup files of all TencentDB for MySQL instances in a region, including automatic data backups, manual data backups, and log backups.

TencentDB for MySQL offers a certain amount of backup capacity free of charge based on the region, which is equivalent to the sum of storage capacity of all high availability instances (including master and disaster recovery instances) in your region.
> Free backup capacity will be provided when you purchase a master or disaster recovery instance but not a read-only instance.

## Backup Pricing
Excessive backup capacity will be charged at 0.000127 USD/GB/hour.
If the excessive backup capacity is less than 1 GB, no fees will be incurred. If the time period is less than 1 hour, it will be calculated as 1 hour for billing. TencentDB for MySQL adopts a flexible giveaway policy, so that you generally do not need to pay for the backup capacity for most instances.

## Billing Schedule
**TencentDB for MySQL will charge for excessive backup capacity from October 2019 on. The specific schedule will be announced separately.**

## Calculation Formula

**Free backup capacity in one region = Sum of storage capacity of all TencentDB for MySQL high availability instances in that region**

**Paid backup capacity in one region = Data backup volume + log backup volume - free backup capacity (all values are for that region)**

>TencentDB for MySQL instance backups in the recycle bin will also be calculated for the backup capacity.

**Calculation Example**
If you have a running a TencentDB for MySQL high availability instance with a purchased database storage capacity of 500 GB/month in Guangzhou Zone 3 and another such instance with a purchased database storage capacity of 200 GB/month in Guangzhou Zone 4, you will get a free backup capacity of 700 GB/month in the Guangzhou region.

If your data backups reach 800 GB and log backups reach 100 GB, your total backup capacity in Guangzhou will exceed 700 GB, and your hourly paid backup capacity will be 200 GB per hour (800 + 100 - 700 = 200).

## Note on Arrears


### Pay-as-you-go Instances
- Backups are subject to change over the instance lifecycle.
- Backups can work normally within two hours after an instance expires.
- After two hours, the instance will be isolated into the recycle bin. At this time, auto backup will stop and manual backup will be prohibited.
- After one day, the instance will be deactivated and terminated, along with all data backups. Please save the needed backups in a timely manner.

 
