CVMs use KMS to authorize Windows servers.
>! 
> - This document is intended only for Windows Server public images provided by Tencent Cloud. It is not applicable for custom images or images imported from external sources.
> - Windows Server 2008 and Windows Server 2012 need to be authorized using this method. The default KMS address (kms.tencentyun.com:1668) configured for the public images of Windows Server 2016 and Windows Server 2019 is correct and does not need to be modified.


## Notes
1. The SPP Notification Service in **Windows Server 2008** is used for activation. Make sure it runs properly, as shown in the following figure:
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. Some optimization software may disable modifying the execute permissions of service programs. For example, modifying the execute permissions of sppsvc.exe might result in exceptions, as shown below:
![](https://main.qcloudimg.com/raw/c1ad23337b0f1b6e186d0c6e50c9e1b5.png)
Before you activate a Windows CVM, make sure that services and other features on the Windows CVM are normal.
 
## Automatic Activation
Tencent Cloud encapsulates a script for activating Windows servers, which simplifies automatic activation. To use the activation script, follow the steps below:
1. Log in to the Windows CVM.
2. Download the [script](https://iso-1251783334.cos.ap-guangzhou.myqcloud.com/scripts/activate-win.bat), and run it to complete automatic activation.


## Manual Activation

### Notes
An inaccurate system clock will trigger an error during manual activation for some systems. In that case, you need to synchronize the system clock first by following the steps below:
>? If the system clock on the Windows CVM is normal, skip to [Activation](#ActivationStep).
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
3. In the console window, run the following commands sequentially to complete manual activation.
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




