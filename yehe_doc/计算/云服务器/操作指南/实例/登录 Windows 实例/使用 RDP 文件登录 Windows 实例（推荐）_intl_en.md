## Scenario

Remote Desktop Protocol (RDP) is a multiple-channel protocol developed by Microsoft, which allows a local computer to connect to a remote computer. We recommend that you use RDP to log in to your Windows CVMs. This topic describes how to log in to Windows instances using RDP files.

## Applicable local OS
You can log in to your CVMs from Windows, Linux, and MacOS using RDP.

## Prerequisites

- You must already have the admin account and password for logging in to Windows instance remotely.
 - If you log in to the instance with a random password, you can get the password through the [Message Center](https://console.cloud.tencent.com/message).
 - If you forget your password, please [reset instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- You have purchased public IPs for your CVM instance and the port 3389 is open.

## Directions

### Logging in to your CVM from Windows using RDP
1. Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, select the target Windows CVM and click **Log In**, as shown below.
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. In the **Log into Windows instance** pop-up window, select **Log in with RDP file** and click **Download RDP file** to download RDP file to your local computer.
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. Double-click the downloaded RDP file, enter the password, and click **OK** to remotely connect to your Windows CVM.
 - If you log in to the instance with a random password, you can get the password through the [Message Center](https://console.cloud.tencent.com/message).
 - If you forget your password, please [reset instance password](https://intl.cloud.tencent.com/document/product/213/16566).

### Logging in to your CVM from Linux using RDP

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
If you want to install a new version, visit [the rdesktop home on GitHub](https://github.com/rdesktop/rdesktop/releases) to find it. Then replace the path in the command with the new one.
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
   If you log in to the instance with a random password, you can get the password through the [Message Center](https://console.cloud.tencent.com/message). If you forget your password, please [reset instance password](https://intl.cloud.tencent.com/document/product/213/16566).
 - `<hostname or IP address>` indicates the public IP address or custom domain name of your Windows instance.
 
### Logging in to your CVM from MacOS using RDP

>
>- The following operations take Microsoft Remote Desktop for Mac as an example. Microsoft ceased providing a link for downloading the Remote Desktop client in 2017. Currently, its subsidiary [HockeyApp][HockeyApp](https://appcenter.ms/apps) is responsible for releasing the beta client.
>- The following operations take a CVM on Windows Server 2012 R2 as an example.
>
1. Download and install Microsoft Remote Desktop for Mac on your local computer.
2. Start MRD and click **Add Desktop**, as shown below:
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. In the **Add Desktop** pop-up window, establish a connection to your Windows CVM by following steps shown in the figure below.
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. In the **PC name** text box, enter the public IP address of your CVM.
    2. Click **Add**.
    3. Leave other options as default and complete the process.
    Your entry is saved, as shown below:
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Double click the new entry. Input your username and password for CVM and click **Continue**.
 - If you log in to the instance with a random password, you can get the password through the [Message Center](https://console.cloud.tencent.com/message).
 - If you forget your password, please [reset instance password](https://intl.cloud.tencent.com/document/product/213/16566).
5. Click **Continue** to establish the connection, as shown below:
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
If the connection is successful, the following page appears:
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
