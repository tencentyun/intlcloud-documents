## Scenario

Remote Desktop Protocol (RDP) is a multiple-channel protocol developed by Microsoft, which allows a local computer to connect to a remote computer. Tencent Cloud recommends that you use RDP to log in to your Windows CVMs. This document describes how to log in to Windows instances with RDP files.

## Applicable Local Operating Systems
You can log in to your CVMs by using RDP on Windows, Linux, and MacOS.

## Prerequisites

- You already have the admin account and password for logging into Windows instances remotely.
 - If you want to use a system default password to log in to the instance, you can view the password in [Internal Messages](https://console.cloud.tencent.com/message).
 - If you forget your password, [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- A public IP address has been purchased for your CVM instance, and port 3389 is open (if the CVM is purchased with "Quick Configuration", this port is open by default.)

## Procedure

### RDP login on Windows
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance’s management page, select the Windows CVM that you want to log in to and click **Log In**, as shown below:
![](https://main.qcloudimg.com/raw/02780bea40867bc32024d6edc1ed1949.png)
3. In the **Log into Windows instance** window that appears, select **Log in with RDP file** and click **Download RDP file** to download the RDP file to your local computer.
![](https://main.qcloudimg.com/raw/84dc8461976327135b3caab36dc04758.png)
4. Double click the downloaded RDP file to remotely connect to your Windows CVM.
 - If you want to use a system default password to log in to the instance, you can view the password in [Internal Messages](https://console.cloud.tencent.com/message).
 - If you forget your password, [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).

### RDP login on Linux

>We recommend that you use rdesktop as the remote desktop client. For more information, see the [official introduction to rdesktop](http://www.rdesktop.org/).
>
1. Run the following command to check if rdesktop has been installed.
```
rdesktop
```
 - If yes, perform [Step 4](#step04).
 - If no, you will be prompted with "command not found". In this case, perform [Step 2](#step02).
2. <span id="step02"></span>Open a terminal window and run the following command to download rdesktop v1.8.3.
```
wget https://github.com/rdesktop/rdesktop/releases/download/v1.8.3/rdesktop-1.8.3.tar.gz
```
To install the latest version of rdesktop, go to [the rdesktop page on GitHub](https://github.com/rdesktop/rdesktop/releases) to find it. Then, replace the installation path in the command with the new one.
3. In the directory where rdesktop will be installed, run the following commands to decompress and install rdesktop.
```
tar xvzf rdesktop-<x.x.x>.tar.gz ## Replace x.x.x with the version number of the downloaded version. 
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
   If you want to use a system default password to log in to the instance, you can obtain it in [Internal Messages](https://console.cloud.tencent.com/message). If you forget your password, [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
 - `<hostname or IP address>` indicates the public IP address or custom domain name of your Windows instance.
 
### RDP login on MacOS

>
>- The following operations use Microsoft Remote Desktop for Mac as an example. Microsoft ceased providing a download link for the Remote Desktop client in 2017. Currently, its subsidiary HockeyApp is responsible for releasing the beta client.
>- The following operations use a CVM with Windows Server 2012 as an example.
>
1. Download and locally install [Microsoft Remote Desktop for Mac](https://www.techspot.com/downloads/4698-microsoft-remote-desktop-for-mac.html).
2. Start MRD and click **Add Desktop**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. The **Add PC** window appears. Follow the steps illustrated in the following figure to establish a connection to your Windows CVM.
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. In the **PC name** text box, enter your CVM’s public IP address.
    2. Click **Add** to confirm the creation.
    3. Use the defaults for other options and finish the process.
    Now, your connection has been established, as shown in the following figure:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Double click the newly added connection. Enter your username and password for the CVM and click **Continue**.
 - If you want to use a system default password to log in to the instance, you can view the password in [Internal Messages](https://console.cloud.tencent.com/message).
 - If you forget your password, [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
5. Click **Continue** to establish the connection, as shown in the following figure:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
If the connection is successful, the following page appears:
![](https://main.qcloudimg.com/raw/901749cdab5e347ba1989c28f00b7691.png)
