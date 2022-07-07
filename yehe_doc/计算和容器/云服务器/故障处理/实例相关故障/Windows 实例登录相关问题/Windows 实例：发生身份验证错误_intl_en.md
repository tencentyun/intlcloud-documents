## Problem Description

When a Remote Desktop Connection is used to log in to a Windows instance, an error is displayed.
- "An authentication error has occurred. The token supplied to the function is invalid"
- "An authentication error has occurred. The function requested is not supported"

## Problem Analysis

Microsoft published a security update in March 2018. By correcting how the Credential Security Support Provider protocol (CredSSP) validates requests during authentication, this update fixes the remote code execution vulnerability in the CredSSP. Both the client and server need to install the security update, or the preceding error may occur.
Remote connection fails in the following three scenarios:

- Scenario 1: The security update is installed on the server but not on the client, and the "force updated clients" policy is configured.
- Scenario 2: The security update is installed on the client but not on the server, and the "force updated clients" policy is configured.
- Scenario 3: The security update is installed on the client but not on the server, and the "mitigated" policy is configured.

## Solution



<dx-alert infotype="explain" title="">
If you only update the client locally, use [Solution 1. Install the security update (recommended)](#step4).
</dx-alert>


### Logging in to CVM via VNC

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, find the target CVM instance and click **Log in**.
![CVM list page](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the **Standard Login | Windows Instance** pop-up window, select **Login via VNC**.
4. In the login pop-up window, select **Send remote command** in the top-left corner and press **Ctrl-Alt-Delete** to open the system login window as shown below:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)
5. Enter the login password and press **Enter** to log in to the Windows CVM instance.


### Solution 1. Install the security update (recommended)[](id:step4)

Install the security update on the unpatched client or server. For updates for different operating systems, see [CVE-2018-0886 | CredSSP remote code execution vulnerability](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886). This solution uses Windows Server 2016 as an example.
In other operating systems, you may use the following methods to enter **Windows Update**:

- Windows Server 2012: <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;width: 22px;"></img> > **Control Panel** > **System and Security** > **Windows Update**
- Windows Server 2008: **Start** > **Control Panel** > **System and Security** > **Windows Update**
- Windows 10: <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;"></img> > **Settings** > **Update & Security**
- Windows 7: <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin:-3px 0px;width: 28px;"></img> > **Control Panel** > **System and Security** > **Windows Update**


1. On the desktop, click <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin:-3px 0px;"></img> and select **Settings**.
2. In the *Settings* pop-up window, select **Update & Security**.
3. In **Update & Security**, select **Windows Update** and click **Check for updates**.
4. Click **Start Installation**.
5. After the installation is complete, restart the instance to finish the update.

### Solution 2. Modify the policy

In a CVM instance that has the security update installed, set the **Encryption Oracle Remediation** policy to **Vulnerable**. This solution uses Windows Server 2016 as an example. Follow the steps below:


<dx-alert infotype="notice" title="">
If no group policy editor is available in the Windows 10 Home operating system, you can modify the registry to edit the policy as instructed in [Solution 3. Modify the registry](#Plan3).
</dx-alert>


1. On the desktop, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin:-3px 0px;"></img>, enter "gpedit.msc", and press **Enter** to open **Local Group Policy Editor**.
<dx-alert infotype="explain" title="">
You can also press **Win+R** to open the **Run** window.
</dx-alert>
2. On the left sidebar, select **Computer Configuration** > **Administrative Templates** > **System** > **Credentials Delegation** and double-click **Encryption Oracle Remediation**.
3. In the **Encryption Oracle Remediation** pop-up window, select **Enabled** and set **Protection level** to **Vulnerable**.
4. Click **OK**.


### Solution 3. Modify the registry[](id:Plan3)

1. On the desktop, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin:-3px 0px;"></img>, enter "regedit", and press **Enter** to open the Registry Editor.
<dx-alert infotype="explain" title="">
You can also press **Win+R** to open the **Run** window.
</dx-alert>
2. On the left sidebar, select **Computer** > **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Microsoft** > **Windows** > **CurrentVersion** > **Policies** > **System** > **CredSSP** > **Parameters**.
<dx-alert infotype="explain" title="">
If the directory path does not exist, create one manually.
</dx-alert>
4. Right-click **Parameters**, select **New** > **DWORD (32-bit) value**, and name the file "AllowEncryptionOracle".
4. Double-click the newly created "AllowEncryptionOracle" file, set **Value data** to "2", and click **OK**.
6. Restart the instance.

## References

- [CVE-2018-0886 | CredSSP remote code execution vulnerability](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [CredSSP updates for CVE-2018-0886](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)

