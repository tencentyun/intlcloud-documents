This document uses Windows Server 2012 as an example to describe how to troubleshoot CVM password reset failure or ineffectiveness.

## Symptoms

- After the CVM password is reset, the system prompts "The system is busy, and the password of your instance failed to be reset (7617d94c)."
- After the CVM password is reset, the new password does not take effect, and the login password is still the old password.


## Possible Causes
Possible causes to both issues are:
- The Cloudbase-Init component in the CVM is damaged, modified, forbidden, or disabled.
- The security software program, such as 360 antivirus installed on the CVM, intercepts related system process components.


## Troubleshooting

Based on the possible causes, use these inspection methods:

### Checking the Cloudbase-Init service

1. [Log in to the Windows instance by using VNC](https://intl.cloud.tencent.com/document/product/213/32496).
2. On the desktop, right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> and choose **Run**. In the **Run** dialog box, enter **services.msc** and press Enter to open the "Services" window.
3. Check whether the cloudbase-init service exists, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2615f5c0e68a31174c16c9a80884455c.png)
 - If yes, proceed to the next step.
 - If no, reinstall the cloudbase-init service. For more information, see [Installing Cloudbase-Init on Windows](https://intl.cloud.tencent.com/document/product/213/32364).
4. Double-click the cloudbase-init service to open the cloudbase-init property dialog box, as shown in the following figure:
![](https://main.qcloudimg.com/raw/10702cb2e359d6de36aec4960771c841.png)
5. On the **General** tab page, check whether the cloudbase-init startup type is **Automatic**.
 - If yes, proceed to the next step.
 - If no, set the cloudbase-init startup type to **Automatic**.
6. Switch to the **Log On** tab page and check whether **Local System account** is selected for the cloudbase-init service.
 - If yes, proceed to the next step.
 - If no, select **Local System account** for the cloudbase-init service.
7. Switch to the **General** tab page, click **Start** in the **Service status** area to manually enable the cloudbase-init service, and check whether an error appears.
 - If yes, [check the security software program installed on the CVM](#CheckSecuritySoftware).
 - If no, proceed to the next step.
8. On the desktop, right-click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> and choose **Run**. In the **Run** dialog box, enter **regedit** and press Enter to open the "Registry Editor" window.
9. In the leftside navigation tree, choose **HKEY_LOCAL_MACHINE** > **SOFTWARE** > **Cloudbase Solutions** > **Cloudbase-Init**.
10. Locate all "LocalScriptsPlugin" registry keys and check whether the LocalScriptsPlugin value is 2.
![](https://main.qcloudimg.com/raw/75580b56e3a28fb9e0559372eb33ff11.png)
 - If yes, proceed to the next step.
 - If no, set the LocalScriptsPlugin value to 2.
11. On the desktop, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> and choose **This PC**. Check whether the CD driver is loaded under **Devices and drivers**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/8755719fb39bb5f841f4c32897545233.png)
 - If yes, [check the security software program installed on the CVM](#CheckSecuritySoftware).
 - If no, start the CD-ROM driver in Device Manager.

<span id="CheckSecuritySoftware"></span>
### Checking the security software program installed on the CVM

Scan for vulnerabilities in the CVM by using the installed security software program and check whether Cloudbase-Init core components are intercepted.
- If the CVM has vulnerabilities, fix them.
- If core components are intercepted, unblock them.

To prevent CVM password reset failure or ineffectiveness, we recommend that you add the following directories and files to the whitelist and trusted file area in the security software program.
- Add the following directories to the whitelist of the security software program:
```
C:\Windows\System32\WindowsPowerShell\
C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Scripts
C:\Program Files\QCloud
C:\Program Files\Cloudbase Solutions\
```
- Add the following files to the trusted file area:
```
C:\Windows\System32\cmd.exe
C:\Windows\SysWOW64\cmd.exe
```





