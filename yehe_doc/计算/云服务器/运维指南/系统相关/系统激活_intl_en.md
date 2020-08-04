CVMs use KMS to authorize Windows servers.
> 
> - This document is only applicable to Windows Server public images provided by Tencent Cloud. Custom and imported images cannot use the activation methods described in this document.
> - Windows Server 2008 and Windows Server 2012 need to be authorized using this method. The default KMS address (kms.tencentyun.com:1668) configured for the public images of Windows Server 2016 and Windows Server 2019 is correct and does not need to be modified.


## Notes
1. SPP Notification Service in Windows is used to run activation services. Make sure it runs properly, as shown in the following figure:
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. Some optimization software may disable modifying the execute permissions of service-related programs. For example, if the execute permissions of sppsvc.exe processes are modified, services may have an exception.
![](https://main.qcloudimg.com/raw/c1ad23337b0f1b6e186d0c6e50c9e1b5.png)
Before you activate a Windows CVM, make sure that services and other features on the Windows CVM are normal.

## Automatic Activation
Tencent Cloud encapsulates a script for activating Windows servers, which simplifies automatic activation.
1. Log in to the Windows CVM.
2. Open the browser on CVM, visit `http://mirrors.tencentyun.com/install/windows/activate-win.bat` and download the script.
3. Run the script to complete automatic activation.

## Manual Activation

### Notes
If the system clock has any issues, an error will occur during manual activation. Synchronize the system clock first by completing the following steps:
> If the system clock on the Windows CVM is normal, skip to [Activation](#ActivationStep).
>
1. Log in to the Windows CVM.
2. On the desktop, choose **Start** > **Run**. Enter `cmd.exe` in the "Run" dialog box to open the console window.
3. In the console window, run the following commands in sequence to synchronize the system clock:
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### Activation

1. Log in to the Windows CVM.
2. On the desktop, choose **Start** > **Run**. Enter `cmd.exe` in the "Run" dialog box to open the console window.
3. In the console window, run the following commands in sequence to complete manual activation:
 - Run the following commands in sequence for Windows Server 2008 and Windows Server 2012 servers:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Run the following commands in sequence for Windows Server 2016 servers:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




