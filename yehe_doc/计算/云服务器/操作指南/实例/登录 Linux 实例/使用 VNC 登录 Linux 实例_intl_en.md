## Overview

VNC login provided by Tencent Cloud allows users to remotely log in to CVM via a web browser. If a client does not have remote login installed or it cannot be used, user can log in to the CVM using VNC login to check the CVM status and perform basic management operations using the CVM account.


## Use Limits

- VNC login currently does not support copy and paste, Chinese input method, and file upload or download.
- When you use VNC to log in to CVM, mainstream browsers must be used, such as Chrome, Firefox, IE 10 and above.
- VNC login is a dedicated terminal, meaning only one user can use VNC login at a time.

## Prerequisites
You already have the admin account and password to log in to the instance.
- If you have chosen to generate a random password when creating an instance, please get it from [Message Center](https://console.cloud.tencent.com/message).
- If you have set a login password, please use it for login. If you forgot it, please [reset it](https://intl.cloud.tencent.com/document/product/213/16566).


## Directions

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, locate the Linux CVM instance you want to log in to and click **Log In** as shown below:
![](https://main.qcloudimg.com/raw/a4cc736f2dc7f13bf39756b8e39532d4.png)
3. In the **Standard Login | Linux Instance** window that is opened, select **login with VNC** as shown below:
![](https://main.qcloudimg.com/raw/1bd4877abc15d06adb8c54fc7ed1318e.png)
4. In the opened window, enter the username after **login** and press **Enter**.
The default username of Linux instances is `root`, and the default username of Ubuntu instances is `ubuntu`. Please enter as needed.
5. Enter the password after **Password** and press **Enter**.
The entered password is not displayed by default. After login, the information of the CVM that you are currently logged in to will appear on the left of the command prompt as shown below:
![](https://main.qcloudimg.com/raw/03a8492f66e8342221858709b6068669.png)


## Operations


After logging in to the CVM, you can build a personal website or forum or perform other operations. For more information, please see:
- [Common Operations and Commands](https://intl.cloud.tencent.com/document/product/213/2150) 
- [Manually Building WordPress Website](https://intl.cloud.tencent.com/zh/document/product/213/8044)
- [Manually Building Discuz! Forum](https://intl.cloud.tencent.com/zh/document/product/213/8043)

