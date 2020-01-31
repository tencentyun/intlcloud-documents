## Scenario

This document takes PuTTY software as an example to describe how to log in to a Linux instance by using remote login software on a local computer with a Windows system.


## Applicable local OS

Windows

## Authentication Method

**Password** or **Key**

## Prerequisites
- You must already have the admin account and password (or key) for logging into the instance.
 - If you use a system default password to log in to the instance, obtain it by visiting [Internal Message](https://console.cloud.tencent.com/message).
 - If you forget your password, [reset the instance password](http://intl.cloud.tencent.com/document/product/213/16566).
- A public IP has been purchased and obtained for your CVM instance, and port 22 is open (this is open by default for CVMs purchased with quick configuration).


## Steps

### Logging in with a password

1. Download the Windows remote login software, PuTTY.
How to get PuTTY: [Click here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
2. Double click **putty.exe** to open the PuTTY client.
3. In the **PuTTY Configuration** window, enter the following content. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
Parameters are as follows:
 - Host Name (or IP address): The public IP of the CVM (log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to obtain the public IP in the list and details pages).
 - Port: The port of the CVM. This must be set to 22.
 - Connect type: Select **SSH**.
 - Saved Sessions: Enter the session name, such as `test`.
 After configuring the **Host Name**, configure **Saved Sessions** and save it. You can double click the session name saved under **Saved Sessions** to directly log into the CVM from now on.
3. Click **Open** to enter **PuTTY** interface. **login as:** appears.
4. Enter the user name after **login as:** and press **Enter**.
5. Enter the password after **Password** and press **Enter**.
Information about the CVM that you are currently logged in to will appear on the left of the command prompt. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)

### Logging in with a key

1. Download the Windows remote login software, PuTTY.
Download putty.exe and puttygen.exe software. To obtain PuTTy, [click here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
2. Double click **puttygen.exe** to open the PuTTY Key client.
3. Click **Load**, select and open the saved path of the downloaded private key. This is shown in the following figure:
For example, select and open the private key file that has the file name **david**.
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. In the **PuTTY Key Generator** window, enter the key name and the encrypted private key password. Click **Save private key**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. In the pop-up window, select the path where the key will be saved. In the file name field, enter **Key Name.ppk**, and click **Save**. For example, save the `david` private key file as `david.ppk` key file. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/d0fa9fd8aad7d2259bd8a0ce48ae5160.png)
6. Double click **putty.exe** to open the PuTTY client.
7. In the left sidebar, select **Connection** > **SSH** > **Auth**, to enter the Auth configuration interface.
8. Click **Browse**, select and open the saved path of the key. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
8. Switch to the Session configuration interface. Configure the CVM’s IP, port, and connection type. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
 - Host Name (IP address): The public IP of the CVM. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index) to obtain the public IP in the list and details pages.
 - Port: Port of the CVM, which must be 22.
 - Connect type: Select **SSH**.
 - Saved Sessions: Enter the session name, such as `test`.
 After configuring the **Host Name**, configure **Saved Sessions** and save it. You can double click the session name saved under **Saved Sessions** to directly log into the CVM from now on.
9. Click **Open** to initiate the login request.

## Subsequent Operations

After logging into the CVM, you can build a personal website or forum on Tencent Cloud CVM or perform other operations. For more information, see the following:
- [Building a personal WordPress website]
- [Building a Discuz! forum]

