## Scenario

RemoteFx is an upgraded version of Windows Remote Desktop Protocol (RDP). From RDP 8.0, RemoteFx can be used to redirect local USB devices to a remote desktop through the RDP data channel, ensuring that the CVM can use these USB devices.

This document uses the following environment versions as examples to describe how to enable the RemoteFx USB redirection feature of RDP to redirect USB devices to a CVM.
- Client: Windows 10
- Server: Windows Server 2016

## Use Limits

Given that RDP 8.0 and subsequent versions all support the RemoteFX USB Redirection feature, it follows that Windows Server 2012 and later versions are all compatible with the RemoteFX USB Redirection feature. If your local computer's operating system is Windows Server 2008 R2, it is advisable to upgrade to a higher supported version to ensure the system's optimal performance.


## Directions

### Configuring the server

1. [Logging in to a Windows instance using the RDP file (recommended)](https://intl.cloud.tencent.com/document/product/213/5435).
2. On the desktop, click <img src="https://main.qcloudimg.com/raw/ab9a3a22baf69f63a90a43476f12db94.png" style="margin: 0;"></img> and select **Server Manager** to open Server Manager.
3. In the "Server Manager" window, click **Add roles and features**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/4ee64b60cf2993013698c2f641ea8dc1.png)
4. In the pop-up "Add Roles and Features Wizard" window, click **Next** to go to the "Select installation type" page.
5. On the "Select installation type" page, select **Role-based or feature-based installation** and click **Next**.
6. On the "Select destination server" page, keep the default configurations and click **Next**.
7. On the "Select server roles" page, select **Remote Desktop Services** and click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/76481a67eb8aa5b98e2e8a8de5895263.png)
8. Keep the default configurations and click **Next** for 2 times.
9. On the "Select role services" page, select **Remote Desktop Session Host**, **Remote Desktop Connection Broker**, and **Remote Desktop Licensing**. In the pop-up window, click **Add Features**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/38d46bf2c391f82684c5c82c439df3ec.png)
10. Click **Next**.
11. Click **Install**.
12. After the installation is completed, restart the CVM.
13. On the desktop, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, enter **gpedit.msc**, and press Enter to open "Local Group Policy Editor".
14. In the leftside navigation tree, choose **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Device and Resource Redirection**, and double-click **Do not allow supported Plug and Play device redirection**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/9d62d199cb34482f6c80f3dddb47bb0e.png)
15. In the pop-up window, select **Disabled** and click **OK**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a76cf6ec239df644f6905eca7de3a2bd.png)
16. Restart the CVM.


### Configuring the client

1. On the local PC, right-click <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> and choose **Run** to open the "Run" dialog box, as shown in the following figure:
2. In the "Run" dialog box, enter **gpedit.msc** and click **OK** to open "Local Group Policy Editor".
3. In the leftside navigation tree, choose **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Connection Client** > **RemoteFx USB Redirection** and double-click **Allow RDP redirection of other supported RemoteFx USB devices**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/e65d8e43fcf5531c701d08e257daa20f.png)
4. In the pop-up window, select **Enabled** and set the RemoteFx USB redirection access permission to **Administrators and Users**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8fc197ed25e82d2f85ad32144b197a06.png)
5. Click **OK**.
6. Restart the local PC.

### Verifying the configuration result

1. On your local PC, insert a USB device, right-click <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> and choose **Run** to open the "Run" dialog box.
2. In the "Run" dialog box, enter **mstsc** and press Enter to open the remote desktop connection dialog box, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5478a5d46f6825cdfe604600a1391f4d.png)
3. Enter the Windows server's public IP address in **Computer**, and then click **Options**.
4. On the **Local Resources** tab page, click **More** under "Local devices and resources", as shown in the following figure:
![](https://main.qcloudimg.com/raw/f9c676bba12a01e029d727d9771faa38.png)
5. In the pop-up window, expand **Other supported RemoteFx USB devices**, select the inserted USB device, and click **OK**.
![](https://main.qcloudimg.com/raw/681b010102c112bd99309c2c325d53c2.png)
6. Click **Connect**.
7. In the pop-up **Windows Security** window, enter the instance's admin account and password, as shown in the following figure:
![](https://main.qcloudimg.com/raw/f87c5e1240ce07fe0ac28b48d88e61fd.png)
8. Click **OK** to log in to the Windows instance.
If <img src="https://main.qcloudimg.com/raw/73fe2b3cfa740517e44e4596a222840a.png" style="margin: 0;"></img> appears on the Windows instance operation page, the configuration was successful.
![](https://main.qcloudimg.com/raw/af5b70150d4032a29e1ded2db75858b6.png)


## Relevant Operations

Windows RDP provides optimized connection for standard USB devices. Devices such as drivers and cameras can be mapped directly without enabling the RemoteFx feature. The RemoteFX USB redirection feature is required for less commonly used USB devices. The following table lists the redirection methods for these USB devices.
![](https://main.qcloudimg.com/raw/715de06c08753eefe6e4ff5cc3bca270.png)

