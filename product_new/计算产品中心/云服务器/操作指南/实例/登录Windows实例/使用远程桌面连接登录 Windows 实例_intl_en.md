## Scenario

This document describes how to log in to a Windows instance through remote desktop on a local computer.

## Applicable OS

Windows

## Prerequisites

- You must already have the admin account/password for logging into Windows instance remotely.
 - If you use a system default password to log in to the instance, obtain it by visiting [Internal Message](https://console.cloud.tencent.com/message).
 If you forgot the password, then [reset instance password](http://intl.cloud.tencent.com/document/product/213/16566).
- A public IP has been purchased for your CVM instance, and port 3389 is open (if the CVM is purchased with “Quick Configuration”, this port is open by default.)

## Steps
> The following steps take the Windows 7 operating system as an example.
>
1. On the local Windows computer, click <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 35px;">, and enter **mstsc** in **Search programs and files** and press **Enter** to open the remote desktop connection dialog box, as shown below:
![](https://main.qcloudimg.com/raw/d8a4b0f70f876f6c0edc6e995a02c37d.png)
2. Enter the Windows server’s public IP after **Computer** and click **Connect**.
3. Enter the instance’s admin account/password in the **Windows Security** pop-up window, as shown below:
> If the **Do you trust this remote connection?** dialog box pops up, you can check **Don’t ask me again for connections to this computer** and click **Connect**.

![](https://main.qcloudimg.com/raw/5d3d89e3ec4616a367b80ba377a3f541.png)
4. Click **OK** to log in to the Windows CVM instance.

