## Overview
This document describes how to log in to a Windows instance through remote desktop on a local computer.

## Supported Systems

Windows

## Prerequisites[](id:Preconditions)

- You must have the admin account and password for logging in to a Windows instance remotely.
 - If you use a system default password to log in to the instance, you can obtain the password at the [Message Center](https://console.cloud.tencent.com/message).
 - If you forgot your password, please [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- You have purchased public IPs for your CVM instance and port 3389 is open (this port is open by default for a CVM purchased with quick configuration).

## Directions


<dx-alert infotype="explain" title="">
The following takes the Windows 7 operating system as an example.
</dx-alert>

1. On the local Window server, click <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: -5px 0px;width: 35px;">, enter **mstsc** in **Search programs and files**, and press **Enter** to open the **Remote Desktop Connection** window as shown below:
![](https://main.qcloudimg.com/raw/d8a4b0f70f876f6c0edc6e995a02c37d.png)
2. Enter the public IP of the Windows server after **Computer** and click **Connect**. You can get the server public IP as instructed in [Getting Public IP Address](https://intl.cloud.tencent.com/document/product/213/17940).
3. Enter the instance's admin account and password in the **Windows Security** pop-up window as shown below:
<dx-alert infotype="explain" title="">
 - If the **Do you trust this remote connection?** window pops up, you can select **Don't ask me again for connections to this computer** and click **Connect**.
 - The default admin account of the Windows CVM instance is `Administrator`, and the password can be obtained as instructed in [Prerequisites](#Preconditions).
</dx-alert>
<img src="https://main.qcloudimg.com/raw/5d3d89e3ec4616a367b80ba377a3f541.png"/>
4. Click **OK**.

