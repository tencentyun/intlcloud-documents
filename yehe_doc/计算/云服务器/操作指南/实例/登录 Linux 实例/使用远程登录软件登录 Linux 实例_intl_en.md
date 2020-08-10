## Overview

This document takes PuTTY as an example to describe how to log in to a Linux instance from Windows by using remote login software.


## Applicable OS

Windows

## Authentication Method

**Password** or **Key**

## Prerequisites
- You must already have the admin account and password (or key) of the instance to be logged in to.
 - If you use a system default password to log in to the instance, go to [Message Center](https://console.cloud.tencent.com/message) to obtain the password first.
 - If you forgot your password, please [reset your instance password](https://intl.cloud.tencent.com/document/product/213/16566).
- A public IP has been purchased and obtained for your CVM instance, and port 22 is open (this is open by default for CVM purchased with quick configuration).


## Directions

### Logging in with a password

1. Download the Windows remote login software, PuTTY.
To download PuTTY: [click here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
2. Double-click **putty.exe** to open the PuTTY client.
3. In the **PuTTY Configuration** window, enter the following content, as shown below:
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
Configure parameters as follows:
 - Host Name (or IP address): the public IP of the CVM. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to obtain the public IP from the instance list and details pages.
 - Port: The port of the CVM, which must be “22”.
 - Connect type: Select **SSH**.
 - Saved Sessions: Enter the session name, such as `test`.
 After configuring **Host Name**, configure and save **Saved Sessions**. You can double-click the session name saved under **Saved Sessions** to log in to CVM.
4. Click **Open** to enter the **PuTTY** interface. The **login as:** command prompt appears.
5. Enter the username after **login as:** and press **Enter**.
6. Enter the password after **Password** and press **Enter**.
The entered password is not displayed by default, as shown below:
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
Once logged in, you can see the information about the CVM to which you are currently logged into on the left of the command prompt.

### Logging in with a key

1. Download the Windows remote login software, PuTTY.
Download both putty.exe and puttygen.exe. To download PuTTY, [click here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
2. Double-click **puttygen.exe** to open the PuTTY Key client.
3. Click **Load**, select and access the path where the downloaded private key is saved, as shown below:
For example, select and open the private key file `david`.
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. <span id="Step4"></span>In the **PuTTY Key Generator** window, enter the key name and the encrypted private key password, and click **Save private key**, as shown below:
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. In the pop-up window, select the path where the key will be saved. In the **File name** field, enter “Key Name.ppk” and click **Save**. For example, save the private key file `david` as `david.ppk`, as shown below:
![](https://main.qcloudimg.com/raw/44df54ca77069356a26c51e2a4db7643.png)
6. Double-click **putty.exe** to open the PuTTY client.
7. In the left sidebar, go to **Connection** > **SSH** > **Auth** and enter the Auth configuration interface.
8. Click **Browse**, and select and access the path where the key is saved, as shown below:
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
9. Switch to the Session configuration interface. Configure the CVM IP, port, and connection type, as shown below:
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - Host Name (or IP address): the public IP of the CVM. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to obtain the public IP from the instance list and details pages.
 - Port: The port of the CVM, which must be “22”.
 - Connect type: Select **SSH**.
 - Saved Sessions: Enter the session name, such as `test`.
 After configuring **Host Name**, configure and save **Saved Sessions**. You can double-click the session name saved under **Saved Sessions** to log in to CVM.
9. Click **Open** to enter **PuTTY** interface. **login as:** appears.
10. Enter the user name after **login as:** and press **Enter**.
11. Enter the password configured in [Step 4](#Step4) after **Passphrase for key "imported-openssh-key":**.
The entered password is not displayed by default, as shown below:
![](https://main.qcloudimg.com/raw/89b2ef5f04a6402f0b1832301fa811cb.png)
Once logged in, you can see the information about the CVM to which you are currently logged into on the left of the command prompt.



## Subsequent Operations

After logging in to the CVM, you can build a personal website or forum or perform other operations. For more information, see the following documents:
- [Manually Building WordPress Website](https://intl.cloud.tencent.com/document/product/213/8044)
- [Manually Building Discuz! Forum](https://intl.cloud.tencent.com/document/product/213/8043)

