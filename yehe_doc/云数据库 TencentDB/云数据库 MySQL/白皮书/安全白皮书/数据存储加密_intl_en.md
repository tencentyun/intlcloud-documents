TencentDB for MySQL supports the [Enabling Transparent Data Encryption](https://intl.cloud.tencent.com/document/product/236/38491)  feature developed by the Tencent Cloud database team. Transparent encryption means that the data encryption and decryption are imperceptible to you. When creating an encrypted table, you do not need to specify an encryption key, and the data will be encrypted during write to the disk and decrypted during read from the disk.

TDE uses the internationally popular AES algorithm and 256-bit encryption keys, which are managed in Tencent Cloud [KMS](https://intl.cloud.tencent.com/document/product/1030/31961). You need to be authorized to access KMS and can rotate keys in the KMS Console to further improve the system security.

