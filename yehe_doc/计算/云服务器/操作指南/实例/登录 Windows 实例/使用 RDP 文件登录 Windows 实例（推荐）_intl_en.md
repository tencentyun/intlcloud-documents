## Scenario

Remote Desktop Protocol (RDP) is a multi-channel protocol developed by Microsoft, which allows a local computer to connect to a remote computer. Tencent Cloud recommends that you use RDP to log in to your Windows CVMs. This document describes how to log in to Windows instances by using RDP files.

## Applicable Local Operating Systems
You can log in to your CVMs by using RDP on Windows, Linux, and MacOS.

## Prerequisites

- You already have the admin account and password for logging in to the Windows instance remotely.
 - If you use a system default password to log in to the instance, go to [Message Center](https://console.cloud.tencent.com/message) to obtain the password.
 - If you forget your password, [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- A public IP has been purchased for your CVM instance, and port 3389 is open (if the CVM is purchased with “Quick Configuration”, this port is open by default.)

## Directions

### Logging in to your CVM on Windows by using RDP
1. Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, select the Windows CVM that you want to log in to and click **Log In**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. In the **Log in to Windows instance** window that appears, select **Log in with RDP file** and click **Download RDP file** to download the RDP file to your local computer.
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. Double-click the downloaded RDP file to remotely connect to your Windows CVM.
 - If you use a system default password to log in to the instance, go to [Internal Messages](https://console.cloud.tencent.com/message) to obtain the password.
 - If you forget your password, [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).

### Logging in to your CVM on Linux by using RDP

> We recommend that you use rdesktop as the remote desktop client. For more information, see the [official introduction to rdesktop](http://www.rdesktop.org/).
>
1. Run the following command to check whether rdesktop has been installed.
```
rdesktop
```
 - If yes, perform [Step 4](#step04).
 - If no, you will be prompted with "command not found". In this case, perform [Step 2](#step02).
2. <span id="step02"></span>Open a terminal window and run the following command to download rdesktop, for example, rdesktop v1.8.3.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
To install the latest version, visit the [rdesktop homepage on GitHub](https://github.com/rdesktop/rdesktop/releases) to find the installation package for the latest version. Then, replace the path in the command with that of the latest version.
3. In the directory where rdesktop will be installed, run the following commands to decompress and install rdesktop.
```
tar xvzf rdesktop-<x.x.x>.tar.gz ## Replace x.x.x with the version number of the downloaded rdesktop. 
cd rdesktop-1.8.3
./configure 
make 
make install
```
4. <span id="step04">Run the following command to connect to the remote Windows instance.</span>
> Replace the values of the parameters in the example with your actual values.
>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` indicates the admin account mentioned in the prerequisites.
 - `<your-password>` indicates the login password that you set.
   To use a system default password to log in to the instance, go to [Message Center](https://console.cloud.tencent.com/message) to obtain the password. If you forget your password, [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
 - `<hostname or IP address>` indicates the public IP address or custom domain name of your Windows instance.
 
### Logging in to your CVM on MacOS by using RDP

>
>- The following operations use Microsoft Remote Desktop for Mac as an example. Microsoft ceased providing a link for downloading the Remote Desktop client in 2017. Currently, its subsidiary [HockeyApp](https://appcenter.ms/apps) is responsible for releasing the beta client.
>- The following operations use a CVM on Windows Server 2012 R2 as an example.
>
1. Download and install Microsoft Remote Desktop for Mac on your local computer.
2. Start MRD and click **Add Desktop**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. The **Add Desktop** window appears. Complete the steps in the following figure to establish a connection to your Windows CVM.
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. In the **PC name** text box, enter the public IP address of your CVM.
    2. Click **Add** to confirm creation.
    3. Leave default settings for other parameters, and finish the connection establishment.
    Your entry is saved, as shown in the following image:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Double-click the new entry. Enter your username and password for CVM and click **Continue**.
 - If you use a system default password to log in to the instance, go to [Internal Messages](https://console.cloud.tencent.com/message) to obtain the password.
 - If you forget your password, [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
5. Click **Continue** to establish the connection, as shown in the following figure.
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
If the connection is successful, then the following page appears:
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
