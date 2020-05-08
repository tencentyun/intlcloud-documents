## Problems

<span id="FaultPhenomenon1"></span>
### Problem 1
When trying to connect to a Windows instance by using Windows Remote Desktop, you are prompted with the message stating "The connection was denied because the user account is not authorized for remote login."

<span id="FaultPhenomenon2"></span>
### Problem 2
When trying to connect to a Windows instance by using Windows Remote Desktop, you are prompted with the message stating "To sign in remotely, you need the permission to sign in through Remote Desktop Services. By default members of the Remote Desktop Users group have this permission. If the group you’re in doesn’t have the permission, or if the permission has been removed from the Remote Desktop Users group, you need to be granted the permission manually."

## Problem Analysis

The user is not allowed to log in to the Windows instance through Remote Desktop connections:

## Solution
- If you encounter [problem 1](#FaultPhenomenon1) when trying to connect to a Windows instance through Remote Desktop, you need to add the user account to the list of accounts that are permitted by the Windows instance to log in through Remote Desktop Services. For details, see [Configuring the permission that allows remote login](#ConfigurationToAllowAccess).
- If you encounter [problem 2](#FaultPhenomenon2) when trying to connect to a Windows instance through Remote Desktop, you need to remove the user account from the list of accounts that are denied by the Windows instance to log in through Remote Desktop Services. For details, see [Configuring the permission that denies remote login](#ModifyLoginAuthority).

## Directions

### Logging in to the CVM by using VNC
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, find the target CVM and click **Log In**, as shown in the following figure:
![CVM list page](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the "Log In to Windows Instance" window, select "Alternative login methods (VNC)" and click **Log In Now** to log in to the CVM.
4. In the login window that appears, select **Send Ctrl-Alt-Delete** in the upper-left corner, and click **Ctrl-Alt-Delete** to enter the system login interface, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

<span id="ConfigurationToAllowAccess"></span>
### Configuring the permission that allows remote login

> The following operations take Windows Server 2016 as an example.
>
1. On the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, enter **gpedit.msc**, and press Enter to open "Local Group Policy Editor".
2. In the left navigation tree, choose **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**, and double-click **Allow log in through Remote Desktop Services**.
3. In the "Allow log on through Remote Desktop Services Properties" window, check whether the user account you want to use for remote login is in the user list of "Allow log in through Remote Desktop Services".
 - If the user is not in the list, perform [step 4](#step04).
 - If the user is in the list, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
4. <span id="step04">Click **Add User or Group** to go to the "Select User or Group" window.</span>
5. Enter the account that you want to use for remote login and click **OK**.
6. Click **OK** and close Local Group Policy Editor.
7. Restart the instance and try to connect to the Windows instance with the account through Remote Desktop again.

<span id="ModifyLoginAuthority"></span>
### Configuring the permission that denies remote login

> The following operations take Windows Server 2016 as an example.
>
1. On the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, enter **gpedit.msc**, and press Enter to open "Local Group Policy Editor".
2. In the left navigation tree, choose **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**, and double-click **Deny log in through Remote Desktop Services**.
3. In the "Properties" window, check whether the account you want to use for remote login is in the user list of "Deny log in through Remote Desktop Services".
 - If the user is in the list, remove the user account from the list and restart the instance.
 - If the user is not in the list, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
