

### Encryption Context

Encryption context is a piece of data in JSON format. If you input this data when calling the `Encrypt` API, you must provide the same JSON data during decryption; otherwise, the decryption may fail. You can regularly update the encryption context to improve business security or quickly block unauthorized access without disabling CMK.



### KMS

For more information, please see [Key Management Service](https://intl.cloud.tencent.com/document/product/1030/31984#1196).



### Key Management Service

Tencent Cloud Key Management Service (KMS) is a security management solution that enables you to easily create and manage keys and protect their confidentiality, integrity, and availability, helping meet your key management and compliance needs in multi-application and multi-business scenarios.



### Data Encryption Key

Data encryption keys (DEKs) are protected by CMK and used to encrypt business data. They can be customized or created through KMS APIs.



### Envelope Encryption

Envelope encryption is a high-performance encryption and decryption solution for massive amounts of data. It uses DEKs to encrypt and decrypt business data by means of high-performance symmetric encryption and ensures the secure use of the DEKs through KMS. It can ensure data security while providing high data read/write performance.



### Customer Master Key

Customer master keys (CMKs) are kept by Tencent Cloud. They are protected by a third-party certified hardware security module (HSM) and used to encrypt and decrypt sensitive data used in your business such as passwords, certificates, and DEKs. They can be created and managed in the console or through APIs.
CMKs include customer managed CMKs and Tencent Cloud managed CMKs.

### Tencent Cloud Managed CMK

Tencent Cloud managed CMKs are automatically created for you when a Tencent Cloud service (such as COS or TDSQL) calls the KMS service.
You can query and rotate Tencent Cloud managed CMKs but cannot disable or delete them.