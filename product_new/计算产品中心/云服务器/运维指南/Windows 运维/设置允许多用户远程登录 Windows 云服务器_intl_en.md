## Scenario
This document shows you how to configure a multi-user remote login to Windows CVM, taking a CVM with Windows Server 2012 R2 as the operating system as an example.

## Steps
### Adding remote desktop service
1. Log in to the Windows CVM.
2. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**, as shown below:
![](https://main.qcloudimg.com/raw/4bdac63da39ed206ef3c3951d6ed5a13.png)
3. Click **Add roles and features**, and the **Add Roles and Features Wizard** window will pop up.
4. In the “Add Roles and Features Wizard” window, keep the default parameters for the first 3 steps.
5. In the **Select server roles** page, check **Remote Desktop Services** and click **Next**, as shown below:
![](https://main.qcloudimg.com/raw/a395eee56ec77e729faf8b6d3217566d.png)
6. Keep the default parameters and click **Next** two times in a row.
7. In the **Select role service** interface, check **Remote Desktop Session Host**, as shown below:
The “Add features that are required for Remote Desktop Session Host?” prompt box will pop up.
![](https://main.qcloudimg.com/raw/cabbd6cc5a22558e088c26be458f5421.png)
8. In the “Add features required for Remote Desktop Session Host?” prompt box, click **Add Features**, as shown below:
![](https://main.qcloudimg.com/raw/d21de386096c36baa0a4382f4d8f59e1.png)
9. In the **Select role service** page, check **Remote Desktop Licensing**, as shown below:
The “Add features that required for Remote Desktop Licensing?” prompt box will pop up.
![](https://main.qcloudimg.com/raw/c37cbd9d47b521f36ab42a4179357a22.png)
10. In the “Add features that required for Remote Desktop Licensing?” prompt box, click **Add Features**.
![](https://main.qcloudimg.com/raw/f10d21c2f28d5f49841b4aac656b9efa.png)
11. Click **Next**.
12. Check **Restart the destination server automatically if required**, and click **Yes** in the pop-up prompt box, as shown below:
![](https://main.qcloudimg.com/raw/05a63b7593c57573a5c19b03ae4cd4a5.png)
13. Click **Install** and wait for the remote desktop service installation to complete.

### Configuring multi-user remote login to instance
1. Use VNC to log in to Windows CVM.
2. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> to open the Windows PowerShell window.
3. In the Windows PowerShell window, enter **gpedit.msc** and press **Enter** to open the **Local Group Policy Editor**.
4. In the left navigation tree, select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Connections**, and double click **Limit number of connections**, as shown below:
![](https://main.qcloudimg.com/raw/5db10d892563f1492584f98ed550d67c.png)
5. In the **Limit number of connections** window that pops up, select **Enabled**, and enter the maximum number of simultaneous remote users in **RD Maximum Connections allowed**, as shown below:
![](https://main.qcloudimg.com/raw/72b16384df297cbaae5619d841e4369f.png)
6. Click **OK**.
4. In the left navigation tree, select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Connections**, and double click **Restrict Remote Desktop Services users to a single Remote Desktop Services session**, as shown below:
![](https://main.qcloudimg.com/raw/ef6170f145555e4156d83653e75f29d1.png)
8. In the “Restrict Remote Desktop Services users to a single Remote Desktop Services session” window that pops up, select **Disabled**, and click **OK**, as shown below:
![](https://main.qcloudimg.com/raw/cdfe7762d6248da40cbf3e876edc8dfa.png)
9. Close local group policy editor.
10. Restart the instance.



