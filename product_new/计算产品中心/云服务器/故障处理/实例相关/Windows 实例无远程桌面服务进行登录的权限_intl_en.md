## Problem Description

When trying to connect to a Windows instance via Remote Desktop from Windows, you get the message as shown below:
![Error Message](https://main.qcloudimg.com/raw/52a79c81015d7e6b2f5299f98474348d.png)
To sign in remotely, you need the right to sign in through Remote Desktop Services. By default members of the Remote Desktop Users group have this right. If the group you’re in doesn’t have the right, or if the right has been removed from the Remote Desktop Users group, you need to be granted the right manually.

## Solution

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the Instance page, find the CVM instance which you failed to connect and click **Log in** as shown below:
![CVM list page](https://main.qcloudimg.com/raw/56596196a93181ac4c9467abe19c383a.png)
3. In the “Log into Windows CVM” window, select “Alternative login methods (VNC)”,  click **Log In Now** as shown below:
![VNC login](https://main.qcloudimg.com/raw/80b613a90328bb34a006d5988dcff18b.png)
4. In the login window, select “Send CtrlAltDel” in the top left corner, and click **Ctrl-Alt-Delete** to enter the system login interface as shown below:
![Ctrl-Alt-Delete](https://main.qcloudimg.com/raw/27daf8cc33746b195c74dfb5066addee.png)
5. In the operating system interface, use “win+r” to open the Run box and enter **gpedit.msc**.
6. Press **Enter** to open the Local Group Policy Editor.
7. In the left navigation tree, choose **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment** as shown below:
![Deny logon through Remote Desktop Services](https://main.qcloudimg.com/raw/55937ed371582903a7235b56aa0a38f1.png)
5. In the policy list on the right, double-click **Deny logon through Remote Desktop Services** and select **Properties**.
6. In the Properties window, check whether the account you want to use for remote login is on the user list of “Deny logon through Remote Desktop Services”.
 - If it is, please remove the account from the list.
 - If it is not, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).

