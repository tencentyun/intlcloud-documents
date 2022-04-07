## Overview
rdesktop is an open source client for Remote Desktop Protocol (RDP) that allows a local computer to connect to a Windows CVM. This document describes how to use it to upload files from a local Linux computer to a Tencent Cloud CVM with the Windows Server 2012 R2 operating system.
>? 
>- The Linux computer should be built with a visualized interface to use rdesktop.
>- This document uses a CVM with CentOS 7.6 installed as an example. Note that the steps may vary according to the operating system version.  
>

## Prerequisites
You have purchased a Windows CVM.

## Directions
### Obtaining a public IP
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), navigate to the **Instances** page, and record the public IP of the CVM to which you want to upload files, as shown below:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)

### Installing rdesktop
1. Open a terminal window and run the following command to download rdesktop. This step uses rdesktop v1.8.3 as an example.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
If you want to install the latest version, visit [the rdesktop page on GitHub](https://github.com/rdesktop/rdesktop/releases) to find it. Then replace the path in the command with that of the latest version.
2. Run the following commands to decompress the installation package and enter the directory.
```
tar xvzf rdesktop-1.8.3.tar.gz
```
```
cd rdesktop-1.8.3
```
3. Run the following commands to compile and install rdesktop.
```
./configure 
```
```
make
```
```
make install
```
4. After the installation is complete, run the following command to check if rdesktop is successfully installed:
```
rdesktop
```

### Uploading files
1. Run the following command to specify the shared folder:
```
rdesktop [cvm_public_ip]  -u [cvm_account] -p [cvm_password] -r disk:[shared_folder_name]=[local_folder_path]
```
>?
>- The default account for the Windows CVM is `Administrator`.
>- If you use a system default password to log in to the instance, go to the [Message Center](https://console.cloud.tencent.com/message) to obtain the password first.
>- If you’ve forgotten your password, you can [reset the instance password](http://intl.cloud.tencent.com/document/product/213/16566).
>
For example, run the following command to share the `/home` folder on your local Linux computer with the specified CVM, and rename it as `share`.
```
rdesktop 118.xx.248.xxx  -u Administrator -p 12345678 -r disk:share=/home
```
If the operation is successful, the Windows Desktop appears.
Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> in the lower-left corner and select **My Computer** to see a list of shared folders.
2. Double click a shared folder to open it. Copy desired local files to another drive of the Windows CVM.
For example, copy the file A from the `share` folder to the C drive of Windows CVM.

### Downloading files
To download files from the Windows CVM to your computer, you only need to copy desired files from the CVM to a shared folder.
