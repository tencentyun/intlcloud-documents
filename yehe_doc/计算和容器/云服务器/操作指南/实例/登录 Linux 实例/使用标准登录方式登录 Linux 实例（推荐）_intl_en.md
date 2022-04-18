## Overview
WebShell is the login method recommended by Tencent Cloud. No matter your local OS is Windows, Linux or Mac OS, as long as you have purchased public IPs for your instances, you can log in via Web Shell. This document describes how to log in to a Linux instance via Web Shell.
Benefits of Web Shell:
- Supports copy and paste operations with shortcut keys.
- Supports scrolling with mouse wheel.
- Supports Chinese input.
- Features a high security (password or key is required for each login).

## Authentication Method

**Password** or **Key**

## Prerequisites[](id:Prerequisites)

- You already have the admin account and password (or key) to log in to the Linux instance.
 - If you have chosen to generate a random password when creating an instance, please get it from [Message Center](https://console.cloud.tencent.com/message).
 - If you have set a login password, please use it for login. If you forgot it, please [reset it](https://intl.cloud.tencent.com/document/product/213/16566).
 - If a key has been bound to the instance, you can use the key to log in. For more information, see [SSH Keys](https://intl.cloud.tencent.com/document/product/213/6092).
- You have purchased a public IP for your CVM instance and opened a remote login port (22 by default) for the WebShell proxy IP in the security group associated with the instance.
 - If you purchase a CVM instance through quick configuration, the port is opened by default.
 - If you purchase a CVM instance through custom configuration, you can manually open the port as instructed in [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369).

## Directions

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, proceed according to the actually used view mode:
<dx-tabs>
::: List view
Locate the Linux CVM instance you want to log in to and click **Log In** on the right as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: Tab view
Select the tab of the Linux CVM instance you want to log in to and click **Log In** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>

3. In the **Standard Login | Linux Instance** pop-up window, select **Password Login** or **Key Login** as needed:
![](https://main.qcloudimg.com/raw/9c321ad519c8f993c1f768e56fca0ab1.png)
Refer to the following instructions to enter the required information for login:
 - **Port**: the default port is 22. Enter a value as needed.
 - **Username**: the default username of Linux instances is `root`, and the default username of Ubuntu instances is `ubuntu`. Enter a value as needed.
 - **Password**: enter the login password obtained in the [Prerequisites](#Prerequisites) step.
 - **Key**: select the key bound to the instance.
4. Click **Log In** to log in to the Linux instance.
If the login is successful, the following prompt will appear on the WebShell page:
![](https://main.qcloudimg.com/raw/6bcd152ff947909f52da67430aa7eda6.png)

## Subsequent Operations

After logging in to the CVM, you can build a personal website or forum or perform other operations. For more information, see:
- [Manually Building a WordPress Website](https://intl.cloud.tencent.com/document/product/213/8044)
- [Manually Building Discuz! Forum](https://intl.cloud.tencent.com/document/product/213/8043)


## See Also
- [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566)
- [Managing SSH Keys](https://intl.cloud.tencent.com/document/product/213/16691)
