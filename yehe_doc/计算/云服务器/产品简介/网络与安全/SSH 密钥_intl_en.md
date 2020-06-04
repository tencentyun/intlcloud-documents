To ensure the security and reliability of instances, Tencent Cloud provides users with two encrypted login methods. Users can login via a [login password](/doc/product/213/6093) or SSH key pair. This document describes logging in with SSH key pair.
You can select SSH key pair as the encrypted CVM login method when [Customizing Linux CVM Configurations](/doc/product/213/10517#.E8.AE.BE.E7.BD.AE.E4.BF.A1.E6.81.AF).

## SSH Key Overview
Tencent Cloud encrypts and decrypts the login to Linux instances with public key cryptography. Specifically, Tencent Cloud encrypts data, such as a password, using a public key, and then users decrypt the data using a private key. The public and private keys are called key pair, with which, users can connect to CVM securely. This method is more secure than logging in with a password.

Tencent Cloud only stores the public key. The private key will be kept by you. The private key can be used to decrypt your login, so be sure to keep it safe.


## Features and Advantages
Compared to traditional password authentication methods, SSH key has the following advantages:
- SSH keys are more complex and difficult to brute-force.
- SSH keys are easier to use. You can log in to instances remotely with a few simple configuration steps on the console and your local client, and do not need to enter a password when you log in again. 

## Use Limits
- This login method is only available for Linux instances.
- Tencent Cloud will not retain your private key. You need to click **Download** to obtain the private key within 10 minutes after creating an SSH key, and keep it safe.
- To ensure data security, you need to shut the instance down before loading the key.


## Use Cases
- To learn how to create, bind, unbind, or delete a key, see [Managing SSH keys](https://intl.cloud.tencent.com/document/product/213/16691).
- To learn how to log in to CVM instances remotely using SSH login, see
 - [Logging into Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Logging into Linux Instances via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)
