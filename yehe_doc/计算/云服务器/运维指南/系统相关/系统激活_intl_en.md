Tencent CVM uses KMS to authorize a Windows server.
> 
> - This document is intended only for Windows Server public images provided by Tencent Cloud. It is not applicable for custom images or images imported from external sources.
> - This authorization is required for Windows Server 2008 and Windows Server 2012. The default KMS address (kms.tencentyun.com:1668) configured in the public images of Windows Server 2016 and Windows Server 2019 can be used without any further modification.


## Before Activation
1. SPP Notification Service on Windows is used for activation. Make sure it is running properly. 
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. Some optimization software may disable modifying the execution permissions of service programs. For example, modifying the execution permissions of sppsvc.exe might result in exceptions.
![](https://mc.qcloudimg.com/static/img/685fe41ef992f11ba305dfb570cb916c/21.png)
Before you attempt to activate a Windows CVM, make sure that the service and other essential features of Windows are running properly.
 
## Automatic Activation
Tencent Cloud encapsulates a script for Windows server activation, simplifying the activation process.
1. Log in to the Windows CVM.
2. Visit `http://mirrors.tencentyun.com/install/windows/activate-win.bat` via a web browser and download the script.
3. Run the script to complete automatic activation.

## Manual Activation

### Notes
An inaccurate system clock will trigger an error during manual activation for some systems. In such cases, you need to synchronize the system clock first by following the steps below:
> If the system clock on the Windows CVM is accurate, go to the [Activation directions](#ActivationStep).
>
1. Log in to the Windows CVM.
2. On the desktop, click **Start** -> **Run**, and enter `cmd.exe` to open the console window.
3. In the console window, run the following commands sequentially to synchronize the system clock.
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### Activation directions

1. Log in to the Windows CVM.
2. On the desktop, click **Start** -> **Run**, and enter `cmd.exe` to open the console window.
3. In the console window, run the following commands sequentially to complete manual activation.
 - Run the following commands sequentially for Windows Server 2008, Windows Server 2012, and Windows Server 2019:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Run the following commands sequentially for Windows Server 2016:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




