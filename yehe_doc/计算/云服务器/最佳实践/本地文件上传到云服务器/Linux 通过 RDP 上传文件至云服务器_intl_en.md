## Introduction
rdesktop is an open source RDP client. This article describes how to use it to connect to a CVM running Windows Server 2012 R2 to upload files.

## Prerequisites
Purchased a Windows CVM instance.

## Instructions
### Obtaining CVM Public IP
Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index) and find the public IP address of your Windows CVM, as shown in the following image:
![](https://main.qcloudimg.com/raw/59ce52615c467ad80bc4220425bf2b80.png)



###. Installing rdesktop.
1. Open a terminal window and run the following command to download rdesktop 1.8.3:
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
If you want to install a new version, visit [the rdesktop home on GitHub](https://github.com/rdesktop/rdesktop/releases) to find it. Then replace the path in the command with the new one.
2. Run the following commands to decompress the install package and navigate to its directory.
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
4. After installation finishes, run the following command to check if rdesktop is successfully installed:
```
rdesktop
```

### Uploading Files
1. Run the following command to specify the shared folder:
```
rdesktop cvm_ip  -u cvm_username -p cvm_password -r disk:shared_folder_path=local_folder_path
```
>
>- The default username for the CVM is `Administrator`.
>- If you choose to log in with a random password, please check it in [Message Center](https://console.cloud.tencent.com/message).
>- If you forgot your password, please [reset the instance password](http://intl.cloud.tencent.com/document/product/213/16566).
>
For example, execute the following command to share the `/home` folder on your local Linux machine to the specified CVM, and rename it as `share`.
```
rdesktop 118.xx.248.xxx  -u Administrator -p 12345678 -r disk:share=/home
```
If the operation is successful, the Windows Desktop appears.
Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px"> then **My Computer** to see shared folders.
2. Double click the shared folder to open it. Copy a file in the shared folder to a directory on the Windows CVM disk to upload it.
For example, copy **a.txt** in `share` to the C drive of Windows CVM.

### Downloading files
To download files from a Windows CVM to your Linux computer, copy desired files from the CVM to the shared folder.
