## Problem Description

<span id="FaultPhenomenon1"></span>
### Problem 1
When trying to connect to a Windows instance via Remote Desktop from Windows, you get the following message: “The connection was denied because the user account is not authorized for remote login.”


<span id="FaultPhenomenon2"></span>
### Problem 2
When trying to connect to a Windows instance via Remote Desktop from Windows, you get the following message: “To sign in remotely, you need the right to sign in through Remote Desktop Services. By default members of the Remote Desktop Users group have this right. If the group you’re in doesn’t have the right, or if the right has been removed from the Remote Desktop Users group, you need to be granted the right manually.”


## Problem Analysis

The user is not allowed to log in to the Windows instance via Remote Desktop Connections:

## Solution
- If you encounter the [problem 1](#FaultPhenomenon1) when trying to connect to a Windows instance through Remote Desktop, you will need to add the user account to the list of accounts that are allowed by the Windows instance to log in through Remote Desktop Services. For details, see [Configuring the right that allows remote login](#ConfigurationToAllowAccess).
- If you encounter the [problem 2](#FaultPhenomenon2) trying to connect to a Windows instance through Remote Desktop, you will need to remove the user account from the list of accounts that are denied by the Windows instance to log in through Remote Desktop Services.. For details, see [Configuring the right that denies remote login](#ModifyLoginAuthority).

## Directions

### Logging in to the CVM using VNC
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the Instance page, find the CVM and click **Log in** as shown below:

3. In the “Log into Windows Instance” window, select “Alternative login methods (VNC)”, click **Log In Now** to log in to the CVM.
4. In the login window, select “Send CtrlAltDel” in the top left corner, and click **Ctrl-Alt-Delete** to enter the system login interface as shown below:


<span id="ConfigurationToAllowAccess"></span>
### Configuring the right that allows remote login

>? The following operations take Windows Server 2016 as an example.
>
1. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, enter **gpedit.msc**, and press **Enter** to open the Local Group Policy Editor.
2. In the left navigation tree, choose **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**, and right-click **Allow log on through Remote Desktop Services** as shown below:

3. In the **Allow log on through Remote Desktop Services Properties** window, check whether the user account you want to use for remote login is on the user list of “Allow log on through Remote Desktop Services” as shown below:

 - If the user is not on the list, please take [Step 4](#step04)。
 - If the user is on the list, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
4. <span id="step04">Click **Add User or Group** to open the "Select User or Group" window. </span>
5. Enter the account you want to use for remote login and click **OK**.
6. Click **OK** and close the Local Group Policy Editor.
7. Restart the instance and try again to connect to the Windows instance with the account through Remote Desktop.

<span id="ModifyLoginAuthority"></span>
### Configuring the right that denies remote login

>? The following operations take Windows Server 2016 as an example.
>
1. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, enter **gpedit.msc**, and press **Enter** to open the Local Group Policy Editor.
2. In the left navigation tree, choose **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**, and double-click **Deny log on through Remote Desktop Services** as shown below:

3. In the **Deny log on through Remote Desktop Services Properties** window, check whether the user account you want to use for remote login is on the user list of “Deny log on through Remote Desktop Services”.
 - If the user is on the list, remove the user account from the list and restart the instance.
 - If the user is not on the list, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
