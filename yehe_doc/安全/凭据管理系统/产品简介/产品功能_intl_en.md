To avoid risks posed by sensitive configuration and hardcoded sensitive secrets, all secrets are encrypted and protected by KMS. Also, easy-to-use APIs and SDK are provided to reduce service and management costs. Users can use SSM to centrally retrieve, manage, and store encrypted database credentials, API keys, and other keys as well as sensitive configuration, avoiding plaintext leakage caused by hardcoding and business risks caused by out-of-control permissions.
## Secure and Controllable Secret Retrieval
Hardcoded secrets are deleted from the application source code and replaced by SSM API calls to facilitate dynamic retrieval and secret management.

## Encrypted Storage and Transmission of Secrets
SSM uses KMS-protected CMKs as the encryption keys. Content of the managed secrets is encrypted and stored. When a secret is needed, it is transferred to the local server over TLS.

## Secret Rotation at Application Layer
With SSM, you can update the content of sensitive secrets periodically. The updates will be automatically synced to all application points that depend on the secrets, achieving secure secret rotation management and ensuring the continuity of businesses that depend on the secrets.

## Multi-Type Secret Storage
Multiple types of data can be stored in the format of Name-Value pairs. "Value" can be up to 4096 bytes, storing data such as database credentials, account passwords, and IP ports.

## Resource-level Access Authorization
SSM integrates with Tencent Cloud CAM. CAM role management and policy management can ensure that only authorized users can access or edit secrets. You can specify what secrets a user or role can access by adding policies to the user or role.

## Comprehensive Audit Control
SSM combines with Tencent CloudAudit, enabling you to perform supervision, compliance check, operational reviews, and risk reviews on your Tencent Cloud accounts. Besides, operations and usage of your secrets can be recorded.

## High Availability DR and Backup
SSM adopts the clustered deployment mode. It uses the distributed database storage system to implement the persistence of data storage, DR, and backup. With SSM, business users can achieve cross-region DR.

## Security and Compliance
SSM is linked to KMS. SSM uses a hardware security module (HSM) certified by third parties at its underlying layer to generate and protect secrets, meeting the supervision and compliance requirements.
