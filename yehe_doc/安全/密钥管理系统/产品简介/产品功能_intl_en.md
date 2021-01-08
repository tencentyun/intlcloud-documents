### Security and Compliance
KMS leverages a State Cryptography Administration of China or FIPS-140-2 certified hardware security module (HSM) to protect keys, thereby ensuring their confidentiality, integrity, and availability.


### Managed Key Services
KMS provides a wealth of management features, including key creation, enabling, disabling, rotation settings, alias settings, key details viewing, and related information modification, which help you create and protect keys and implement key management policies with ease.

### Encryption Algorithms

KMS supports symmetric encryption algorithms (SM4 and AES256) and asymmetric encryption algorithms (RSA and SM2). You can choose an appropriate algorithm based on your actual business needs.



### Key Import

For symmetric keys, KMS allows you to use your own key material to encrypt and decrypt sensitive data by implementing a Bring Your Own Key (BYOK) solution in Tencent Cloud.




### Key Rotation

For symmetric keys, KMS has a [customer master key (CMK)](https://intl.cloud.tencent.com/document/product/1030/32774) rotation feature which is disabled by default and can be enabled as needed. After this feature is enabled, a CMK will be rotated once every year. Managed by KMS, key rotation is imperceptible to the upper-layer businesses, and existing ciphertexts encrypted by the old CMK can still be decrypted, while only new encryption tasks use the new CMK.

### Permission Control
Fully integrated with CAM, KMS can control which accounts and roles can access or manage your sensitive keys through identity and policy management.

### Built-in Audit
KMS is integrated with CloudAudit to record all API requests for detailed statistics of key management activities and key usage.

### Stability and Reliability
KMS is deployed in a distributed and clustered manner across multiple data centers with hot backup enabled, and its underlying HSM devices are deployed in two data centers with cold backup enabled, guaranteeing high availability around the clock.

### Seamless Integration
Seamlessly integrated with Tencent Cloud services such as COS, TDSQL for MySQL, and CBS, KMS enables you to encrypt data stored in such services with ease.

### Centralized Key Management
KMS can be called and integrated through APIs, SDKs, and Tencent Cloud products and services to achieve centralized management of keys from various applications, no matter whether they are in or off Tencent Cloud.

### Sensitive Data Encryption
Sensitive information encryption is a core capability of KMS, which is mainly used to protect sensitive data (less than 4 KB) on the server disks such as keys, certificates, and configuration files.

### Envelope Encryption
Envelope encryption is a high-performance encryption and decryption solution for massive amounts of data. With the aid of envelope encryption in KMS, only the [data encryption keys (DEKs)](https://intl.cloud.tencent.com/document/product/1030/32774) need to be transferred to the KMS server to be encrypted or decrypted with the CMK, and all business data is processed with efficient local symmetric encryption which has little impact on the business access experience.


