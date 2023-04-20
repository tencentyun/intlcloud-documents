>!  **WebRDP is the default login method** for Windows instances. It allows you to log in to a Windows instance in the CVM console without downloading a local login client.
>

## Overview
Remote Desktop Protocol (RDP) is a multiple-channel protocol developed by Microsoft that allows a local computer to connect to a remote computer. We recommend you use RDP to log in to your Windows CVMs. This document describes how to log in to Windows instances using RDP files.

## Supported Systems
You can log in to your CVMs from Windows, Linux, and MacOS servers using RDP.

## Prerequisites

- You must have the admin account and password for logging in to a Windows instance remotely.
  - If you have chosen to generate a random password when creating an instance, please get it from [Message Center](https://console.cloud.tencent.com/message).
  - If you have set a login password, please use it for login. If you forgot it, please [reset it](https://intl.cloud.tencent.com/document/product/213/16566).
- You have purchased a public IP for your CVM instance and opened a remote login port (3389 by default) for the WebRDP proxy IP in the security group associated with the instance.
  - If you purchase a CVM instance through quick configuration, the port is opened by default.
  - If you purchase a CVM instance through custom configuration, you can manually open the port as instructed in [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369).
- Make sure that the public network bandwidth of your instance is ≥ 5 Mbit/s; otherwise, the remote desktop may lag. To adjust the network bandwidth, please see [Adjusting Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517).


## Directions
<dx-tabs>
::: From Windows server[](id:windowsRDP)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, locate the Windows CVM instance you want to log in to and click **Log In**.
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. In the **Standard Login | Windows Instance** window that is opened, select **Download RDP File**.
<dx-alert infotype="explain" title="">
If you have changed the remote login port, append the IP address with `:port` in the RDP file.
</dx-alert>
![](https://main.qcloudimg.com/raw/0b0076390b95da3885c8967093683975.png)
4. Double-Click the downloaded RDP file, enter the password, and click **OK** to remotely connect to your Windows CVM.
  - If you use a system default password to log in to the instance, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message).
  - If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
:::
::: From Linux server[](id:LinuxRDP)
<dx-alert infotype="explain" title="">
We recommend you use rdesktop as the remote desktop client. For more information, please see the [official introduction to rdesktop](http://www.rdesktop.org/).
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
4. [](id:step04)Run the following command to connect to the remote Windows instance.</span>
<dx-alert infotype="explain" title="">
Replace the parameters in the example with your own parameters.
</dx-alert>
```
rdesktop -u Administrator -p <your-password> <hostname or IP address>
```
 - `Administrator` refers to the admin account mentioned in the prerequisites section.
 - `<your-password>` refers to the login password that you set.
   If you use a system default password to log in to the instance, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message). If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
 - `<hostname or IP address>` is the public IP or custom domain name of your Windows instance. For more information on how to get the public IP, please see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
:::
::: From MacOS server[](id:MacRDP)
<dx-alert infotype="explain" title="">
-The following operations use Microsoft Remote Desktop for Mac as an example. Microsoft stopped providing a link to download the Remote Desktop client in 2017. Currently, its subsidiary HockeyApp is responsible for releasing the beta client. Go to [Microsoft Remote Desktop Beta](https://install.appcenter.ms/orgs/rdmacios-k2vy/apps/microsoft-remote-desktop-for-mac/distribution_groups/all-users-of-microsoft-remote-desktop-for-mac) to download a Beta version.
-The following operations use a CVM on Windows Server 2012 R2 as an example.
</dx-alert>
1. Download and install Microsoft Remote Desktop for Mac on your local computer.
2. Start MRD and click **Add Desktop**.
![](https://main.qcloudimg.com/raw/e69528d10e9a17dfa26119a090766c49.png)
3. In the **Add PC** pop-up window, follow the steps illustrated in the following image to establish a connection to your Windows CVM.
![](https://main.qcloudimg.com/raw/d8e20278dd7c8aed487be2c43986f5e4.png)
     1. In the **PC name** text file, enter the public IP address of your CVM instance. For more information on how to obtain the public IP address, please see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
     2. Click **Add**.
     3. Retain the default settings for the other options and establish the connection.
    Your entry has now been saved.
![](https://main.qcloudimg.com/raw/1c0eff28aa68a7f02e8f295917bb603b.png)
4. Double-click the new entry. Input your username and password for CVM and click **Continue**.
5. If you use a system default password to log in to the instance, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message).
6. If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
7. In the pop-up window, click **Continue** to establish the connection.
![](https://main.qcloudimg.com/raw/61b3d9566365183fcc1d92c2f6bc2e7b.png)
If the connection is successful, the following page will appear:
![](https://main.qcloudimg.com/raw/20db4a1d63384bc0575ded68a8fe912d.png)
:::
</dx-tabs>

## RDP Bandwidth Limit Description[](id:illustrate)
The available network bandwidth directly affects the experience of logging in to and using CVM instances over RDP, and different applications and display resolutions require different network configurations. Microsoft has laid down the minimum bandwidth requirements for instances when using RDP in different application scenarios. Please check out the following table to make sure that the network configuration of your instance can meet your business needs; otherwise, issues such as lag may occur.

To adjust the bandwidth of your instance, please see [Adjusting Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517).
</dx-alert>
These numbers apply to a single monitor configuration with 1920x1080 resolution and with both default graphics mode and H.264/AVC 444 graphics mode.

<table>
<tr>
<th width="15%">Scenario</th>
<th width="19%">Default Mode</th>
<th width="19%">H.264/AVC 444 Mode	</th>
<th width="47%">Description</th>
</tr>
<tr>
<td>Idle</td>
<td>0.3 Kbps	</td>
<td>0.3 Kbps</td>
<td>User has paused their work, and there's no active screen updates.</td>
</tr>
<tr>
<td>Microsoft Word</td>
<td>100–150 Kbps</td>
<td>200–300 Kbps</td>
<td>User is actively working with Microsoft Word, typing, pasting graphics, and switching between documents.</td>
</tr>
<tr>
<td>Microsoft Excel</td>
<td>150–200 Kbps</td>
<td>400–500 Kbps</td>
<td>User is actively working with Microsoft Excel and updating multiple cells with formulas and charts simultaneously.</td>
</tr>
<tr>
<td>Microsoft PowerPoint</td>
<td>4–4.5 Mbps</td>
<td>1.6–1.8 Mbps</td>
<td>User is actively working with Microsoft PowerPoint, typing, and pasting. User is also modifying rich graphics and using slide transition effects.</td>
</tr>
<tr>
<td>Web browsing</td>
<td>6–6.5 Mbps</td>
<td>0.9–1 Mbps</td>
<td>User is actively working with a graphically rich website that contains multiple static and animated images. User scrolls the pages both horizontally and vertically.</td>
</tr>
<tr>
<td>Image gallery</td>
<td>3.3–3.6 Mbps	</td>
<td>0.7–0.8 Mbps</td>
<td>User is actively working with the image gallery application, browsing, zooming, resizing, and rotating images.</td>
</tr>
<tr>
<td>Video playback</td>
<td>8.5–9.5 Mbps</td>
<td>2.5–2.8 Mbps</td>
<td>User is watching a 30 FPS video that consumes 1/2 of the screen.</td>
</tr>
<tr>
<td>Fullscreen video playback</td>
<td>7.5–8.5 Mbps</td>
<td>2.5–3.1 Mbps</td>
<td>User is watching a 30 FPS video that is maximized to a fullscreen.</td>
</tr>
</table>
