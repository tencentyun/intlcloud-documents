## Overview
TencentDB for MariaDB comes with the transparent data encryption (TDE) feature. Transparent encryption means that the data encryption and decryption are transparent to users. TDE supports real-time I/O encryption and decryption of data files. It encrypts data before it is written to disk, and decrypts data when it is read into memory from disk, which meets the compliance requirements of static data encryption.

This document describes how to enable data encryption and encrypt/decrypt data in the console.

## Limits
- The TDE feature is currently supported only for MySQL 8.0.24 or later and Percona 5.7.
>?To use TDE feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.
- [KMS](https://intl.cloud.tencent.com/document/product/1030/32774) must be activated in advance or as prompted when TDE is enabled.
- KMS key permissions must be granted in advance or as prompted when TDE is enabled.

## Notes
- After KMS is activated, KMS fees may be incurred as detailed in [Purchase Method](https://intl.cloud.tencent.com/document/product/1030/31967).
- TDE can't be disabled once enabled.
- If disaster recovery read-only instances are created, TDE cannot be enabled.
- After TDE is enabled, disaster recovery read-only instances cannot be created.
After TDE is enabled, the database instances can't be restored from a backup file. You recommend that you restore them as instructed in [Rolling back Databases](https://intl.cloud.tencent.com/document/product/237/8719).
- TDE enhances the security of static data while compromising the read-write performance of encrypted databases. Therefore, use it based on your actual needs.
- After TDE is enabled, more CPU resources will be consumed, and about 5% of the performance will be compromised.

## Directions
1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb). Click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Data Security** > **Data Encryption** and toggle on **Encryption Status**.
![](https://qcloudimg.tencent-cloud.cn/raw/e51114f20679d505a825653ce73fc358.png)
3. In the pop-up dialog box, activate the KMS, grant the KMS key permissions, select a key, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/30844c6a9b6e3adb397d7fc1d0c02ec4.png)
4. After data encryption is enabled, you must perform DDL operations on the database table to encrypt or decrypt data. The detailed steps are as follows:
 - Encrypt a new table:
```
CREATE TABLE t1 (c1 INT) ENCRYPTION='Y'
```
 - Encrypt an existing table:
```
ALTER TABLE t1 ENCRYPTION='Y'
```
 - Decrypt a table:
```
ALTER TABLE t1 ENCRYPTION='N'
```
