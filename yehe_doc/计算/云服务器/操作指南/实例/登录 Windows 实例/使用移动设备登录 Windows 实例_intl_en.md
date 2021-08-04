## Overview
This document describes how to log in to a Windows instance from different mobile devices using Microsoft Remote Desktop.

## Applicable Mobile Devices
iOS and Android devices

## Prerequisites
- The CVM instance is in the **Running** status.
- You already have the administrator account and password to log in to the instance.
 - If you use a system default password to log in to the instance, go to [Message Center](https://console.cloud.tencent.com/message) to obtain the password first.
 - If you’ve forgotten your password, you can [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- A public IP has been purchased for your CVM instance, and the port 3389 is open. It is open by default for a CVM instance purchased with quick configuration.

## Directions
>? This document uses the iOS device as an example. Steps for Android devices are almost the same.
>
1. Download Microsoft Remote Desktop and start it.
2. In the **PCs** page, tap **+** in the upper-right corner, then tap **Add PC**.
2. Configure the login information to add a PC.
 - **PC name**: the public IP address of your CVM instance. For more information, see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
 - **User account**: by default, **Ask when required** is selected.
4. Tap **Save**.
5. In the **PCs** page, select the instance to log in and enter its administrator account and password.
 - **User name**: enter the administrator account `Administrator`.
 - **Password**: enter the instance login password.
6. Tap **Continue**. If the page shown in the following figure is displayed, the login succeeds.
 ![](https://main.qcloudimg.com/raw/60abc6a9f51ae33ea95aa11edc53e009.jpg)
