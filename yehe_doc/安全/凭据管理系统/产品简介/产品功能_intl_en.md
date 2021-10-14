To avoid risks posed by sensitive configuration and hardcoded sensitive secrets, all secrets are encrypted and protected by KMS. Also, easy-to-use APIs and SDK are provided to reduce service and management costs. Users can use SSM to centrally retrieve, manage, and store encrypted database credentials, API keys, and other keys as well as sensitive configuration, avoiding plaintext leakage caused by hardcoding and business risks caused by out-of-control permissions.
## Secure Secret Retrieval
With SSM, hardcoded secrets are deleted from the application source code and replaced by calls to Secrets Manager API, so you can dynamically retrieve and manage secrets programmatically.

## Encrypted Secret Storage and Transfer
SSM allows encrypted storage of your secrets using a [Key Management Service (KMS)](https://intl.cloud.tencent.com/product/kms)-protected Customer Master Key (CMK) as encryption key, and transmit them to your local server securely over [TLS](https://intl.cloud.tencent.com/document/product/1078/38618).

## Application-layer Secret Rotation
SSM helps you rotate and manage your secrets. It can routinely update sensitive secrets and automatically sync the update across all applications, ensuring that your applications are using the latest version of your secrets and guaranteeing business continuity.

## Multi-Type Secret Storage
Multiple types of data can be stored in the format of Name-Value pairs. "Value" can be up to 4096 bytes, storing data such as database credentials, account passwords, and IP ports.

## Resource-level Access Authorization
Integrating with Tencent Cloud [Cloud Access Management](https://intl.cloud.tencent.com/product/cam) (CAM), SSM allows only granted users to access and modify secrets via identity management and policy management, and to specify users or roles who can access these secrets by associating with these policies.

## Refined Regulation and Audit
SSM combines with [CloudAudit](https://intl.cloud.tencent.com/product/cloudaudit) to perform supervision, compliance checks, operational reviews, and risk reviews on your Tencent Cloud accounts. All management operations and usage of the secrets can be recorded.

## High-availability Disaster Recovery and Backup
SSM utilizes cluster deployment and a distributed database storage system for data storage and disaster recovery. You can create the same secrets in multiple regions to implement cross-region disaster recovery for secrets.

## Security Compliance
SSM is linked to KMS. SSM uses a hardware security module (HSM) certified by third parties at its underlying layer to generate and protect secrets, meeting the supervision and compliance requirements.

## Automatic Rotation
There are security challenges your account may face, such as improper use of management permission, your password unchanged for a long time, and key information in plaintext, leading to a loss of digital assets.

Given these risks, database credentials will be periodically rotated to create strong passwords and manage sensitive configuration information, securing your data while reducing security risks and threats to your account.
