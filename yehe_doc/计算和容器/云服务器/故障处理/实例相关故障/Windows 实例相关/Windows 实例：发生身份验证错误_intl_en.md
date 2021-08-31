## Problem Description

When users try to log in to a Windows instance through a Remote Desktop Connection, an error occurs.
- The error message states "Authentication error. The token supplied to the function is invalid.".
- "Authentication error. The requested function is not supported.".

## Problem Analysis

Microsoft published a security update in March 2018. By correcting how the Credential Security Support Provider protocol (CredSSP) validates requests during authentication, this update fixes the remote code execution vulnerability in the CredSSP. Both the client and server need to install the security update, or the preceding error may occur.
Remote connection fails in the following conditions:

- Condition 1: the security update is installed on the server but not on the client, and the "force updated clients" policy is configured.
- Condition 2: the security update is installed on the client but not on the server, and the "force updated clients" policy is configured.
- Condition 3: the security update is installed on the client but not on the server, and the "mitigated" policy is configured.

## Solution

> If you only need to upgrade the client locally, use [Solution 1: Install the security update (recommended)](#step4).
>
### Logging in to the CVM by using VNC

1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, find the target CVM instance and click **Log In**.
3. In the **Log in to Windows instance** window that appears, select **Alternative login methods (VNC)** and click **Log In Now**.
4. In the login window that appears, select **Send CtrlAltDel** in the upper-left corner and click **Ctrl-Alt-Delete** to go to the system login page.

<span id="step4"></span>
### Solution 1: Install the security update (recommended)

Install the security update on the unpatched client or server. For updates for different operating systems, see [CVE-2018-0886 | CredSSP remote code execution vulnerability](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886). This solution uses Windows Server 2016 as an example.
In other operating systems, you can use the following methods to go to **Windows Update**.
- Windows Server 2012: <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;"></img> > **Control Panel** > **System and Security** > **Windows Update**
- Windows Server 2008: **Start** > **Control Panel** > **System and Security** > **Windows Update**
- Windows 10: <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> > **Settings** > **Update and Security**
- Windows 7: <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 28px;"></img> > **Control Panel** > **System and Security** > **Windows Update**


1. On the desktop, click <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> and choose **Settings**.
2. In the **Settings** window, choose **Update and Security**.
3. On the **Update and Security** page, choose **Windows Update** and click **Check for updates**.
4. Click **Install updates**.
5. After the installation is completed, restart the instance to finish the update.

### Solution 2: Modify the policy

In a CVM with the security update installed, set the **Encryption Oracle Remediation** policy to **vulnerable**. This solution uses Windows Server 2016 as an example. Complete the following steps:
> If no group policy editor is available in the Windows 10 Home operating system, you can modify the policy in the registry. For details, see [Solution 3: Modify the registry](#Plan3).
>
1. On the desktop, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, enter **gpedit.msc**, and press **Enter** to open "Local Group Policy Editor".
> You can also press **Win+R** to open the **Run** dialog box.
>
3. In the left-side navigation tree, choose **Computer Configuration** > **Administrative Templates** > **System** > **Credentials Delegation** and double-click **Encryption Oracle Remediation**.
4. In the **Encryption Oracle Remediation** window, select **Enabled** and set **Protection Level** to **Vulnerable**.
5. Click **OK** to finish the configuration.

<span id="Plan3"></span>
### Solution 3: Modify the registry

1. On the desktop, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, enter **regedit**, and press **Enter** to open "Registry Editor".
> You can also press **Win+R** to open the **Run** dialog box.
> 
2. In the left-side navigation tree, choose **Computer** > **HKEY_LOCAL_MACHINE** > **Software** > **Microsoft** > **Windows** > **CurrentVersion** > **Policies** > **System** > **CredSSP** > **Parameters**.
> If this path does not exist, create one manually.
>
4. Right-click **Parameters**, choose **New** > **DWORD (32-bit) value**, and name the file "AllowEncryptionOracle".
5. Double-click the newly created "AllowEncryptionOracle" file, set "Value data" to "2", and click **OK**.
6. Restart the instance.

## Related Documents

- [CVE-2018-0886 | CredSSP remote code execution vulnerability](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [CredSSP updates for CVE-2018-0886](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)
