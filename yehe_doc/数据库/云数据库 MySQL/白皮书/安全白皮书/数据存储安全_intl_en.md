TencentDB for MySQL ensures the confidentiality and integrity of data during storage.

## [Automatic backup](id:ZDBF)
TencentDB for MySQL supports both automatic and manual backup to ensure data restorability that guarantees data integrity and reliability. It provides data backup and log backup features by default, where the frequency of automatic backup should be set to more than twice a week. If you have other backup needs, you can initiate manual backup through the console or APIs at any time.

For more information on how to use this feature, see [Backing up Databases](https://intl.cloud.tencent.com/document/product/236/37796).

## [Archive backup retention](id:DQBFBL)
TencentDB for MySQL allows you to enable archive backup retention. You can flexibly configure the retention period of backup files as needed, which is 7 days by default and can be up to 1,830 days. Backup files that exceed the retention period will be automatically deleted. For data security considerations, we recommend you back up your data at least twice a week.

For more information on how to use this feature, see [Backing up Databases](https://intl.cloud.tencent.com/document/product/236/37796).

## [Transparent data encryption](id:TMSJJM)
TencentDB for MySQL supports the transparent data encryption (TDE) feature developed by the Tencent Cloud database team. Transparent encryption means that the data encryption and decryption are imperceptible to you. When creating an encrypted table, you do not need to specify an encryption key, and the data will be encrypted during write to the disk and decrypted during read from the disk.

TDE uses the internationally popular AES algorithm and 256-bit encryption keys, which are managed in Tencent Cloud [Key Management Service (KMS)](https://intl.cloud.tencent.com/document/product/1030/31961). You need to be authorized to access KMS and can rotate keys in the KMS console to further improve the system security.

For more information on how to use this feature, see [Enabling Transparent Data Encryption](https://intl.cloud.tencent.com/document/product/236/38491).

## [Data security](id:SJAQ)
The **sensitive data discovery** feature can automatically discover sensitive instance data via identification rules and then implement automatic classified protection on the discovered data. It supports 20 built-in rules to identify the sensitive attributes from all dataset fields while meeting the compliance requirements, ensuring that sensitive data hidden in long text can be handled properly. In addition, it supports automatic discovery of custom types of sensitive data to satisfy your personalized needs of data protection.

The **data masking** feature has many built-in advanced masking algorithms that intelligently run and manage masking tasks in different business scenarios to keep core enterprise data confidential. It guarantees security while not changing how raw data is distributed or formatted after processing, ensuring effective data uses for statistical analysis, testing, development, and training.
- In terms of compliance, data masking can use the anonymization technology to ensure that the masked data cannot be restored. This guarantees that enterprises can strictly comply with applicable laws and regulations during use of personal information and meet compliance requirements.
- In terms of system performance, data masking pulls your latest real-time backup data when starting a data masking task and completes the task dynamically online in an imperceptible manner. It doesn't stop the source database, compromise the database performance, or incur additional overheads.


