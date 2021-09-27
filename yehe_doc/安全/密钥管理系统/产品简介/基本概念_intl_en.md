This guide describes basic concepts in Key Management Service (KMS).

### Key lifecycle

Key lifecycle refers to a set of operations including generating, saving, distributing, importing, exporting, applying, restoring, archiving and terminating keys. KMS provides a full lifecycle management to manage keys in a safe manner and prevent key leaks.

### Symmetric encryption and decryption

Symmetric encryption and decryption is a data encryption technique where the same key is used to both encrypt and decrypt the data.
>?KMS supports symmetric encryption and decryption. For more details, see [**Symmetrical Encryption and Decryption**](https://intl.cloud.tencent.com/document/product/1030/31975).

### Asymmetric encryption and decryption

Asymmetric encryption and decryption is a type of encryption that uses a pair of keys (public key and private key) to encrypt and decrypt data. The public key is used by a sender to encrypt data and only the receiver can decrypt the data with the matched private key. On the other hand, the sender can use the private key to sign a confidential message, while the receiver can verify the message using the matched public key.
>?KMS also supports asymmetric encryption and decryption. For more details, see [**Asymmetric Encryption and Decryption**](https://intl.cloud.tencent.com/document/product/1030/35541).


### Sensitive data

Sensitive data refers to sensitive and private user information such as keys, certificates, bank accounts and ID numbers.

### HSM

Hardware Security Module (HSM) is a computer hardware device that protects and manages keys in the strong authentication system as well as supports cryptographic operations. With the State Cryptography Administration or FIPS-140-2 approved HSM, Tencent Cloud KMS secures keys in terms of confidentiality, integrity and availability. 


### BYOK

Bring Your Own Key (BYOK) refers to the ability of a user to import key material to a Customer Master Key (CMK). For details, see [**Importing External Key**](https://intl.cloud.tencent.com/document/product/1030/32795).




