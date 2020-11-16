To avoid risks posed by sensitive configuration and hardcoded sensitive secrets, all secrets are encrypted and protected by KMS. Also, easy-to-use APIs and SDK are provided to reduce service and management costs. Users can use SSM to centrally retrieve, manage, and store encrypted database credentials, API keys, and other keys as well as sensitive configuration, avoiding plaintext leakage caused by hardcoding and business risks caused by out-of-control permissions.
## Secure Secret Retrieval
With SSM, hardcoded secrets are deleted from the application source code and replaced by calls to Secrets Manager API, so you can dynamically retrieve and manage secrets programmatically.

## Encrypted Secret Storage and Transfer
Secrets are encrypted and stored in SSM using our Key Management Service (KMS), and the encryption key is generated and protected by the hardware security module (HSM) authenticated by a third party. When a secret is retrieved from SSM, it will be securely transferred to the local server over TLS.

## Application-layer Secret Rotation
SSM helps you rotate and manage your secrets. It can routinely update sensitive secrets and automatically sync the update across all applications, ensuring that your applications are using the latest version of your secrets and guaranteeing business continuity.

## Multi-Type Secret Storage
Multiple types of data can be stored in the format of Name-Value pairs. "Value" can be up to 4096 bytes, storing data such as database credentials, account passwords, and IP ports.

## Resource-level Access Authorization
SSM is fully integrated with Cloud Access Management (CAM), so you can use the granular identity and access policies to ensure that only authorized users can access or modify secrets. In addition, you can bind policies to users or roles to specify the secrets that can be accessed by them.

## Refined Regulation and Audit
SSM is integrated with CloudAudit and provides monitoring, compliance check, and auditing services for your Tencent Cloud account. It can record all secret management operations and usage.

## High-availability Disaster Recovery and Backup
SSM utilizes cluster deployment and a distributed database storage system for data storage and disaster recovery. You can create the same secrets in multiple regions to implement cross-region disaster recovery for secrets. 

## Security Compliance
SSM is linked to KMS. SSM uses a hardware security module (HSM) certified by third parties at its underlying layer to generate and protect secrets, meeting the supervision and compliance requirements.
