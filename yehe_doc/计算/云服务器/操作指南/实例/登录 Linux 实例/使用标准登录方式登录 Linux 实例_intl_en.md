### Scenario

WebShell is the login method recommended by Tencent Cloud. No matter your local OS is Windows, Linux or Mac OS, as long as you have purchased public IPs for your instances, you can log in via Web Shell. This document describes how to log into a Linux instance via Web Shell.
Benefits of Web Shell:
- Supports copy and paste operations with shortcut keys.
- Supports scrolling with mouse wheel.
- Supports Chinese input.
- Features a high security (password or key is required for each login).

## Applicable Local OS

Windows, Linux, or Mac OS.

## Authentication Method

**Password** or **Key**

## Prerequisites

- You must already have the admin account and password (or key) for the instance to be logged in to.
 - If you choose **Random Password** when creating the instance, please go to [Internal Message](https://console.cloud.tencent.com/message) to check the password.
 - If you forgot your password, then [reset the instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- Make sure the CVM instance has a public IP, and port 22 is open (if the CVM is purchased with “Quick Configuration”, this port is open by default.)

### Directions

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance’s management page, select the Linux CVM that you want to log in to and click **Log In**, as shown below:
![](https://main.qcloudimg.com/raw/cc5786b9f8b57ff4057b666503729bc0.png)
3. In the **Log into Linux Instance** pop-up window, select **Standard login method** and click **Log In Now**, as shown below.
![](https://main.qcloudimg.com/raw/87ba7e511f8d0ffe48f220cecaa7b057.png)
4. In the **Log into Instance** window, select **Password Login** or **Key Login**, as shown below:
![](https://main.qcloudimg.com/raw/9c321ad519c8f993c1f768e56fca0ab1.png)
If the login is successful, “Socket connection established” will display as shown below:
![](https://main.qcloudimg.com/raw/6bcd152ff947909f52da67430aa7eda6.png)

## Subsequent Operations

After logging into the CVM, you can build a personal website or forum on the Tencent Cloud CVM or perform other operations. For more information, see the following documents:
- [Build a personal WordPress site](https://intl.cloud.tencent.com/document/product/213/8044)

