## Operation Scenarios

To improve the security of ciphertext storage, Tencent Cloud KMS provides the capability of imperceptible key rotation to refresh the stored ciphertext.
Key rotation is imperceptible and has no impact on your business. After being rotated, the CMK is compatible with the ciphertext encrypted before rotation. The [ReEncrypt ](https://cloud.tencent.com/document/product/573/34414) API is offered to refresh the ciphertext. This document describes how to enable key rotation in the console.





## Directions

1. Log in to the [KMS Console](https://console.cloud.tencent.com/kms2).
2. Locate the key to be rotated and click **Enable Rotation** in the "Key Rotation" column.
>By default, key rotation is disabled. Once it is enabled, the CMK will be rotated annually.
>
![](https://main.qcloudimg.com/raw/8a5cb74ec67cf6fca540c86a3e62300c.jpg)
