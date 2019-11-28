
Envelope encryption is a high-performance encryption/decryption solution for massive amounts of data. For encryption of large files or performance-sensitive data, use the GenerateDataKey API to generate a data encryption key (DEK). Only the DEK need to be transferred to the KMS server (which are encrypted/decrypted with a CMK), and all data are processed with efficient local symmetric encryption which has little impact on user access.
In actual business scenarios where massive amounts of data needs to be encrypted with high encryption performance needed, a DEK can be generated to encrypt/decrypt local data, which not only meets the requirements for encryption performance, but also enables KMS to keep DEKs random and secure.


#### Comparison of KMS encryption schemes

| Item | Sensitive Data Encryption | Envelope Encryption |
|---------|---------|---------|
| Related key | CMK | CMK, DEK |
| Performance | Symmetric encryption, remote call | Remote symmetric encryption for small amounts of data, and local symmetric encryption for massive amounts of data.|
| Key scenarios |	Keys, certificates, and small data entries; suitable for scenarios with low call frequency | 	Massive amounts of data; suitable for scenarios with high requirements for encryption performance |


#### Schematic diagram
In this scenario, a CMK generated in KMS, as an important resource, is used to generate and get the DEK plaintext and ciphertext. Based on your actual business needs, you can first encrypt local data through the DEK plaintext in the memory and store the DEK ciphertext and ciphertext data in the disk, then decrypt the DEK ciphertext using KMS when necessary, and finally decrypt the data in the memory using the decrypted DEK plaintext.

## Features
- High efficiency: All business data is encrypted using highly efficient local symmetric encryption, which has little impact on the access experience in your business. As for the overhead of DEK creation and encryption/decryption, except in extreme cases, you need to use a "one key at a time" scheme. In most scenarios, the plaintext and ciphertext of one DEK can be reused for a certain period of time, so the overhead is generally small.
- Security and ease of use: The security of envelope encryption is protected with the key security feature of KMS. As DEKs protect business data, and KMS protects DEKs and provides increased availability, your CMK is mainly used to generate DEKs. Only authorized objects can operate on the CMK.

## Precautions
- Secure storage of `SecretId` and `SecretKey`:
	- Tencent Cloud API authentication mainly relies on `SecretId` and `SecretKey`, which are your unique credentials. Tencent Cloud's service systems need such credentials to call Tencent Cloud APIs.
- Permission control over `SecretId` and `SecretKey`:
 - It is recommended to use a sub-account and manage risks by means of API authorization as needed.
- Plaintext key processing by the business system:
 - Envelope encryption uses symmetric encryption, so plaintext keys should not be stored in the disk and need to be used in the memory during business processes.
- DEK processing by the backend system:
 - Envelope encryption uses symmetric encryption. You can reuse the same DEK as needed by your business, or use different DEKs for different users and at different times.


