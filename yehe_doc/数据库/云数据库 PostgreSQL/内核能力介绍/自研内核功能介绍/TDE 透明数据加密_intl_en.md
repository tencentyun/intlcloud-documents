## Feature Background
As the requirements for data security protection get more and more strict, information security protection laws in many countries/regions stipulate that databases must encrypt the stored data to prevent data leakage caused by accidental loss of data files.

## Feature Description
TencentDB for PostgreSQL comes with the transparent data encryption (TDE) feature. Transparent encryption means that the data encryption and decryption are transparent to users. TDE supports real-time I/O encryption and decryption of data files. It encrypts data before it is written to disk, and decrypts data when it is read into memory from disk, which meets the compliance requirements of static data encryption. The keys used for encryption are generated and managed by KMS.

[KMS](https://Intl.cloud.tencent.com/document/product/1030) is a data and key security protection service of Tencent Cloud, where all involved processes use high-security communication protocols to guarantee high service security. In addition, it provides distributed cluster management and hot backup capabilities to ensure high service reliability and availability.

KMS uses a two-layer key system, which involves two types of keys: customer master key (CMK) and data encryption key (DEK). A CMK is used to encrypt small packet data (up to 4 KB in size), such as DEK, password, certificate, and configuration file. A DEK is used to encrypt massive amounts of business data in symmetric encryption method during storage or communication and is encrypted and protected in asymmetric encryption method with a CMK. In this way, data files can be encrypted.

## Supported Versions
Kernel version: v10.17_r1.2、v11.12_r1.2、v12.7_r1.2、v13.3_r1.2、v14.2_r1.0
## Use Cases
TDE means that the data encryption and decryption are transparent to users. TDE supports real-time I/O encryption and decryption of data files. It encrypts data before it is written to disk, and decrypts data when it is read into memory from disk, which meets the compliance requirements of static data encryption.

## Directions
For more information on how to enable TDE and encrypt a database with TDE, see [Enabling TDE](https://intl.cloud.tencent.com/document/product/409/47762).
