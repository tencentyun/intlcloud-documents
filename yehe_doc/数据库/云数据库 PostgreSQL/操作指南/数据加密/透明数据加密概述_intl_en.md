## Overview
Transparent Data Encryption (TDE) provides file-level encryption for data stored in the disk. It is imperceptible to applications at the upper layer of the database and doesn't require you to modify the business code. It encrypts data before it is written to disk and decrypts data when it is read from the disk in a transparent manner.

TDE is usually used to address security and compliance issues in various scenarios where the static data needs to be protected, such as PCI DSS and CCP compliance.

## Encryption
In cryptography, encryption refers to converting information in plaintext into unreadable content in ciphertext.

Modern cryptography is a study based on number and probability theories. Its ultimate goal is the perfect security (also called **information-theoretic security**) defined by Claude Shannon.

Let E = (E, D) be a Shannon cipher defined over (K,M, C). Consider a probabilistic experiment in which the random variable k is uniformly distributed over K. If for all m0, m1 ∈ M, and all c ∈ C, we have

Pr[E(k, m0) = c] = Pr[E(k, m1) = c],

then we say that E is a perfectly secure Shannon cipher.

Simply put, ciphertext `c` can be encrypted from any plaintext `m`, and its relevance to the plaintext cannot be found in itself.

## Encryption Algorithm Types
There are two types of encryption algorithms: symmetric and asymmetric.
- Symmetric encryption: The same key is used for both encryption and decryption. It is much faster than asymmetric encryption and is required in many scenarios.
- Asymmetric encryption: It is also called public-key cryptography. It uses different keys for encryption and decryption and is mainly used to transfer user information.

Common symmetric encryption algorithms include AES and 3DES. The most popular asymmetric encryption algorithm is RSA, whose reliability lies in the difficulty in factorizing extremely large integers.

## TDE Threat Model
TDE is mainly used to protect static data (data at rest) to prevent data leakage caused by disk theft.

## TencentDB for PostgreSQL Data Encryption Implementation
TencentDB for PostgreSQL applies to use the CMK stored in KMS to generate the DEK ciphertext and plaintext. Then, it uses them to encrypt and decrypt the keys used to encrypt Tencent Cloud product data.
![img](https://main.qcloudimg.com/raw/beb03cab3bc4157e94661a78904d34fd.png)
This encryption scheme is called envelope encryption, where a key is used to encrypt another key. It has a high performance in encrypting and decrypting massive amounts of data. Specifically, it can generate DEKs to encrypt and decrypt local data, which guarantees the randomness and security of data keys based on KMS while meeting the requirements for robust business encryption.

As encryptions and decryptions are in-memory operations, the database will get key materials from KMS every time it is restarted or its memory is closed. No key materials used for decryption are stored in the local storage.
![](https://qcloudimg.tencent-cloud.cn/raw/9b2db6c35942d31a692f57e87937cea5.png)
