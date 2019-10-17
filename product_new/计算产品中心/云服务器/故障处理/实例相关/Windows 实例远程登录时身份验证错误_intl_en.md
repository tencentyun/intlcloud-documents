## Problem Description

When trying to log in to a Windows instance via Remote Desktop Connections, you get the message as shown below:
- “An authentication error has occurred. The token supplied to the function is invalid.”

-  “An authentication error has occurred. The function requested is not supported.”


## Problem Analysis

Microsoft published a security update in Mar 2018 which can address a remote code execution vulnerability in Credential Security Supporting Program protocol (CredSSP) by correcting how CredSSP validates requests during the authentication process. Both the client and server need to be updated, or the error described above may occur.

As shown in the figure above, in the following three scenarios, remote connection will fail.
- Scenario 1: The client is unpatched; the server is installed with the security update; the policy setting is “force updated clients”.
- Scenario 2: The server is unpatched; the client is installed with the security update; the policy setting is “force updated clients”.
- Scenario 3: The server is unpatched; the client is installed with the security update; the policy setting is “mitigated”.

## Solution

> If you only need to update the client locally, please directly use [Solution 1: Install the security update (recommended)](#step4).
>
### Log in to the CVM using VNC

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the Instance page, find the CVM and click **Log in** as shown below:

3. In the “Log into Windows Instance” window, select “Alternative login methods (VNC)”, click **Log In Now** to log in to the CVM.
4. In the login window, select “Send CtrlAltDel” in the top left corner, and click **Ctrl-Alt-Delete** to enter the system login interface as shown below:


<span id="step4"></span>
### Solution 1: Install the security update (recommended)

Installing the security update can update the unpatched client/server. For updates for different systems, please refer to [CVE-2018-0886 | CredSSP remote code execution vulnerability](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886). Here we take Windows Server 2016 as an example.
In other operating systems, you may use the following operations to go to **Windows update**:
- Windows Server 2012：<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;"></img> > **Control Panel** > **System and Security** > **Windows Update**
- Windows Server 2008：**Start** > **Control Panel** > **System and Security** > **Windows Update**
- Windows10：<img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img> > **Settings** > **Update and Security**
- Windows 7：<img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 28px;"></img> > **Control Panel** > **System and Security** > **Windows Update**


1. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/6e36af2ceb4604b81de13cb42f30e859.png" style="margin: 0;"></img>, select **Settings** as shown below:

2. In the Settings window, select **Update and Security** as shown below:

3. In the “Update and Security” page, select **Windows Update** and click **Check for updates** as shown below:

4. Click **Install updates**.
5. After the installation is completed, restart the instance to finish the update.

### Solution 2: Modify the policy setting

In a CVM installed with the security update, set the **Encryption Oracle Remediation** policy to "vulnerable”. Here we take Windows Server 2016 as an example. Please follow the steps below:
> In Windows 10 Home operating system, if there is no group policy editor, you can modify the policy setting by modifying the registry. For details, see [Solution 3: Modify the registry](#Plan3).
>
1. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>，enter **gpedit.msc**, and press **Enter** to open the Local Group Policy Editor.
> You can also use the shortcut “Win+R” to open the Run box.
>
3. In the left navigation tree, select **Computer Configuration** > **Administrative Templates** > **System** > **Credentials Delegation**, and double-click **Encryption Oracle Remediation** as shown below:

3. In the “Encryption Oracle Remediation” window, select **Enabled**, and set **Protection Level** to **Vulnerable** as shown below:

4. Click **OK** to complete the configuration.

<span id="Plan3"></span>
###  Solution 3: Modify the registry

1. In the operating system interface, click <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;"></img>, enter **regedit**, and press **Enter** to open the Registry Editor.
> You can also use the shortcut “Win+R” to open the Run box.
> 
2. In the left navigation tree, select **Computer** > **HKEY_LOCAL_MACHINE** > **Software** > **Microsoft** > **Windows** > **CurrentVersion** > **Policies** > **System** > **CredSSP** > **Parameters** as shown below:
> If the directory path does not exist, please create one manually.
>

4. Right-click **Parameters**, select **New** > **DWORD (32-bit) value**, and name the file "AllowEncryptionOracle".
5. Double-click the newly created “AllowEncryptionOracle” file, set “Value data” to “2”, and click **OK** as shown below:

6. Restart the instance.

## Related Documentation

- [CVE-2018-0886 | CredSSP remote code execution vulnerability](https://portal.msrc.microsoft.com/zh-cn/security-guidance/advisory/CVE-2018-0886)
- [CredSSP updates for CVE-2018-0886](https://support.microsoft.com/zh-cn/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)
