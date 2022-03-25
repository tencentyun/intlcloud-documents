## Overview
This document describes how to log in to a Windows instance using the standard login method (WebRDP). 

<dx-alert infotype="explain" title="">
This method does not vary by the local operating system and supports direct login to the Windows instance in the console.
</dx-alert>



## Prerequisites[](id:Prerequisites)
- You must have the admin account and password for logging in to a Windows instance remotely.
 - If you have set a login password, please use it for login. If you forgot it, please [reset it](https://intl.cloud.tencent.com/document/product/213/16566).
 - If you have chosen to generate a random password when creating an instance, please get it from [Message Center](https://console.cloud.tencent.com/message).
- You have purchased a public IP for your CVM instance and opened a remote login port (3389 by default) for the WebRDP proxy IP in the security group associated with the instance.
 - If you purchase a CVM instance through quick configuration, the port is opened by default.
 - If you purchase a CVM instance through custom configuration, you can manually open the port as instructed in [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369).
- Make sure that the public network bandwidth of your instance is ≥ 5 Mbit/s; otherwise, the remote desktop may lag. To adjust the network bandwidth, please see [Adjusting Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517).


## Directions

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, proceed according to the actually used view mode:
<dx-tabs>
::: List view
Locate the Windows CVM instance you want to log in to and click **Log In** on the right as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: Tab view
Select the tab of the Windows CVM instance you want to log in to and click **Log In** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>
3. In the **Standard Login | Windows Instance** window that is opened, enter the login information according to the actual situation.
 - **Port**: the default port is 3389. Enter a value as needed.
 - **Username**: the default username of Windows instances is `Administrator`. Enter a value as needed.
 - **Password**: enter the login password obtained in the [Prerequisites](#Prerequisites) step.
5. Click **Log In** to log in to the Windows instance.
This document uses logging in to a CVM instance on Windows Server 2016 Datacenter Edition 64-bit as an example. If the login is successful, a page similar to the following will appear:
![](https://main.qcloudimg.com/raw/60abc6a9f51ae33ea95aa11edc53e009.jpg)


## Relevant Documentation
- [Resetting Instance Password](https://intl.cloud.tencent.com/document/product/213/16566)
- [Adjusting Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517)
