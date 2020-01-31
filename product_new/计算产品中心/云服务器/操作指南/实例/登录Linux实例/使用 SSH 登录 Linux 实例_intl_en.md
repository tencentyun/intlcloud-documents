## Scenario

This document describes how to use SSH key to log into a Linux instance in a local computer using Linux or MacOS.

## Applicable local OS

Linux or Mac OS

## Authentication Method

**Password** or **SSH Key**

## Prerequisites
- You must already have the admin account and password (or key) for logging into the instance.
 - If you use a system default password to log in to the instance, obtain it by visiting [Internal Message](https://console.cloud.tencent.com/message).
 - If you [log in to the instance with a key](#LoginWithKe), you must have created a key and bound it to this CVM. For more information, see [SSH Keys](http://intl.cloud.tencent.com/document/product/213/16691).
 - If you forget your password, [reset the instance password](http://intl.cloud.tencent.com/document/product/213/16566).
- A public IP has been purchased for your CVM instance, and port 22 is open (this is open by default for CVMs purchased with quick configuration).

## Steps

### Logging in with a password

1. Execute the following command to connect to the Linux CVM.
> If your local computer uses Mac OS, you must open the terminal provided by the system and then execute the following command.
> If your local computer uses Linux, you can directly execute the following command.
>
```
ssh <username>@<hostname or IP address>
```
 - `username` is the default account name obtained as a prerequisite.
 - `hostname or IP address` is the public IP address or custom domain name of your Linux instance.
2. Enter the password you have already obtained, and press **Enter** to log in.

<span id="LoginWithKey"></span>
### Logging in with a key

1. Execute the following command to set the private key file readable only to you.
> If your local computer uses Mac OS, you must open the terminal provided by the system and then execute the following command.
> If your local computer uses Linux, you can directly execute the following command.
>
```
chmod 400 <The absolute path of the private key downloaded to be associated with the CVM>
```
2. Execute the following command for remote login.
```
ssh -i <The absolute path of the private key downloaded to be associated with the CVM> <username>@<hostname or IP address>
```
 - `username` is the default account name obtained as a prerequisite.
 - `hostname or IP address` is the public IP address or custom domain name of your Linux instance.

 For example, execute the `ssh -i "Mac/Downloads/shawn_qcloud_stable" ubuntu@192.168.11.123` command to remotely log into the Linux CVM.

## Subsequent Operations

After logging into the CVM, you can build a personal website or forum on Tencent Cloud CVM or perform other operations. For more information, see the following:
- [Building a personal WordPress website]
- [Building a Discuz! forum]


