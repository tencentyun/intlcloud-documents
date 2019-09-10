## Overview
Envelope encryption is a high-performance encryption and decryption solution for massive amounts of data. For encryption of large files or performance-sensitive data, use the GenerateDataKey API to generate AES data encryption keys (DEKs). Only DEKs need to be transferred to the KMS server (which are encrypted and decrypted with the CMK), and all data is processed with efficient local symmetric encryption which has little impact on user access.

### Schematic Diagram
![](https://main.qcloudimg.com/raw/742563a8fdd4d43414201b17c8a08fa3.png)

## Directions
### Creating a Plaintext DEK

1. Create an AES-256 DEK using the TencentCloud KMS API. For detailed directions, see [Generating a DEK](https://intl.cloud.tencent.com/document/product/1030/32188).
2. You can also create one using a third-party tool or development library (such as OpenSSL).

### Creating and Saving a Ciphertext DEK

1. The ciphertext DEK can be created by encrypting the plaintext using the TencentCloud KMS API or an online tool. For detailed directions, see [Encryption and Decryption](https://intl.cloud.tencent.com/document/product/1030/31973).
2. The ciphertext DEK is stored on your own. In common implementation solutions, the DEK is stored together with ciphertext business data; for example, it can be stored in a container or space that can be accessed in a similar way in storage scenarios. In communication scenarios, the ciphertext DEK and business data together form a message.

## Advantages

### High Efficiency
All data is encrypted using highly efficient local symmetric encryption, which has little impact on user access. Except in extreme situations, you generally only need to use one key for each operation. In most cases, the plaintext and ciphertext of one DEK can be reused for a certain period of time, so costs incurred for DEK and encryption and decryption is usually small.

### Security and Ease of Use
The security of Envelope Encryption is similar to a common public key system. Since DEK protects business data, and Tencent Cloud KMS protects DEK and provides increased availability, your CMK is never disclosed. Only the object authorized to access with the key can operate on CMK.

## When should I use Envelope Encryption in the cloud?

1. **Large file size**: Currently, KMS API supports the encryption and decryption of data under 4 KB in size.
2. **Massive amounts of data with low latency required**: Most users want to encrypt their data, but access delay is a major concern. Although the KMS backend is extremely high in performance, it only supports remote call and uses asymmetric encryption. Envelope Encryption uses high-performance local symmetric encryption for most operations.

### Comparison of Common Solutions
| | Sensitive Information Encryption | Envelope Encryption|
|-|:-:|:-:|
| Related key | CMK | CMK, DEK |
| Performance | Asymmetric encryption, remote call | Remote asymmetric encryption for small amount of data, and local symmetric encryption for massive amounts of data |
| Key scenarios | Keys, certificates, small data entries | Massive amounts of data |
