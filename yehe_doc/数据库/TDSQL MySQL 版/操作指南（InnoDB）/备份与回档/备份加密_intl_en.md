## Feature Overview
TDSQL for MySQL offers the transparent data encryption (TDE) feature that makes data encryption and decryption transparent to users. TDE supports data file encryption and decryption in real time. It allows data files to be encrypted before being written to disk and decrypted when read into memory from disk, meeting the static data encryption compliance requirements.

TDE is only supported for Percona 5.7 in Hong Kong region, but it will be available to more kernel versions in the future. You can access **Data Security** > **Data Encryption** on the instance management page in the [TDSQL console](https://console.cloud.tencent.com/tdsqld/instance-tdmysql)

After data encryption is enabled, the database instances can’t be restored from a backup file. It is recommended to restore them as instructed in [Rolling Back Database](https://intl.cloud.tencent.com/document/product/1042/47382). 
>?To use the data encryption feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.


## Notes
- Currently, you can’t create disaster recovery read-only instances for the instance with KMS enabled. For more information about KMS, see [Getting Started](https://intl.cloud.tencent.com/document/product/1030/32774) with KMS.
- TDE can't be disabled once enabled.
- TDE enhances the security of static data while compromising the read-write performance of encrypted databases. Therefore, use it based on your actual needs.
- After TDE is enabled, more CPU resources will be consumed, and about 5% of the performance will be compromised.
