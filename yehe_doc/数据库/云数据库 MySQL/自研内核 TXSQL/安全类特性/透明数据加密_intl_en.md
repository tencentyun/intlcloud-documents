## Overview
TXSQL inherits the transparent data encryption mechanism of MySQL and provides another implementation of the keyring plugin: keyring KMS, which integrates keyring with Tencent Cloud's enterprise-grade [Key Management Service (KMS)](https://intl.cloud.tencent.com/zh/document/product/1030) service.

KMS is a data and key security protection service of Tencent Cloud, where all involved processes use high-security communication protocols to guarantee high service security. In addition, it provides distributed cluster management and hot backup capabilities to ensure high service reliability and availability.

KMS uses a two-layer key system, which involves two types of keys: customer master key (CMK) and data encryption key (DEK). A CMK is used to encrypt small packet data (up to 4 KB in size), such as DEK, password, certificate, and configuration file. A DEK is used to encrypt massive amounts of business data in symmetric encryption method during storage or communication and is encrypted and protected in asymmetric encryption method with a CMK. In this way, data can be encrypted both in the memory and files.

## Supported Versions
- Kernel version: MySQL 5.7 20171130 and later.
- Kernel version: MySQL 8.0 20200630 and later.

## Use Cases
Transparent data encryption means that data encryption/decryption operations are imperceptible to users. It supports real-time I/O encryption/decryption of data files; that is, data will be encrypted before being written to the disk and decrypted when being read from the disk into the memory. This helps meet the compliance requirements for static data encryption.

## Instructions
For more information, see [Enabling Transparent Data Encryption](https://intl.cloud.tencent.com/document/product/236/38491).
