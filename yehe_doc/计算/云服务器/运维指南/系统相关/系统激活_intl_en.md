Tencent CVM uses KMS to authorize a Windows server.
> 
> - This document is intended only for Windows Server public images provided by Tencent Cloud, but inapplicable to custom images or images imported from external sources.
> - Windows Server 2008 and Windows Server 2012 require this authorization. The default KMS address (kms.tencentyun.com:1668) configured in the public images of Windows Server 2016 and Windows Server 2019 is correct without any modification needed.


## Before Activation
1. SPP Notification Service on Windows is used to perform activation-related services, and its proper operation needs to be ensured, as shown below:
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. Some optimization software may disable modifying the execution permissions of service-related programs. For example, if the execution permissions of the sppsvc.exe process are modified, services may become abnormal.
![](https://main.qcloudimg.com/raw/c1ad23337b0f1b6e186d0c6e50c9e1b5.png)
Before you attempt to activate a Windows CVM, make sure that the service and other essential features of Windows are normal.


## Automatic Activation
Tencent Cloud encapsulates a script for Windows server activation, which is much simpler than manual activation.
1. Log in to the Windows CVM.
2. Visit `http://mirrors.tencentyun.com/install/windows/activate-win.bat` in the web browser, and download the script.
3. Run the script to complete automatic activation.

## Manual Activation

### Notes
On some systems, if the system clock has any problem, an error will occur during manual activation. In this case, you need to synchronize the system clock first by following the steps below:
> If the system clock on the Windows CVM is normal, go to the [Activation directions](#ActivationStep).
>
1. Log in to the Windows CVM.
2. On the desktop, click **Start** -> **Run**, and enter `cmd.exe` to open the console window.
3. In the console window, run the following commands in sequence to synchronize the system clock.
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### Activation directions

1. Log in to the Windows CVM.
2. On the desktop, click **Start** -> **Run**, and enter `cmd.exe` to open the console window.
3. In the console window, run the following commands in sequence to complete manual activation.
 - Run the following commands in sequence for Windows Server 2008, Windows Server 2012, and Windows Server 2019:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Run the following commands in sequence for Windows Server 2016:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




