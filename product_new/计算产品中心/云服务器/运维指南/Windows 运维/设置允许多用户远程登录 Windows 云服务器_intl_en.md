## Scenario
This document shows you how to configure a multi-user remote login to Windows CVM, taking a CVM with Windows Server 2012 R2 as the operating system as an example.

## Steps
### Adding remote desktop service
1. Log in to the Windows CVM.
2. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**, as shown below:
![](https://main.qcloudimg.com/raw/66bb5237846f1dd79e3145bfd82d9257.png)
3. Click **Add roles and features**, and the **Add Roles and Features Wizard** window will pop up.
4. In the “Add Roles and Features Wizard” window, keep the default parameters for the first 3 steps.
5. In the **Select server roles** page, check **Remote Desktop Services** and click **Next**, as shown below: 
![](https://main.qcloudimg.com/raw/54d329c2667ac5c60ffdc2b74f1fc555.png)
6. Keep the default parameters and click **Next** two times in a row.
7. In the **Select Role Service** interface, check **Remote Desktop Session Host**, as shown below:
The “Add features that are required for remote desktop session host?” prompt box will pop up.
![](https://main.qcloudimg.com/raw/8d24fd515bd363dc020257c2843c5562.png)
8. In the “Add features required for remote desktop session host?” prompt box, click **Add Features**, as shown below: 
![](https://main.qcloudimg.com/raw/2a33d896c16b1d98012536cdc3776248.png)
9. In the **Select Role Service** page, check **Remote Desktop Licensing**, as shown below:
The “Add features that required for Remote Desktop Licensing?” prompt box will pop up.
![](https://main.qcloudimg.com/raw/1c908dc77f50488387a2fdbfda08ba35.png)
10. In the “Add features that required for Remote Desktop Licensing?” prompt box, click **Add Features**.
![](https://main.qcloudimg.com/raw/d7aa066366b168ac8a7475155d34ea19.png)
11. Click **Next**.
12. Check **Restart the destination server automatically if required**, and click **Yes** in the pop-up prompt box, as shown below:
![](https://main.qcloudimg.com/raw/05a63b7593c57573a5c19b03ae4cd4a5.png)
13. Click **Install** and wait for the remote desktop service installation to complete.

### Configuring multi-user remote login to instance
1. Use VNC to log in to Windows CVM.
2. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> to open the Windows PowerShell window.
3. In the Windows PowerShell window, enter **gpedit.msc** and press **Enter** to open the **Local Group Policy Editor**.
4. In the left navigation tree, select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Connections**, and double click **Limit number of connections**, as shown below:
![](https://main.qcloudimg.com/raw/e0420d2bb8ddd3e1524ee688173cb9d1.png)
5. In the **Limit number of connections** window that pops up, select **Enabled**, and enter the maximum number of simultaneous remote users in **RD Maximum Connections allowed**, as shown below:
![](https://main.qcloudimg.com/raw/066c9dfb06dc4c092424c4e1142f7471.png)
6. Click **OK**.
4. In the left navigation tree, select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Connections**, and double click **Restrict Remote Desktop Services users to a single Remote Desktop Services session**, as shown below:
![](https://main.qcloudimg.com/raw/1183e9f4c6c08b6f99746db42b0d183e.png)
8. In the “Restrict Remote Desktop Services users to a single Remote Desktop Services session” window that pops up, select **Disabled**, and click **OK**, as shown below:
![](https://main.qcloudimg.com/raw/56d910ea359024d34dc05de3a274c91a.png)
9. Close local group policy editor.
10. Restart the instance.



