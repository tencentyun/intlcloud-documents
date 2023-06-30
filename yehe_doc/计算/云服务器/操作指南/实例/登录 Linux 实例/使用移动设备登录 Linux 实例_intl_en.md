## Overview
This document describes how to log in to a Linux instance from different mobile devices. The following tools are used as an example.
 - iOS device: Termius-SSH client
 - Android device: JuiceSSH

## Applicable Mobile Devices
iOS and Android devices

## Prerequisites
- The CVM instance is in the **Running** status.
- You already have the admin account and password (or key) to log in to the instance.
 - If you use a system default password to log in to the instance, go to [Message Center](https://console.cloud.tencent.com/message) to obtain the password first.
 - If you’ve forgotten your password, you can [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- A public IP has been purchased for your CVM instance, and the port 22 is open. It is open by default for a CVM instance purchased with quick configuration.

## Directions
Log in to the instance from the mobile device you are using:

<dx-tabs>
::: iOS\sdevice
1. Download the Termius-SSH client from the App Store, and register as instructed.
2. Tap **New Host** on the home screen.
3. Access the **New Host** page and configure the login information as follows:
![](https://main.qcloudimg.com/raw/b0a672d2fae5ed3cb8e08be6492987cd.jpg)
 - **Hostname**: the public IP address of your CVM instance. For more information, see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
 - **Use SSH**: enabled by default.
 - **Username**: enter the admin account `root`, or `ubuntu` if your instance uses the Ubuntu operating system.
 - **Password**: enter the login password of the instance.
4. Tap **Save** in the upper-right corner to save the login configuration.
5. Select the login information on the **Hosts** page and tap **Continue** in the prompt box at the bottom of the page.
![](https://main.qcloudimg.com/raw/2c1e0518f8bf4377c36ce92d0d484b57.jpg)
6. Login succeeds if you see the following.
![](https://main.qcloudimg.com/raw/54a7fde256f500b32a2b0753c0966b2d.jpg)
:::
::: Android\sdevice
#### Creating an identity[](id:newAuthentication)
1. Download and install JuiceSSH.
2. From the home screen, tap **Connections** to reach the **Identities** tab.
3. Tap **+** in the lower-right corner.
4. Configure the account name and password on the **Identity** page.
 - **Nickname**: enter a custom name for the identity, optional.
 - **Username**: enter the admin account `root`, or `ubuntu` if your instance uses the Ubuntu operating system.
 - **Password**: tap **Set (optional)** and enter the instance login password in the pop-up window.
5. Tap **✔** in the upper-right corner of the page.

#### Creating a connection
1. From the home screen, tap **Connections**, then tap **+** in the lower-right corner of the **Connections** page.
2. Configure the login information for the new connection.
 - **Nickname**: enter a custom connection name, optional.
 - **Type**: select **SSH**.
 - **Address**: the public IP address of your CVM instance. For more information, see [Getting Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/17940).
 - **Identity**: select the identity created in [Creating an identity](#newAuthentication).
 - **Port**: enter the port 22.
 Retain the default settings for other parameters.
3. Tap **Add to team** in the bottom of the page to save the login configuration.

#### Logging in to the instance
1. On the **Connections** page, select the instance to log in and tap **Accept**.
2. Login succeeds if you see the following.
  ![](https://main.qcloudimg.com/raw/a07b70fa518c0d474073515147487264.jpg)

:::
</dx-tabs>

