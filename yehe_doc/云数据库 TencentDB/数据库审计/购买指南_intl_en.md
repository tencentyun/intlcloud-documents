
## Supported Services
Database Audit currently supports:
- TencentDB for MySQL 5.6 and 5.7 (two-node and three-node) instances but not TencentDB for MySQL 5.5 or single-node instances.
- TDSQL-C for MySQL.

## Audit Price
[Database Audit](https://console.cloud.tencent.com/dls/mysql) is billed by the amount of audit log storage for every clock-hour, and usage duration shorter than one hour will be calculated as one hour.

| Region | Price (USD/GB/Hour) | 
|---------|---------|
| China (including finance regions) | 0.00147059 | 
| Other countries and regions | 0.00220588 | 

## Release
- After audit is enabled for pay-as-you-go TencentDB instances, when you release an instance, its corresponding audit service will also be stopped, and the logs will be automatically deleted and cannot be recovered.
- After audit is enabled for monthly subscribed TencentDB instances, when you release an instance or an instance is released upon expiration, its corresponding audit service will also be stopped, and the logs will be automatically deleted and cannot be recovered.

## Overdue Payments
1. **When your account balance becomes negative:**
 - You can continue to use the SQL audit service for 2 hours from the moment your account balance becomes negative. We will also continue to bill you for this period.
 - When your account has been in arrears for 2 hours, the SQL audit service will be **automatically stopped**, and billing will stop.

2. **After the service is automatically stopped:**
 - If you top up your account to a positive balance within 24 hours after the SQL audit service is automatically stopped, it will be resumed, and billing will continue; otherwise, it cannot be resumed.
 - If your account balance remains negative after 24 hours, the logs will be deleted and cannot be recovered.
