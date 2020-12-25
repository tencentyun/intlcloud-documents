This document uses Windows Server 2012 as an example to describe how to troubleshoot failed or invalid CVM password resets.

## Problems

- After the CVM password is reset, the system prompts "The system is busy, and your instance password failed to be reset (7617d94c)."
- After the CVM password is reset, the new password does not take effect, and the login password remains the old one.


## Possible Causes
Possible causes are:
- The Cloudbase-Init component in the CVM is damaged, modified, disabled, or not launched.
- The components of a system process are blocked by the security program (e.g., 360 Safeguard) installed on the CVM.


## Troubleshooting

Based on possible causes, troubleshoot as follows

### Checking the Cloudbase-Init service

1. [Log in to the Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. On the desktop, right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> and choose **Run**. Enter **services.msc** in the **Run** dialog box, and press **Enter** to open the **Services** window.
3. Check whether the cloudbase-init service exists, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2615f5c0e68a31174c16c9a80884455c.png)
 - If yes, proceed to the next step.
 - If no, reinstall the cloudbase-init service. For more information, see [Installing Cloudbase-Init on Windows](https://intl.cloud.tencent.com/document/product/213/32364).
4. Double-click the cloudbase-init service to open the cloudbase-init properties dialog box, as shown in the following figure:
![](https://main.qcloudimg.com/raw/10702cb2e359d6de36aec4960771c841.png)
5. Select the **General** tab and check whether the cloudbase-init startup type is **Automatic**.
 - If yes, proceed to the next step.
 - If no, set the cloudbase-init startup type to **Automatic**.
6. Switch to the **Log On** tab and check whether **Local System account** is selected for the cloudbase-init service.
 - If yes, proceed to the next step.
 - If no, select **Local System account** for the cloudbase-init service.
7. Switch to the **General** tab, click **Start** in **Service status** to manually enable the cloudbase-init service, and check whether an error occurs.
 - If yes, [check the security program installed on the CVM](#CheckSecuritySoftware).
 - If no, proceed to the next step.
8. On the desktop, right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> and choose **Run**. Enter **regedit** in the **Run** dialog box, and press **Enter** to open the **Registry Editor** window.
9. In the registry navigation pane on the left, expand the following hierarchies in order: **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Cloudbase Solutions** > **Cloudbase-Init**.
10. Locate all "LocalScriptsPlugin" registry keys under **ins-xxx** and check whether the LocalScriptsPlugin value is 2.
![](https://main.qcloudimg.com/raw/75580b56e3a28fb9e0559372eb33ff11.png)
 - If yes, proceed to the next step.
 - If no, set the LocalScriptsPlugin value to 2.
11. On the desktop, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> and choose **This PC**. Check whether the CD driver is loaded under **Devices and drives**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8755719fb39bb5f841f4c32897545233.png)
 - If yes, [check the security program installed on the CVM](#CheckSecuritySoftware).
 - If no, launch the CD-ROM driver in Device Manager.

<span id="CheckSecuritySoftware"></span>
### Checking the security program installed on the CVM

Scan for CVM vulnerabilities using the installed security program and check whether Cloudbase-Init components are blocked.
- If the CVM has vulnerabilities, fix them.
- If core components are blocked, unblock them.

To prevent failed or invalid CVM password resets, we recommend adding the following directories and files to the allowlist and trusted locations of the security program.
- Allowlist the following directories in the security program:
```
C:\Windows\System32\WindowsPowerShell\
C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Scripts
C:\Program Files\QCloud
C:\Program Files\Cloudbase Solutions\
```
- Add the following files to trusted locations:
```
C:\Windows\System32\cmd.exe
C:\Windows\SysWOW64\cmd.exe
```

