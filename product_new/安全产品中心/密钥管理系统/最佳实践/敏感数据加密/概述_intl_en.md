Sensitive information encryption is a core capability of KMS, which is mainly used to protect small pieces of sensitive data (less than 4 KB) such as keys, certificates, and configuration files. A CMK is used to encrypt sensitive data instead of storing it in plaintext. During decryption, the data ciphertext is decrypted to the memory, so that the plaintext does not get stored in the disk. HTTPS requests are used in the entire interaction and transfer process, ensuring the security of sensitive data.

If you need to use KMS for high-performance encryption/decryption of massive amounts of data, please see [Envelope Encryption](https://cloud.tencent.com/document/product/573/8791) scenario.

#### Examples of sensitive information

| - | Key/Certificate | Backend Configuration File |
|-|:-:|:-:|
| Usage | Encrypts business data, communication channels, and digital signatures. | Stores system architecture and other business information, such as database IP and password. |
| Risk of data loss | Confidential information is stolen; encrypted tunnels are monitored; signatures are faked. | Business data is breached and used to attack other systems. | 


#### Schematic diagram

In this scenario, sensitive data is encrypted/decrypted through a CMK, which is protected by a third-party certified hardware security module (HSM). The CMK performs encryption/decryption inside the HSM, and any unauthorized party, including Tencent Cloud, has no access to the CMK in plaintext.

![](https://main.qcloudimg.com/raw/f52c0a8bc2398d310c7641f809450b9f.png)



## Features

- Permission control: Fully integrated with CAM, KMS can control which accounts have access to your CMK through identity and policy management.
- Built-in audit: KMS is integrated with CloudAudit to record all API requests for detailed statistics of key management activities and key usage, ensuring that all data operations can be traced and audited.
- Integrated key management: KMS enables centralized management of keys from various applications.
- Security and compliance: KMS leverages a State Cryptography Administration of China or FIPS-140-2 certified hardware security module (HSM) to generate and protect keys, thereby ensuring their confidentiality, integrity, and availability.
- Sensitive data encryption: KMS supports encryption/decryption of small pieces of sensitive data (less than 4 KB), such as keys, certificates, and configuration files.


## Precautions
- Secure storage of `SecretId` and `SecretKey`:
	- Tencent Cloud API authentication mainly relies on `SecretId` and `SecretKey`, which are your unique credentials. Tencent Cloud's service systems need such credentials to call Tencent Cloud APIs.
- Permission control over `SecretId` and `SecretKey`:
	- It is recommended to use a sub-account and manage risks by means of API authorization as needed.
- Plaintext data storage:
 - Data has already encrypted through sensitive data encryption. To ensure data security, please make sure that the original plaintext data is deleted.
