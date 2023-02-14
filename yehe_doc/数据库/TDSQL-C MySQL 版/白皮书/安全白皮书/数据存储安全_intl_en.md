TDSQL-C for MySQL stores your data confidentially and maintains its integrity.

## Automatic backup
TDSQL-C for MySQL supports both automatic and manual backup to ensure data restorability that guarantees data integrity and reliability. It provides data backup and binlog backup features by default. Automatic backup is performed once a day between 2:00 AM and 6:00 AM by default. You can customize the backup start time and retention period as needed in the console. If you have other backup needs, you can also initiate manual backup through the console or APIs at any time.

For more information on how to use this feature, see [Automatic Backup](https://intl.cloud.tencent.com/document/product/1098/48399).

## Periodic backup retention
TDSQL-C for MySQL allows you to set the backup start time and retention period flexibly for higher data security. You can shorten or extend the retention period based on your business needs, which is 7 days by default and can be up to 1,830 days. Backup files that exceed the retention period will be automatically deleted.

For more information on how to use this feature, see [Setting Backup Retention Period](https://intl.cloud.tencent.com/document/product/1098/48396).


## Data security
The **sensitive data discovery** feature can automatically discover sensitive instance data via identification rules and then implement automatic classified protection on the discovered data. It supports 20 built-in rules to identify the sensitive attributes from all dataset fields while meeting the compliance requirements, ensuring that sensitive data hidden in long text can be handled properly. In addition, it supports automatic discovery of custom types of sensitive data to satisfy your personalized needs of data protection.

The **data masking** feature has many built-in advanced masking algorithms that intelligently run and manage masking tasks in different business scenarios to keep core enterprise data confidential. It guarantees security while not changing how raw data is distributed or formatted after processing, ensuring effective data uses for statistical analysis, testing, development, and training.
- In terms of compliance, data masking can use the anonymization technology to ensure that the masked data cannot be restored. This guarantees that enterprises can strictly comply with applicable laws and regulations during use of personal information and meet compliance requirements.
- In terms of system performance, data masking pulls your latest real-time backup data when starting a data masking task and completes the task dynamically online in an imperceptible manner. It doesn't stop the source database, compromise the database performance, or incur additional overheads.

For more information on how to use this feature, see [Masking Task List](https://www.tencentcloud.com/document/product/1035/48605).
