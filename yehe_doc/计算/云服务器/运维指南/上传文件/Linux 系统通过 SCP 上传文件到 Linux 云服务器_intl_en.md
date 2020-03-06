## Introduction
The document uses CVMs with CentOS 7.6 as an example to describe how to upload and download files via SCP.


## Prerequisites
You have purchased a Linux CVM.

## Directions
### Obtaining a public IP
Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index), navigate to the instance list page, and record the public IP of the CVM to which you want to upload files as shown below:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)


### Uploading a file
1. Execute the following command on a computer with the Linux OS to upload files to the Linux CVM.
```
scp local file address CVM account@CVM instance public IP/domain name: CVM file location
```
For example, if you want to upload the local file `/home/lnmp0.4.tar.gz` to the corresponding directory of the CVM whose public IP is `129.20.0.2`, please execute the following command:
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
2. Enter **yes** and press **Enter** to confirm the upload and enter the login password to complete the upload.
 - If you use a system default password to log in to the instance, you can view the password in the [Message Center](https://console.cloud.tencent.com/message).
 - If you forget your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).

### Downloading a file
1. Execute the following command on a computer with the Linux OS to download files from the Linux CVM.
```
scp CVM account@CVM instance public IP/domain name: CVM file location local file address   
```
For example, if you want to download the file `/home/lnmp0.4.tar.gz` from the CVM whose public IP is `129.20.0.2` to the corresponding local directory, please execute the following command:
```
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```
