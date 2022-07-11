## Overview
The document uses CVMs with CentOS 8.2 as an example to describe how to upload and download files via SCP.


## Prerequisites
You have purchased a Linux CVM.

## Directions
### Obtaining a public IP
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), navigate to the **Instances** page, and record the public IP of the CVM to which you want to upload files, as shown below:
![](https://main.qcloudimg.com/raw/4ffafbd2f6ab65d55e56fe59b669363a.png)


### Uploading files
1. Run the following command to upload files to a Linux CVM.
```
scp local file address CVM account@CVM instance public IP/domain name: CVM file location
```
For example, you can run the following command to upload the local file `/home/lnmp0.4.tar.gz` to the same directory of the CVM whose public IP is `129.20.0.2`:
```
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
<dx-alert infotype="explain" title="">
You can add the `-r` parameter to upload folders. For more information on the `scp` command, run `man scp`.
</dx-alert>
2. Enter yes and press Enter to confirm the upload and enter the login password to complete the upload. 

- If you use a system default password to log in to the instance, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message).
- If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566)

### Downloading files
1. Run the following command to download a file from a Linux CVM.
```
scp CVM account@CVM instance public IP/domain name: CVM file location local file address 
```
For example, you can run the following command to download the file `/home/lnmp0.4.tar.gz` from the CVM whose public IP is `129.20.0.2` to the same local directory:
```
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```

