## Overview

This document describes how to use the FTP service to upload files from a local Linux computer to a CVM.

## Prerequisites

You have built the FTP service on CVM.
- To use FTP to upload files to a Linux CVM, see [Building the FTP Service (Linux)](https://intl.cloud.tencent.com/document/product/213/10912)
- To use FTP to upload files to a Windows CVM, see [Building the FTP Service (Windows)](https://intl.cloud.tencent.com/document/product/213/10414)

## Directions

### Connecting to the CVM
1. Run the following command to install the FTP service.
> If the FTP service has already been installed on the local Linux computer, skip this step.
>
```
yum -y install ftp
```
2. Run the following command to connect to the CVM and enter the FTP service username and password as prompted.
```
ftp <CVM IP address>
```
If the following interface appears, the connection has been established successfully.
![](https://main.qcloudimg.com/raw/9d93f45167addf70e023a21543af59f8.png)

### Uploading a file
Run the following command to upload a local file to the CVM.
```
put local-file [remote-file]
```
For example, to upload the local `/home/1.txt` file to the CVM, run the following command.
```
put /home/1.txt 1.txt
```

### Downloading a file
Run the following command to download a file from the CVM to a local directory.
```
get [remote-file] [local-file]
```
For example, to download the `A.txt` file from the CVM to the local `/home` directory, run the following command.
```
get A.txt /home/A.txt
```

