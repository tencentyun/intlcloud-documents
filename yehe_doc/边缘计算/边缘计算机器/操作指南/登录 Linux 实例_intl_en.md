## Overview
ECM supports the following two login methods:
- [Login through VNC](#ECM_VNCLoginLinux)
- [Login over SSH](#ECM_SSHLoginLinux)

After creating an ECM instance successfully, you can log in to it as instructed in this document.

## Prerequisites

- You have created an ECM instance and obtained its public IP.
- You already have the administrator account and password to log in to the instance.
If you forgot your password, you can [reset it](https://intl.cloud.tencent.com/document/product/1119/43428).
- If you want to log in to a Linux instance over SSH, ensure that Xshell has been installed on the local PC.

## Directions

<span id="ECM_VNCLoginLinux"></span>
### Logging in through VNC

1. Log in to the [ECM console](https://console.cloud.tencent.com/ecm/overview) and select **Instance List** on the left sidebar.
2. In **Instance List**, select the target Linux instance and click **Login** as shown below: 
![](https://qcloudimg.tencent-cloud.cn/raw/5e31ba1eaff47d5fbd4bc3ac9d6bdb4c.png)
3. In the **Log in to Linux Instance** pop-up window, select **Log in Through VNC** and click **Log in Now** .
4. In the pop-up dialog box, enter the username after **login** and press **Enter**.
5. Enter the password after **Password** and press **Enter**.
The entered password is not displayed by default.

<span id="ECM_SSHLoginLinux"></span>
### Logging in over SSH
>? There are multiple software applications for remote login to a Linux instance, such as PuTTY and Xshell. This document uses Xshell 6 as an example to describe how to use remote login software to log in to a Linux instance on a local Windows PC.
>

1. Open the Xshell client and click **New**.
2. In the **New Session Properties** window, enter the following content.
 - Name: enter a session name, such as `test`.
 - Host: enter the public IP of the ECM instance (log in to the [ECM console](https://console.cloud.tencent.com/ecm/instance), and you can get the public IP on the instance list page).
 - Protocol: select "SSH".
 - Port Number: enter the port of the ECM instance, which must be set to 22.
3. Click **Connect**.
4. Enter the login username such as `root` and click **OK** .
5. Enter the login password and click **OK** .
Once logged in, you can see the information of the ECM instance to which you are currently logged in on the left of the command prompt.

