## Overview
This document describes how to log in to a Windows instance through remote desktop software on local Windows, Linux, and macOS computers.

## Supported Operating Systems
Windows, Linux, and macOS.

## Prerequisites

- You must have the admin account (Administrator) and password for logging in to a Windows instance remotely.
	- If you set a login password when creating an instance, use it for login. If you forgot it, you can [reset it](https://intl.cloud.tencent.com/document/product/1103/41553).
	- If you choose to generate a random password when creating an instance, you can get it from [Message Center](https://console.cloud.tencent.com/message).
- Make sure the network connection between the local computer and the instance is working, and the port 3389 is open in the firewall policies of the instance (Port 3389 is open by default upon the creation of instance).

## Directions
Select one of the following remote desktop applications to log in to your Windows instance based on your local operating system.

<dx-tabs>
::: Windows

<dx-alert infotype="explain" title="">
The following takes Windows 7 as an example.
</dx-alert>


1. On the local Window server, click <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 35px;">, enter **mstsc** in **Search programs and files**, and press **Enter** to open the **Remote Desktop Connection** window.
![](https://qcloudimg.tencent-cloud.cn/raw/942c8d417f971cd22f5574de8445521c.png)
2. Enter the Windows instance's public IP after **Computer** and click **Connect**.
You can get the Window instance's public IP in the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
3. Enter the instance's admin account/password in the **Windows Security** pop-up window.
<dx-alert infotype="explain" title="">
If the **Do you trust this remote connection?** window pops up, you can select **Don't ask me again for connections to this computer** and click **Connect**.
</dx-alert>
4. Click **OK**.

:::
::: Linux


<dx-alert infotype="explain" title="">
We recommend you use rdesktop as the remote desktop client. For more information, see the [official introduction to rdesktop](http://www.rdesktop.org/).
</dx-alert>


1. Run the following command to check whether rdesktop has been installed.
```
rdesktop
```
   - If yes, perform [step 4](#step04).
   - If no, you will be prompted with "command not found". In this case, perform [step 2](#step02).
2. [](id:step02)Open a terminal window and run the following command to download rdesktop. This step uses rdesktop v1.8.3 as an example.
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
4. [](id:step04)Run the following command to connect to the remote Windows instance.
<dx-alert infotype="explain" title="">
Replace the parameters in the example with your own parameters.
</dx-alert>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
   - `Administrator` refers to the admin account mentioned in the prerequisites section.
   - `<your-password>` refers to the login password that you set.

    If you forgot your password, you can [reset it](https://intl.cloud.tencent.com/document/product/1103/41553).
   - `<hostname or IP address>` refers to the public IP address or custom domain name of your Windows instance.


:::
::: macOS

<dx-alert infotype="explain" title="">
- The following operations use Microsoft Remote Desktop for Mac as an example. Microsoft stopped providing a link to download the Remote Desktop client in 2017. Currently, its subsidiary HockeyApp is responsible for releasing the beta client. Go to [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) to download a Beta version.
- The following operations use a Lighthouse instance on Windows Server 2012 R2 as an example:
</dx-alert>


1. Download and install Microsoft Remote Desktop for Mac on your local computer.
2. Start MRD and click **Add Desktop**.
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. In the **Add PC** pop-up window, follow the steps illustrated in the following image to establish a connection to your Windows instance.
  ![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
    1. In the **PC name** field, enter the instance's public IP.
    2. Click **Add**.
    3. Retain the default settings for the other options and establish the connection.
    Your entry has now been saved
      ![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Double-click the new entry. In the pop-up window, enter your admin account and password obtained in "Prerequisites" as prompted and click **Continue**.
If you forgot your password, you can [reset it](https://intl.cloud.tencent.com/document/product/1103/41553).
5. In the pop-up window, click **Continue** to establish the connection.
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
If the connection is successful, the following Windows instance page will appear:
![](https://qcloudimg.tencent-cloud.cn/raw/09da9b26eb5ec4475ffe266e2761cf03.png)
:::
</dx-tabs>

