## Secrets Manager Overview
Secrets Manager (SSM) is a management service that enables you to create, retrieve, update, and delete secrets through their lifecycle. You can use SSM together with resource-level role authorization and comprehensive audit control to centrally manage sensitive secrets easily. Users and applications can call SSM APIs to avoid risks of sensitive configuration and sensitive secret hardcoding, and avoid sensitive information leakage as well as business risks caused by out-of-control permissions.

## Strengths
### Enterprise-level Secret management
SSM facilitates the management of sensitive secrets, avoiding plaintext leakage caused by hardcoding and business risks caused by out-of-control permissions.
### Full lifecycle management
You can use SSM to easily manage secrets through their lifecycle, such as creating, retrieving, updating, deleting, and managing permissions for secrets. You can use SSM together with resource-level role authorization and comprehensive audit control to centrally manage sensitive secrets easily.
### Security and reliability
SSM adopts the clustered deployment mode. It uses the distributed database storage system to implement data storage, DR, and backup. With SSM, business users can create the same secrets in different regions to achieve cross-region DR.
### Encrypted storage
Secrets are encrypted and stored by Tencent Cloud Key Management Service (KMS). Encryption keys are generated and protected by a hardware security module (HSM) certified by third parties. During secret retrieval, secrets are securely transferred by TLS to the local server.
### Pay-as-you-go
SSM offers pay-as-you-go pricing. You are billed based on the number of managed secrets and API calls in SSM. No minimum fee or setting fee is required. For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/1078/38596).
