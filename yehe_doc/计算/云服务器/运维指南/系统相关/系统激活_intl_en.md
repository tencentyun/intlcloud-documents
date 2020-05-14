Tencent CVMs use KMS to authorize Windows servers.
> 
> - This document is intended only for Windows Server public images provided by Tencent Cloud. The activation methods described in this document are not applicable to custom images or images imported from external sources.
> - Windows Server 2008 and Windows Server 2012 servers need to be authorized in this method. The default KMS address (kms.tencentyun.com:1668) configured in the public images of Windows Server 2016 and Windows Server 2019 is correct and does not need to be modified.


## Activation Precautions
1. SPP Notification Service in Windows is used to run activation-related services. Ensure that it runs properly, as shown in the following figure:
![](https://main.qcloudimg.com/raw/f84f7bd86fae0df1c2394cdc554b6a98.png)
2. Some optimization software programs may disable modifying the execution permissions of service-related programs. For example, if the execution permissions of the sppsvc.exe process are modified, services may become abnormal.
![](https://mc.qcloudimg.com/static/img/685fe41ef992f11ba305dfb570cb916c/21.png)
Before you attempt to activate a Windows CVM, ensure that the service and other basic features of the Windows CVM are normal.
 
## Automatic Activation
Tencent Cloud encapsulates a script for activating Windows servers, which simplifies automatic activation.
1. Log in to the Windows CVM.
2. Visit `http://mirrors.tencentyun.com/install/windows/activate-win.bat` in the web browser and download the script.
3. Run the script to complete automatic activation.

## Manual Activation

### Notes
If the system clock on some systems is incorrect, an error will occur during manual activation. Therefore, synchronize the system clock first by completing the following steps:
> If the system clock on the Windows CVM is correct, skip to [Activation directions](#ActivationStep).
>
1. Log in to the Windows CVM.
2. On the desktop, choose **Start** > **Run**. In the "Run" dialog box, enter `cmd.exe` to open the console window.
3. In the console window, run the following commands in sequence to synchronize the system clock:
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm /resync
```

<span id="ActivationStep"></span>
### Activation directions

1. Log in to the Windows CVM.
2. On the desktop, choose **Start** > **Run**. In the "Run" dialog box, enter `cmd.exe` to open the console window.
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




