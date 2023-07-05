This document describe how to troubleshoot failed or invalid password resets for a Windows Server 2012 CVM.

## Problem

- After the CVM password is reset, the system prompts "The system is busy, and your instance password failed to be reset (7617d94c)."
- After the CVM password is reset, the new password does not take effect, and the login password remains the old one.


## Cause
Possible causes are:
- The `cloudbase-init` component in the CVM is damaged, modified, disabled, or not started.
- The `cloudbase-init` component for password reset is blocked by the third-party security program (e.g., 360 Total Security or Huorong Security) installed on the CVM.


## Troubleshooting

Try the following according to the failure reason.

### Checking the cloudbase-init service

1. [Log in to the target Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. On the desktop, right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"></img> and choose **Run**. Enter **services.msc** in the **Run** dialog box, and press **Enter** to open the **Services** window.
3. Check whether the `cloudbase-init` service exists, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2615f5c0e68a31174c16c9a80884455c.png)
 - If yes, proceed to the next step.
 - If no, reinstall the `cloudbase-init` service. For more information, see [Installing Cloudbase-Init on Windows](https://intl.cloud.tencent.com/document/product/213/32364).
4. Double-click the `cloudbase-init` service to open the cloudbase-init properties dialog box, as shown in the following figure:
![](https://main.qcloudimg.com/raw/10702cb2e359d6de36aec4960771c841.png)
5. Select the **General** tab and check whether the `cloudbase-init` startup type is **Automatic**.
 - If yes, proceed to the next step.
 - If no, set the `cloudbase-init` startup type to **Automatic**.
6. Switch to the **Log On** tab and check whether **Local System account** is selected for the `cloudbase-init` service.
 - If yes, proceed to the next step.
 - If no, select **Local System account** for the `cloudbase-init` service.
7. Switch to the **General** tab, click **Start** in **Service status** to manually enable the `cloudbase-init` service, and check whether an error occurs.
 - If yes, [check the security program installed on the CVM](#CheckSecuritySoftware).
 - If no, proceed to the next step.
8. On the desktop, right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"></img> and choose **Run**. Enter **regedit** in the **Run** dialog box, and press **Enter** to open the **Registry Editor** window.
9. In the registry navigation pane on the left, expand the following hierarchies in order: **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Cloudbase Solutions** > **Cloudbase-Init**.
10. Locate all "LocalScriptsPlugin" registry keys under **ins-xxx** and check whether the LocalScriptsPlugin value is 2.
![](https://main.qcloudimg.com/raw/75580b56e3a28fb9e0559372eb33ff11.png)
 - If yes, proceed to the next step.
 - If no, set the LocalScriptsPlugin value to 2.
11. On the desktop, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"></img> and choose **This PC**. Check whether the CD drive is loaded under **Devices and drives**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8755719fb39bb5f841f4c32897545233.png)
 - If yes, [check the security program installed on the CVM](#CheckSecuritySoftware).
 - If no, start the CD-ROM drive in Device Manager.

<span id="CheckSecuritySoftware"></span>
### Checking the security program installed on the CVM

Scan for CVM vulnerabilities using the installed security program and check whether `cloudbase-init` components are blocked.
- If the CVM has vulnerabilities, fix them.
- If core components are blocked, unblock them.

Check and configure the `cloudbase-init` components as instructed below.
1. [Log in to the target Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. Restore and set the `cloudbase-init` components according to the actually installed third-party security program.




