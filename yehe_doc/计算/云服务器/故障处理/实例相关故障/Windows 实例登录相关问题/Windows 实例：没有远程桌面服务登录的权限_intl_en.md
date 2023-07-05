## Error Description

<span id="FaultPhenomenon1"> </span>
**Case 1**: When trying to connect to a Windows instance via Remote Desktop from Windows, the user sees an error that says **The connection was denied because the user account is not authorized for remote login.**

<span id="FaultPhenomenon2"> </span>
**Case 2**: When trying to connect to a Windows instance via Windows Remote Desktop, the user sees an error that says **To sign in remotely, you need the right to sign in through Remote Desktop Services. By default, members of the Remote Desktop Users group have this right. If the group you’re in doesn’t have the right, or if the right has been removed from the Remote Desktop Users group, you need to be granted the right manually.**

## Possible Reasons

The user is not allowed to log in to the Windows instance via Remote Desktop connections.

## Solution
- For [Case 1](#FaultPhenomenon1), add the user account to the list of accounts that are permitted by the Windows instance to log in through Remote Desktop Services. For detailed directions, see [Allowing remote login](#ConfigurationToAllowAccess).
- For [Case 2](#FaultPhenomenon2), remove the user account from the list of accounts that are denied by the Windows instance to log in through Remote Desktop Services. For detailed directions, see [Denying remote login](#ModifyLoginAuthority).

## Directions

### Logging in to the CVM using VNC
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, locate the target CVM instance and click **Log In**, as shown in the following figure:
![CVM list page](https://main.qcloudimg.com/raw/bd24015a7332c824e649c034417f708d.png)
3. In the **Log in to Windows Instance** window that appears, select “Alternative login methods (VNC)”, click **Log In Now** to log in to the CVM.
4. In the login window that appears, select **Send CtrlAltDel** in the upper-left corner, and press **Ctrl-Alt-Delete** to open the system login window, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)


<span id="ConfigurationToAllowAccess"> </span>
### Allowing remote login

>? The following operations take Windows Server 2016 as an example.
>
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, enter **gpedit.msc**, and press **Enter** to open “Local Group Policy Editor”.
2. In the left navigation tree, choose **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**, and right-click **Allow log on through Remote Desktop Services**.
![](https://main.qcloudimg.com/raw/69a452fc83bb2d9013c1830ae67996ac.png)
3. In the “Allow log on through Remote Desktop Services Properties” window that appears, check whether the user account you want to use for remote login is in the user list of “Allow log on through Remote Desktop Services”.
![Allow log on through Remote Desktop Services](https://main.qcloudimg.com/raw/a3d28bd18e13fe2c0ce1fceb850a3284.png)
 - If the user is not in the list, go to [step 4](#step04).
 - If the user is in the list, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).
4. <span id="step04">Click **Add User or Group** to go to the **Select User or Group** window.</span>
5. Enter the account you want to use for remote login and click **OK**.
6. Click **OK** and close “Local Group Policy Editor”.
7. Restart the instance and try to connect to the Windows instance with the account through Remote Desktop again.


<span id="ModifyLoginAuthority"> </span>
### Denying remote login

>? The following operations take Windows Server 2016 as an example.
>
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">, enter **gpedit.msc**, and press **Enter** to open “Local Group Policy Editor”.
2. In the left navigation tree, choose **Computer Configuration** > **Windows Settings** > **Security Settings** > **Local Policies** > **User Rights Assignment**, and double-click **Deny log on through Remote Desktop Services** as shown below:
![Deny log on through Remote Desktop Services](https://main.qcloudimg.com/raw/4c4d47a70c0d55e9c7de1f9351f4b0ab.png)
3. In the pop-up window, check whether the account you want to use for remote login is in the user list of "Deny log in through Remote Desktop Services".
 - If the user is in the list, remove the user account from the list and restart the instance.
 - If the user is not in the list, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2).

 

