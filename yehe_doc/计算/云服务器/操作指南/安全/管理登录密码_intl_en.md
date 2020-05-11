## Introduction
CVM accounts and passwords can be used as credentials for CVM instances. This article describes how to use and manage passwords when logging in to a CVM instance.

## Password Requirements

A password must meet these requirements:
- Linux instance password: the password must consist of 8 to 30 characters. We recommend that you use a password of at least 12 characters. The password cannot start with `/` and must contain at least three of the following: (`a-z`, `A-Z`, `0-9` and special symbols ```()`~!@#$%^&*-+=_|{}[]:;'<>,.?/```).
- Windows instance password: the password must consist of 12 to 30 characters. The password cannot start with `/` and must contain at least three of the following: (`a-z`, `A-Z`, `0-9` and special symbols ```()`~!@#$%^&*-+=_|{}[]:;'<>,.?/```), and it cannot contain your user name.

## Directions

### Setting an initial password
There are two ways to set the initial password depending on how your configured your CVM instance when purchasing it:
 - If you used the [**Quick Configuration**](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly&regionId=33&zoneId=330001&instanceType=SA2.SMALL1&platform=CentOS&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR) option, the initial password is sent to you through an email and a message to the console [Message Center](https://console.cloud.tencent.com/message).
 - If you used the [**Custom Configuration**](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly&regionId=33&zoneId=330001&instanceType=SA2.SMALL1&platform=CentOS&systemDiskType=CLOUD_PREMIUM&systemDiskSize=50&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR&bandwidth=1) option, the initial password is set in the following ways depending on how you choose to log in:
<table>
	<tr><th>Login Method</th><th>Description</th></tr>
	<tr><td>Automatic password generation</td><td>The initial password is sent to you through email and the console <a href="https://console.cloud.tencent.com/message">Message Center</a>.</td></tr>
	<tr><td>Associate keys now</td><td><b>Disabled by default</b>. You log in using your user name and password, but the initial password is sent to you through email and the console <a href="https://console.cloud.tencent.com/message">Message Center</a>.</td></tr>
	<tr><td>Set a password</td><td>You set the initial password.</td></tr>
</table>


### Viewing the password

Your login password is sent to you through email and the console [Message Center](https://console.cloud.tencent.com/message). The following describes how to check your messages in the message center.
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/).
2. Click <img src="https://main.qcloudimg.com/raw/f5d915ab4297418f3eae30fd28f41122.png" style="margin: 0;"></img> in the upper right corner and select the corresponding product message, as shown in the following figure:
![](https://main.qcloudimg.com/raw/e3c624a805d2f5776807df44bd373b59.png)
View your password on the message page.
![](https://main.qcloudimg.com/raw/73bef8b11ded3d0cee5441d3d3218e25.png)

### Resetting the password

For instructions on how to reset your password, refer to [Resetting the Password of an Instance](http://intl.cloud.tencent.com/document/product/213/16566).
