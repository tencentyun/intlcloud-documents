## Overview
The document uses a Lighthouse instance with CentOS 7.6 as an example to describe how to upload and download files via SCP.


<dx-alert infotype="explain" title="">
To get started, ensure that you have configured the Lighthouse instance admin account and password. If you haven't set or forgot the password, please [reset password](https://intl.cloud.tencent.com/document/product/1103/41553).
</dx-alert>


## Directions
### Obtaining a public IP
Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and obtain the public IP of the target Lighthouse instance on **Instances** page.


### Uploading files
1. Run the following commands on the local server, and upload the files to the Linux-based Lighthouse instance.
```shellsession
scp Local file address Lighthouse instance account@Lighthouse instance public IP/domain name:Lighthouse instance file path
```
For example, you can run the following command to upload the local file `/home/lnmp0.4.tar.gz` to the same directory of the Lighthouse instance whose public IP is `129.20.0.2`:
```shellsession
scp /home/Inmp0.4.tar.gz root@129.20.0.2:/home/Inmp0.4.tar.gz
```
2. Enter **yes** and press **Enter** to confirm the upload and enter the login password to complete the upload.


### Downloading files
1. Run the following command on the local server to download a file from a Linux-based Lighthouse instance.
```shellsession
scp Lighthouse instance account@Lighthouse instance public IP/domain name:Lighthouse instance file path Local file address 
```
For example, you can run the following command to download the file `/home/lnmp0.4.tar.gz` from the Lighthouse instance whose public IP is `129.20.0.2` to the same local directory:
```shellsession
scp root@129.20.0.2:/home/Inmp0.4.tar.gz /home/Inmp0.4.tar.gz
```


