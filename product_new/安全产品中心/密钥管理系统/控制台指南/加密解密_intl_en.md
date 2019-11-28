## Operation Scenarios
Tencent Cloud KMS provides APIs, SDKs, and online tools for you to encrypt and decrypt small pieces of data. You can choose any of them based on your needs for different scenarios.


## Online Tools
The online tools are suitable for one-time or non-batch encryption and decryption operations, such as the initial generation of key ciphertext. With the online tools, you can focus on your core business without developing tools for non-batch encryption and decryption. They can be used in the following steps:

## Prerequisites
A key has been [created](https://intl.cloud.tencent.com/document/product/1030/31971) and enabled.

## Directions
1. Log in to the [KMS Console](https://console.cloud.tencent.com/kms2).
2. Find the target key. In the "Key ID/Name" section, click the key name to enter the key details page.
3. In the "Online Tools" module, click **Encryption**.
4. Enter the data to be processed in the input box below.
5. Click **Convert**, and the resulting data processed by the system will be displayed in the gray box on the right.
6. After encryption is completed, you can click **Download** to download the encrypted data to your local file system.
7. If you need to decrypt the data, click **Decryption** in the "Online Tools" module.
8. Paste the encrypted data into the input box below, click **Convert**, and the decrypted data will be displayed in the gray box on the right.
>The decryption operation automatically calls the CMK used in the encryption. After decryption, the plaintext will be Base64-encoded for display.
9. You can click **Download** to download the decrypted data to your local file system.

