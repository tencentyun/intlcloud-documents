## Security and Compliance
KMS leverages a FIPS-140-2 certified hardware security module (HSM) to generate and protect keys, thereby ensuring their confidentiality, integrity and availability.

## Managed Key Services
KMS offers a rich set of management features, including key creation, enabling, disabling, rotation settings, alias settings, key details display, and related information modification, letting you create and protect keys and implement key management policies with ease.

## Key Rotation
KMS features a customer master key (CMK) rotation capability which is disabled by default and can be enabled as needed. If enabled, a CMK will be rotated once per year. Managed by the KMS system, key rotation is imperceptible to users. Existing ciphertexts encrypted by the CMK can still be decrypted, only new encryption tasks use the new CMK.

## Permission Control
Fully integrated with CAM, KMS can control which accounts and roles can access or manage your sensitive keys through identity and policy management.

## Built-in Audit
KMS is integrated with Tencent Cloud Audit to record all API requests for detailed logs of key management activities and key usage.

## Stability and Reliability
KMS is deployed in a distributed, clustered manner across multiple data centers with hot backup enabled, and its underlying HSM devices are deployed in two data centers with cold backup enabled, guaranteeing high availability around the clock.

## Seamless Integration
Seamlessly integrated with Tencent Cloud services such as COS, TencentDB for TDSQL, and CBS, KMS enables you to encrypt data stored in such services with ease.

## Centralized Key Management
KMS can be called and integrated through APIs, SDKs, and Tencent Cloud products and services to achieve centralized management of keys from various applications, no matter whether they are in or outside the Tencent Cloud.

## Sensitive Data Encryption
Sensitive information encryption is a core capability of KMS, mainly used to protect sensitive data (less than 4 KB) on the server disks such as keys, certificates and configuration files.

## Envelope Encryption
Envelope encryption is a high-performance encryption and decryption solution for massive amounts of data. With the aid of envelope encryption in KMS, only the data encryption keys (DEKs) need to be transferred to the KMS server (which are encrypted and decrypted with the CMK), and all data is processed with efficient local symmetric encryption which has little impact on user access.
