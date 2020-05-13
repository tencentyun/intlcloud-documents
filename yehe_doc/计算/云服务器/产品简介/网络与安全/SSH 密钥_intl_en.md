To ensure the security and reliability of instances, Tencent Cloud provides two encrypted login methods: [password login](https://intl.cloud.tencent.com/document/product/213/6093) and SSH key pair login. This article describes how to use SSH key pair to login.
You can select SSH key as the CVM encrypted login method using [Custom Configuration for Linux CVM](https://intl.cloud.tencent.com/document/product/213/10517).

## Introduction
Tencent Cloud uses public key encryption to encrypt and decrypt Linux instance login information. Public key encryption uses a public key (think of it as a password) to encrypt data and send the encrypted data to the recipient. The recipient uses a private key to decrypt the data. The combination of a public key and a private key is known as a key pair. Users can use key pairs to connect to CVM instances. It’s a more secure login method than passwords.

Tencent Cloud only stores the public key while the private key is stored by the user. Anybody who has the private key would be able to decrypt your login information. Make sure you keep your private key in a secure location.


## Benefits
Comparing to the traditional authentication method using a user name and password, the SSH key method has the following benefits:
- SSH key authentication is much more secure and prevents brute force attacks.
- SSH key authentication is more convenient. Make a few configurations in the console and your local client, and you will not need to enter a password to login every time.

## Limitations
- Only support Linux instances.
- Tencent Cloud does not retain your private key. You need to click **Download** to obtain the private key within 10 minutes of its creation. Keep it in a secure location because you will not be able to retrieve it from Tencent Cloud again.
- To ensure data security, you need to shut the instance down before the key can be loaded.


## Use Cases


For more information, see [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).
