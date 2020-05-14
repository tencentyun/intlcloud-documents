## Scenario
To join an instance to a domain and log in to Windows CVM with the domain account, you need to run Sysprep to ensure its unique SID in the domain before creating a custom image. Otherwise, the instance cannot be joined to the domain because the CVM created with the custom image and the original instance contain some identical information, such as same SID. Skip this operation if you have no need to join your Windows CVM to a domain.

This document describes how to run Sysprep on the Windows Server 2012 R2 64-bit operating system to ensure that each Windows CVM in the domain has unique SID.

For further information of Sysprep, see `https://technet.microsoft.com/zh-cn/library/cc721940(v=ws.10).aspx`


## Notes

- Windows CVM must be an active genuine Windows operating system.
- If your Windows CVM is created with a non-public image, you must always run the Sysprep version provided in the original image under directory `%WINDIR%\system32\sysprep`.
- The remaining Windows reset counts must be greater than 1, otherwise Sysprep cannot be encapsulated.
To check the remaining Windows reset counts, execute the command `slmgr.vbs /dlv`.
- As a built-in account of the agent program Cloudbase-Init, the account Cloudbase-Init of the Windows CVM is used to get metadata and perform configurations when the CVM instance is launched. If you change or delete this account or unmount the agent program Cloudbase-Init, the custom information might be lost when you initialize a CVM generated based on the custom image created from the CVM. Therefore, do not change or delete the account Cloudbase-init.  

## Prerequisites

1. [Logged in to Windows CVM](https://intl.cloud.tencent.com/document/product/213/5435) as Administrator.
- [Installed Cloudbase-Init on Windows CVM](https://intl.cloud.tencent.com/document/product/213/32364).

## Directions

1. On the desktop, click<img src="https://main.qcloudimg.com/raw/f0c84862ef30956c201c3e7c85a26eec.png"></img> to open a Windows PowerShell window.
2. Execute the following command in the Windows PowerShell window to go to the installation directory of the Cloudbase-init tool.
> Assume that Cloudbase-init is installed under `C:\Program Files\Cloudbase Solutions\`.
>
```
cd 'C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf'
```
3. Execute the following command to encapsulate the Windows system.
> 
> - Include `/unattend:Unattend.xml` in the following command, otherwise your current username, password and other important configurations of the CVM will be reset. If you choose **Follow image** for the login, you need to manually reset the username and account of the CVM launched.
> - After the following command is executed, CVM automatically shuts down. To ensure that each CVM later created with the image, has a unique SID, do not launch the CVM instance before creating a custom image. Otherwise, the command is only effective to the current CVM.  
> - After you execute the following command on the Windows Server 2012 or Windows Server 2012 R2 operating system, the account Administrator and its password of the CVM will be cleared. Therefore, reset and save your account and password after restarting the CVM, as detailed in [Reset Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
> 
```
C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /unattend:Unattend.xml
```
4. Create a custom image for the CVM instance on which Sysprep has been executed, and start new CVM instances with the image. See [Create Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
In this way, each new CVM instance has a unique SID after you join them to the domain.
> To check CVM SID, execute the command `whoami /user`.
>


