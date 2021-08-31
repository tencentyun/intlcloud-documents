## Overview
To join an instance to a domain and log in to Windows CVM with the domain account, you need to run Sysprep before creating a custom image to ensure the SID will be unique. Otherwise, the instance cannot be joined to the domain because the CVM created with the custom image and the original instance contains identical information, such as duplicate SIDs. Skip this operation if you have no need to join your Windows CVM to a domain.

This document describes how to run Sysprep on the Windows Server 2012 R2 64-bit operating system to ensure that the Windows CVMs in the domain have unique SIDs.

For more information about Sysprep, see `https://technet.microsoft.com/zh-cn/library/cc721940(v=ws.10).aspx`


## Notes

- Windows CVM must be an active genuine Windows operating system.
- If your Windows CVM is created with a non-public image, you must always run the Sysprep version provided in the original image under directory `%WINDIR%\system32\sysprep`.
- The remaining Windows reset counts must be greater than 1, otherwise Sysprep cannot be encapsulated.
To check the remaining Windows reset counts, execute the command `slmgr.vbs /dlv`.
- The Cloudbase-Init account takes care of the initialization actions when a CVM instance is launched. If you change/delete this account or uninstall Couldbase-Init, you might lose custom information when you provision a new CVM from a custom image. Thus, we do not recommend modifying or deleting the Cloudbase-init account.   

## Prerequisites

1. [Log in to Windows CVM](https://intl.cloud.tencent.com/document/product/213/5435) as Administrator.
- [Install Cloudbase-Init on Windows CVM](https://intl.cloud.tencent.com/document/product/213/32364).

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
> - Include `/unattend:Unattend.xml` in the following command, otherwise your current username, password and other configurations of the CVM will be reset. If you choose **Follow image** for the login, you will need to manually reset the username and account after launch.
> - After the following command is executed, CVM automatically shuts down. To ensure that the CVMs created from this image has unique SIDs, do not launch the CVM instance before creating a custom image, or this action will only be effective for the current CVM.  
> - After you execute the following command on the Windows Server 2012 or Windows Server 2012 R2 operating system, the account Administrator and its password of the CVM will be deleted. Reset your account and password after restarting the CVM as detailed in [Reset Instance Password](https://intl.cloud.tencent.com/document/product/213/16566).
> 
```
C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /unattend:Unattend.xml
```
4. Create a custom image from the CVM instance on which Sysprep has been executed, and start new CVM instances with the image. See [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942).
And now, each new CVM instance will have a unique SID when joining a domain.
> To check CVM SID, execute the command `whoami /user`.
>


