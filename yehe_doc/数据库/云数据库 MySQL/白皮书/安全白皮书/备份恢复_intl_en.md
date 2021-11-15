### Backup
TencentDB for MySQL supports both automatic and manual backup to ensure data restorability that guarantees data integrity and reliability. It provides data backup and log backup features by default, where the frequency of automatic backup should be set to higher than twice a week. If you have other backup needs, you can initiate manual backup through the [console](https://console.cloud.tencent.com/cdb) or APIs at any time.

In addition, you can flexibly configure the retention period of backup files as needed, which is 7 days by default and can be up to 732 days. Backup files that exceed the retention period will be automatically deleted.

For more information on how to use this feature, please see [Backup Mode](https://intl.cloud.tencent.com/document/product/236/32340).

### Restoration
TencentDB for MySQL is capable of data restoration. You can use the rollback feature to restore data to any time point within the retention period as needed. As the time points available for data restoration are subject to the retention period, you should configure a reasonable backup retention policy based on your business needs to ensure data restorability.

For more information on how to use this feature, please see [Database Rollback](https://intl.cloud.tencent.com/document/product/236/7276).
