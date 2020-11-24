## Overview

Remote Desktop Protocol (RDP) is a multiple-channel protocol developed by Microsoft that allows a local computer to connect to a remote computer. We recommend you use RDP to log in to your Windows CVMs. This document describes how to log in to Windows instances using RDP files.

## Supported Systems
You can log in to your CVMs from Windows, Linux, and MacOS using RDP.

## Prerequisites

- You must have the admin account and password for logging in to a Windows instance remotely.
 - If you use a system default password to log in to the instance, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message).
 - If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- You have purchased public IPs for your CVM instance and port 3389 is open. (this port is open by default for a CVM purchased with quick configuration).

## Directions

### Logging in to your CVM on Windows using RDP
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, locate the Windows CVM you want to log in to and click **Log In** as shown below.
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. In the **Log into Windows instance** pop-up window, select **Log in with RDP file** and click **Download RDP file** to download the RDP file to your local computer.
>?If you have changed the remote login port, append the IP address with `:port` in the RDP file.
>
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. Double-click the downloaded RDP file, enter the password, and click **OK** to remotely connect to your Windows CVM.
 - If you use a system default password to log in to the instance, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message).
 - If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).

### Logging in to your CVM on Linux using RDP

>? We recommend you use rdesktop as the remote desktop client. For more information, see the [official introduction to rdesktop](http://www.rdesktop.org/).
>
1. Run the following command to check whether rdesktop has been installed.
```
rdesktop
```
 - If yes, perform [step 4](#step04).
 - If no, you will be prompted with "command not found". In this case, perform [step 2](#step02).
2. <span id="step02"></span>Open a terminal window and run the following command to download rdesktop. This step uses rdesktop v1.8.3 as an example.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
If you want to install the latest version, visit [the rdesktop page on GitHub](https://github.com/rdesktop/rdesktop/releases) to find it. Then replace the path in the command with that of the latest version.
3. In the directory where rdesktop will be installed, run the following commands to decompress and install rdesktop.
```
tar xvzf rdesktop-<x.x.x>.tar.gz ## Replace x.x.x with the version number of the downloaded rdesktop. 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">Run the following command to connect to the remote Windows instance.</span>
>? Replace the parameters in the example with your own parameters.
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` refers to the admin account mentioned in the prerequisites section.
 - `<your-password>` refers to the login password that you set.
   If you use a system default password to log in to the instance, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message). If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
 - `<hostname or IP address>` refers to the public IP address or custom domain name of your Windows instance.
 
### Logging in to your CVM on MacOS using RDP

>?
>- The following operations use Microsoft Remote Desktop for Mac as an example. Microsoft stopped providing a link to download the Remote Desktop client in 2017. Currently, its subsidiary HockeyApp is responsible for releasing the beta client.Go to [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) to download a Beta version.
>- The following operations use a CVM on Windows Server 2012 R2 as an example.
>
1. Download and install Microsoft Remote Desktop for Mac on your local computer.
2. Start MRD and click **Add Desktop**, as shown below:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. In the **Add Desktop** pop-up window, follow the steps illustrated in the following image to establish a connection to your Windows CVM.
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. In the **PC name** text field, enter the public IP address of your CVM.
    2. Click **Add**.
    3. Retain the default settings for the other options and establish the connection.
    Your entry has now been saved, as shown below:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Double-click the new entry. Input your username and password for CVM and click **Continue**.
 - If you use a system default password to log in to the instance, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message).
 - If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
5. In the pop-up window, click **Continue** to establish the connection, as shown below:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
If the connection is successful, the following page will appear:
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
