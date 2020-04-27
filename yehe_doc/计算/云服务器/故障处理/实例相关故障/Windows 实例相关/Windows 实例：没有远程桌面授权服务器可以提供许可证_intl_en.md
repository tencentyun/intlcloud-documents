This document describes how to manage alarm prompts such as "Remote session has been disconnected as no remote desktop authorization server is available for licensing" when you try to remotely connect to a Windows instance.

## Problem

When you try to connect to a Windows instance by using Windows Remote Desktop, a prompt stating "Remote session has been disconnected as no remote desktop authorization server is available for licensing. For assistance, please contact your system administrator" appears, as shown in the following figure:
![](https://main.qcloudimg.com/raw/0034f9d4e822ca556bd54dafb9b13c17.png)

## Problem Analysis

The possible causes to this problem include but are not limited to the following. Therefore, always analyze the problem based on the actual situation.
- The RDP-TCP limit is set by the system by default, and it allows only one session for each user. If the account has been logged in, no additional sessions can be established.
- The "Remote Desktop Session Host" role feature was added by the system, but the validity period of the feature has expired.
The "Remote Desktop Session Host" role feature is free for use for 120 days. After the period, you must pay for the feature to continue to use it.

## Solution
### Logging in to the CVM through VNC

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, locate the target CVM instance and click **Log In**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the **Log in to Windows instance** window that appears, select **Alternative login methods (VNC)**, and click **Log In Now** to log in to the CVM.
4. In the login window that appears, select **Send Remote Command** in the upper-left corner, and press **Ctrl-Alt-Delete** to go to the system login interface, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Solution 1: Modify the policy configuration
1. On the operating system interface, click <img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png" style="margin: 0;"></img> to open a Windows PowerShell window.
2. In the Windows PowerShell window, enter **gpedit.msc** and press **Enter** to open **Local Group Policy Editor**.
3. In the left navigation tree, choose **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Remote Desktop Services** > **Remote Desktop Session Host** > **Connections**, and double-click **Limit number of connections**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/e0420d2bb8ddd3e1524ee688173cb9d1.png)
4. In the "Limit number of connections" window that appears, modify **Maximum RD connections supported** and click **OK**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/066c9dfb06dc4c092424c4e1142f7471.png)
5. Switch to the Windows PowerShell window.
6. In the Windows PowerShell window, enter **gpupdate** and press **Enter** to update the policy.


### Solution 2: Delete the "Remote Desk Session Host" role
> If you want to keep the "Remote Desktop Session Host" role, skip this step and go to the [Microsoft official website](https://www.microsoft.com/) to purchase and configure the appropriate certificate.
>
1. On the operating system interface, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"> to open **Server Manager**.
2. Click **Manage** in the upper-right corner of the "Server Manager" window and select **Delete roles and features**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/373ef0a31c2b8e8fd1539e29852c4fab.png)
3. In the "Delete roles and features" wizard, click **Next**.
4. On the "Delete server roles" page, uncheck **Remote Desktop Services**. In the prompt box that appears, select **Remove Feature**.
6. Click **Next** twice.
6. Check **Restart the destination server automatically if required**, and click **Yes** in the prompt box that appears.
8. Click **Delete**.
Wait for the CVM to restart.






