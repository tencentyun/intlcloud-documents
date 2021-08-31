## Overview
The document uses CVMs with CentOS 7.6 as an example to describe how to upload and download files via SCP.


## Prerequisites
You have purchased a Linux CVM.

## Directions
### Obtaining a public IP
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), navigate to the **Instances** page, and record the public IP of the CVM to which you want to upload files, as shown below:
![](https://main.qcloudimg.com/raw/4ffafbd2f6ab65d55e56fe59b669363a.png)


### Uploading files
1. Run the following command to upload files to a Linux CVM.
```
scp [local file address] [CVM account]@[CVM instance public IP/domain name]:[CVM file location]
```
Suppose that you want to upload the local file `/home/lnmp0.4.tar.gz` the CVM (IP: 129.20.0.2) under the same directory, the command should be as follows:
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
2. Enter **yes** and press **Enter** to confirm the upload and enter the login password to complete the upload.
 - If you use a system default password to log in to the instance, go to the [Message Center](https://console.cloud.tencent.com/message) to obtain the password first.
 - If you’ve forgotten your password, you can [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).

### Downloading a file
1. Run the following command to download a file from a Linux CVM.
```
scp CVM account@CVM instance public IP/domain name: CVM file location local file address 
```
For example, you can run the following command to download the file `/home/lnmp0.4.tar.gz` from the CVM whose public IP is `129.20.0.2` to the same local directory:
```
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```


