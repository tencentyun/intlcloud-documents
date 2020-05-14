To ensure the security and reliability of instances, Tencent Cloud allows users to log in to instances with either [Login Password](/doc/product/213/6093) or SSH key pair. This document describes login with SSH key pair.
You may choose the SSH key pair as an encrypted CVM login method when [Customizing Linux CVM Configurations](/doc/product/213/10517#.E8.AE.BE.E7.BD.AE.E4.BF.A1.E6.81.AF).

## SSH Key Overview
Tencent Cloud encrypts and decrypts the login to Linux instances with public key cryptography. Specifically, Tencent Cloud encrypts data, such as a password, using a public key, and then users decrypt the data using a private key. The public and private keys are called key pair, with which, users can connect to CVM securely. This method is more secure than login with password.

Tencent Cloud only stores the public key, and you need to retain the private key. Anyone who has your private key can decrypt your login, so be sure to properly keep the private key.


## Features and Advantages
Compare to traditional verification methods involving user name and password, SSH key has the following advantages:
- Login verification with SSH key offers a higher security to prevent brute force attacks.
- Login with SSH key is easier to use through simple configurations on the console and local client, so you can log in to instances remotely without entering the password again in case of re-login.

## Use Limits
- This login method is only available to Linux instances.
- Tencent Cloud will not retain your private key. You need to click **Download** to obtain the private key within 10 minutes after creating an SSH key, and keep it properly.
- To ensure data security, you need to shut the instance down before loading the key.


## Use Cases
- How to create, bind, unbind, or delete a key, see [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).
- How to log in to CVM instances remotely using SSH login, see
 - [Logging into Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Logging into Linux Instances via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
