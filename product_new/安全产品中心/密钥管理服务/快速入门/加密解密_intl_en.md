## Overview
KMS provides encryption and decryption APIs. The encryption API (Encrypt) is used to encrypt any data up to 4 KB in size, such as database passwords, RSA keys, or other sensitive information in small size. The decryption API (Decrypt) is used to decrypt ciphertext. A generated DataKey can obtain the key data in plaintext through the decryption API.


## Online Tools
Online tools are suitable for one-time or non-batch encryption and decryption operations, such as the initial generation of a key ciphertext. With online tools, you do not need to bother with developing tools for small encryption and decryption needs and focus your energies on core business issues. The directions for encrypting small data entries are as follows:

### Prerequisites
[A key has been created](https://intl.cloud.tencent.com/document/product/1030/31971) and enabled.

### Directions
1. Log in to the KMS Console.
2. Find the key you want to encrypt/decrypt. In the "Key ID/Name" section, click the key name to enter the key details page.
3. In the "Online Tools" module, select **Encryption** or **Decryption**.
4. Enter the data to be processed in the input box below.
 ![](https://main.qcloudimg.com/raw/a4b45ce66767029f057796bc06fc03a2.png)
5. Click **Convert** and the resulting data processed by the system will be displayed in the gray box on the right.
![](https://main.qcloudimg.com/raw/db30c2d0ec8226726accb5efe1617525.png)
6. You can download the data to your local file system by clicking **Download**.
