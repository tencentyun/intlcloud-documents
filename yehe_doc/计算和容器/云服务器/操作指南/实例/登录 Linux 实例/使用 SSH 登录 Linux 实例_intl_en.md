## Overview

This document describes how to use an SSH key to log in to a Linux instance from a local Linux, Mac OS or Windows server.

## Supported Systems

Linux, Mac OS or Windows (including Windows 10 and Windows Server 2019)

## Authentication Method

**Password** or **Key**

## Prerequisites
- You already have the admin account and password (or key) to log in to the instance.
 - The default admin account is usually `root` for the Linux instance, and is `ubuntu` for the Ubuntu system. You can modify it according to the actual situation.
 - If you use a system default password to log in to the instance, go to the [Message Center](https://console.cloud.tencent.com/message) to obtain the password first.
 - If you [use a key](#LoginWithKey) to log in, you must have created a key and bound it to this CVM. For more information, see [Managing SSH Keys](https://intl.cloud.tencent.com/document/product/213/16691).
 - If you forgot your password, please [reset your instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- A public IP has been purchased for your CVM instance, and the port 22 is open. It is open by default for a CVM instance purchased with quick configuration.

## Directions
<dx-tabs>
::: Using the password [](id:passwordLogin)

1. Execute the following command to connect to the Linux CVM.
<dx-alert infotype="explain" title="">
- If your local computer uses Mac OS, you need to open the terminal that comes with the system before executing the following command.
- If your local computer uses Linux, you can directly execute the following command.
- If your local computer uses Windows 10 or Windows Server 2019, you need to open the command prompt CMD before executing the following command.
</dx-alert>
```
ssh <username>@<hostname or IP address>
```
 - `username` refers to the default account as mentioned in “Prerequisites”.
 - `hostname or IP address` refers to the public IP address or custom domain name of your Linux instance.
2. Enter the password you have obtained, and click **Enter** to log in.

:::
::: Using a key [](id:LoginWithKey)

1. Execute the following command to set the private key file readable only to you.
 - If your local computer uses Mac OS, you need to open the terminal that comes with the system before executing the following command.
 - If your local computer uses Linux, you can directly execute the following command.
```
chmod 400 <The absolute path of the private key downloaded to be associated with the CVM>
```
 - If your local computer uses Windows 10, you need to open the command prompt CMD before executing the following commands in sequence.
```
icacls <The absolute path of the private key downloaded to be associated with the CVM> /grant <Windows user account>:F
```
```
icacls <The absolute path of the private key downloaded to be associated with the CVM> /inheritancelevel:r
```
2. Execute the following command for remote login.
```
ssh -i <The absolute path of the private key downloaded to be associated with the CVM> <username>@<hostname or IP address>
```
 - `username` refers to the default account as mentioned in “Prerequisites”.
 - `hostname or IP address` refers to the public IP address or custom domain name of your Linux instance.

 For example, execute the `ssh -i "Mac/Downloads/shawn_qcloud_stable.pem" ubuntu@192.168.11.123` command to remotely log in to the Linux CVM.
:::
</dx-tabs>

## Subsequent Operations

After logging in to the CVM, you can build a personal website or forum or perform other operations. For more information, please see:
- [Manually Building WordPress Website](https://intl.cloud.tencent.com/document/product/213/8044)
- [Manually Building Discuz! Forum](https://intl.cloud.tencent.com/document/product/213/8043)

