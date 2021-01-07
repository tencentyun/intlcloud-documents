## Overview

This document describes how to use a SSH key to log in to a Linux instance from a local Linux, Mac OS or Windows.

## Supported Systems

Linux, Mac OS or Windows (including Windows 10 and Windows Server 2019)

## Authentication Method

**Password** or **Key**

## Prerequisites
- You must already have the admin account and password (or key) to log in to the instance.
 - If you use a system default password to log in to the instance, go to the [Message Center](https://console.cloud.tencent.com/message) to obtain the password first.
 - If you [use a key](#LoginWithKey) to log in, you must have created a key and bound it to this CVM. For more information, see [Managing SSH Keys](https://intl.cloud.tencent.com/document/product/213/16691).
 - If you forgot your password, please [reset your instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- A public IP has been purchased for your CVM instance, and port 22 is open (this is open by default for a CVM purchased with quick configuration).

## Directions

### Using the password

1. Execute the following command to connect to the Linux CVM.
>? If your local computer uses Mac OS, you must open the terminal provided by the system and then execute the following command.
> If your local computer uses Linux, you can directly execute the following command.
> If your local computer uses Windows 10 or Windows Server 2019, you must first open the command prompt CMD and then execute the following command.
>
```
ssh <username>@<hostname or IP address>
```
 - `username` refers to the default account name obtained as a prerequisite.
 - `hostname or IP address` refers to the public IP address or custom domain name of your Linux instance.
2. Enter the password you have already obtained, and press **Enter** to log in.

<span id="LoginWithKey"></span>
### Using a key

1. Execute the following command to set the private key file readable only to you.
 - If your local computer uses Mac OS, you must first open the terminal provided by the system and then execute the following command.
 - If your local computer uses Linux, you can directly execute the following command.
```
chmod 400 <The absolute path of the private key downloaded to be associated with the CVM>
```
 - If your local computer uses Windows 10, you must first open the command prompt CMD and then execute the following commands.
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
 - `username` refers to the default account name obtained as a prerequisite.
 - `hostname or IP address` refers to the public IP address or custom domain name of your Linux instance.

 For example, execute the `ssh -i "Mac/Downloads/shawn_qcloud_stable.pem" ubuntu@192.168.11.123` command to remotely log in to the Linux CVM.

## Subsequent Operations

After logging in to the CVM, you can build a personal website or forum or perform other operations. For more information, please see:
- [Manually Building a WordPress Website](https://intl.cloud.tencent.com/document/product/213/8044)


