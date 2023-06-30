## Overview

VNC login provided by Tencent Cloud allows users to remotely log in to CVM via a web browser. If a client does not have remote login installed or it cannot be used, user can log in to the CVM using VNC login to check the CVM status and perform basic management operations using the CVM account.

## Use Limits

- VNC login currently does not support copy and paste, Chinese input method, and file upload or download.
- When you use VNC to log in to CVM, mainstream browsers must be used, such as Chrome, Firefox, IE 10 and above.
- VNC login is a dedicated terminal, meaning only one user can use VNC login at a time.


## Prerequisites
You must already have admin account/password for logging into Windows instance remotely.
 - If you have chosen to generate a random password when creating an instance, please get it from [Message Center](https://console.cloud.tencent.com/message).
 - If you have set a login password, please use it for login. If you forgot it, please [reset it](https://intl.cloud.tencent.com/document/product/213/16566).


## Directions

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, locate the Windows CVM instance you want to log in to and click **Log In** as shown below:
![](https://main.qcloudimg.com/raw/e7b1192332a116edca67425a301236be.png)
3. In the **Standard Login | Windows Instance** window that is opened, select **login with VNC** as shown below:
![](https://main.qcloudimg.com/raw/9f964c1ebdec90f7e371b42340e13662.png)
4. In the login window that pops up, select **Send CtrlAltDel** in the upper-left corner and press **Ctrl-Alt-Delete** to open the system login window as shown below:
![](https://main.qcloudimg.com/raw/c07755c1e0d0040e2ecb87f048b8be1b.png)
5. Enter the login password and press **Enter** to log in to the Windows CVM instance.

