### Is there a limit to the number of customer master keys that can be created in KMS?
Yes. You can create up to 200 master keys (excluding Tencent Cloud managed CMKs).

### Which Tencent Cloud services can encrypt data using KMS? 
KMS is seamlessly integrated with Tencent Cloud services such as TencentDB, COS, and CBS to encrypt their data through envelope encryption.

### How do I encrypt data using KMS? 
There are three ways to call KMS:
- Call KMS through KMS API. In this case, your business applications can be either in or outside Tencent Cloud.
- Call KMS by integrating the KMS SDK into your own business application. In this case, your business applications can be either in or outside Tencent Cloud.
- Call KMS through a Tencent Cloud product that has been connected to KMS to encrypt and decrypt the data of the product.

### How do I enable key rotation? 
- You can enable key rotation in KMS console to automatically rotate CMK annually. 
- After CMK rotation, you do not need to encrypt the data again, as Tencent Cloud will automatically retain the original CMK. Ciphertext encrypted with the old CMK can still be decrypted, while new data will be encrypted using the new CMK. 

### Is the quantum key service still available?
KMS no longer offer quantum key management services. However, current quantum key users can continue to use them in the [KMS Console](https://console.cloud.tencent.com/kms).

