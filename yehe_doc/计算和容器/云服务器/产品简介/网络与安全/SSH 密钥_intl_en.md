To ensure the security and reliability of instances, Tencent Cloud provides users with two encrypted login methods, [password](/doc/product/213/6093) and SSH key pair. This document describes how to log in with an SSH key pair.
You can select SSH key pair as the encrypted CVM login method when [Customizing Linux CVM Configurations](/doc/product/213/10517#.E8.AE.BE.E7.BD.AE.E4.BF.A1.E6.81.AF).

## SSH Key Overview
We recommend **using SSH key pair** to log in to a Linux instance. A key pair contains a public key and a private key. It is generated with RSA 2048-bit encryption method.
- **Public key**: When the SSH key pair is generated, Tencent Cloud only stores the public key, and save it in the `~/.ssh/authorized_keys` file.
- **Private key**: You need to download the private key and keep it secretly. The private key can only be downloaded once. Tencent Cloud will not keep your private key. Anyone with your private key can access your instance. Be sure to keep it safe.

You can use the key pair to connect to CVM securely. This method is more secure than logging in with a password. You only need to specify the key pair when creating a Linux instance, or bind key pair to an existing instance, so that you can use the private key to log in to the instance without entering a password.

## Features and Advantages
Compared to traditional password authentication methods, SSH key pair login has the following advantages:
- SSH key pair login is more complex and difficult to brute-force.
- SSH key pair login is easier to use. You can log in to instances remotely with a few simple configuration steps on the console and your local client, and do not need to enter a password when you log in again.

## Use Limits
- SSH key pair login is only available for Linux instances.
- Each Tencent Cloud account can have up to 100 SSH key pairs.
- Tencent Cloud will not retain your private key. You need to download the private key after creating an SSH key, and keep it safe.
- To ensure data security, you need to shut the instance down before loading the key.
- To improve CVM security, you cannot use the password login method after binding a key pair to the instance.


## Use Cases
- To learn how to create, bind, unbind, or delete a key, see [Managing SSH Key Pairs](https://intl.cloud.tencent.com/document/product/213/16691).
- To learn about how to log in to CVM instances remotely using an SSH key pair, see
 - [Logging in to Linux Instances via Remote Login Tools](https://intl.cloud.tencent.com/document/product/213/32502)
 - [Logging in to Linux Instance via SSH Key](https://intl.cloud.tencent.com/document/product/213/32501)



