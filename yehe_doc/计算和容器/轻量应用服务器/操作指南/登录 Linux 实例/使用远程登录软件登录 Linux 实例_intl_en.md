## Overview
This document takes PuTTY as an example to describe how to log in to a Linux instance from a Windows local computer by using the remote login software.

## Supported Operating Systems
Windows
<dx-alert infotype="explain" title="">
If your local computer uses Linux or macOS, [use SSH to log in to the Linux instance](https://intl.cloud.tencent.com/document/product/1103/41525).
</dx-alert>



## Authentication Method
**Password** or **Key**

## Prerequisites

- You have obtained the username and password (or SSH key) to log in to the instance.
<dx-alert infotype="notice" title="">
If it is your first time to log in to a Linux instance through a local remote login application, you need to reset the password of your username (e.g., `root` and `ubuntu`) or bind your key. For detailed directions, see [Resetting Password](https://intl.cloud.tencent.com/document/product/1103/41553) and [Managing Key](https://intl.cloud.tencent.com/document/product/1103/41392).
</dx-alert>
- Make sure the network connection between the local computer and the instance is working, and the port 22 is open in the firewall policies of the instance (Port 22 is open by default upon the creation of the instance).

## Limits

For instances created with Ubuntu images, password login is disabled by default for the `root` account. To enable it, see [Uploading Local Files](https://intl.cloud.tencent.com/document/product/1103/41257).

## Directions

<dx-tabs>
::: Password login
1. Download the Windows remote login software: PuTTY.
[Download PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
2. Double-click **putty.exe** to open the PuTTY Client.
3. In the **PuTTY Configuration** window, enter the following content, as shown below:
![](https://main.qcloudimg.com/raw/7ac87da9721ef7d64fe8cac81a3dab33.png)
Configure parameters as follows:
   - **Host Name (or IP address)**: The public IP of the Lighthouse instance. You can check this public IP in the [Lighthouse console](https://console.cloud.tencent.com/cvm/index). 
   - **Port**: The port open for remote login on the Lighthouse side. For a Linux instance, it defaults to 22.
   - **Connection type**: Select **SSH**.
   - **Saved Sessions**: Enter the session name, such as `test`.
After configuring **Host Name**, configure and save **Saved Sessions**. You can double-click the session name saved under **Saved Sessions** to log in to the instance.
4. Click **Open** to enter the **PuTTY** page. The **login as:** command prompt appears.
5. Enter your username after **login as:** (e.g., `root`) and press **Enter**.
<dx-alert infotype="explain" title="">
For all Linux images, except Ubuntu images, you can log in with the `root` account. For Ubuntu system, the default username is `ubuntu`. To log in with the `root` account, see [How do I log in to an instance with root on Ubuntu?](https://intl.cloud.tencent.com/document/product/1103/41257).
</dx-alert>
6. Enter your password after **Password** and press **Enter**.
The entered password is invisible by default.
![](https://main.qcloudimg.com/raw/9e7ddc631de2a27bfd35f9225de85506.png)
Once logged in, you can see the information about the current Lighthouse instance on the left side of the command prompt.

:::
::: SSH key login
1. Download the Windows remote login software, PuTTY.
Download both putty.exe and puttygen.exe. To download PuTTY, [click here](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).
2. Double-click **puttygen.exe** to open the PuTTY Key Client.
3. Click **Load**, select and open the path where the downloaded private key is saved, as shown below:
For example, select and open the private key file `david`.
![](https://main.qcloudimg.com/raw/0110ba722331fb2892a8e6822ec3f709.png)
4. <span id="Step4"></span>In the **PuTTY Key Generator** window, you can enter the key name and create a password for the key (optional). When finished, click **Save private key**, as shown below:
![](https://main.qcloudimg.com/raw/58a250d3f3d1b78eff3edaab64cd01c0.png)
5. In the pop-up window, select the path to store the key. In the **File name** field, enter “[Key Name].ppk” and click **Save**. For example, save the private key file `david` as `david.ppk`.
![](https://qcloudimg.tencent-cloud.cn/raw/9742e84d2b9ab282eda4a4ef5fe96b7a.png)
6. Double-click **putty.exe** to open the PuTTY Client.
In the left sidebar, select **Connection** > **SSH** > **Auth** to enter the Auth configuration page.
8. Click **Browse** to select and open the path where the key is saved.
![](https://main.qcloudimg.com/raw/61993f3977ff681b8b2d78beac55f2ca.png)
9. Switch to the **Session** configuration page. Configure the server IP, port, and connection type.
![](https://main.qcloudimg.com/raw/ddfd58429288ce0e195e86a6cb1c9cd6.png)
   - <b>Host Name (IP address)</b>: The public IP of the Lighthouse instance. You can check this public IP in the [Lighthouse console](https://console.cloud.tencent.com/cvm/index). 
   - **Port**: The port open for remote login on the Lighthouse side. For a Linux instance, it defaults to 22.
   - **Connection type**: Select **SSH**.
   - **Saved Sessions**: Enter the session name, such as `test`.
After configuring **Host Name**, configure and save **Saved Sessions**. You can double-click the session name saved under **Saved Sessions** to log in to the instance.
10. Click **Open** to enter the **PuTTY** running interface. The **login as:** command prompt appears.
11. Enter your username after **login as:** and press **Enter**.
<dx-alert infotype="explain" title="">
For all Linux images, except Ubuntu images, you can log in with the `root` account. For Ubuntu system, the default username is `ubuntu`. To log in with the `root` account, see [How do I log in to an instance with root on Ubuntu?](https://intl.cloud.tencent.com/document/product/1103/41257).
</dx-alert>
If a password is set for the encrypted private key in [Step 4](#Step4), enter the password here and press **Enter**. The password is invisible by default. 
![](https://main.qcloudimg.com/raw/401da3ef001f103115aa8ba8c54d6ec8.png)
Once logged in, you can see the information about the current Lighthouse instance on the left side of the command prompt.

:::
</dx-tabs>





