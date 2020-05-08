Tencent CVM uses KMS for granting authorization to Windows.
> 
> - This article is only applicable to Windows Server public images hosted by Tencent Cloud. The activation methods described here do not work with custom images or images imported from external sources.
> - Windows Server 2008 and Windows Server 2012 require this mode of authorization. The default KMS address (kms.tencentyun.com:1668) configured in the public images of Windows Server 2016 and Windows Server 2019 is correct and does not need to be modified.


## Pre-activation Notes
1. SPP Notification Service on Windows is used to perform activation-related services. Make sure it runs as it should.
2. Certain optimization software may disable changes to the execution permissions of service-related executable programs. For example, changes to the execution permissions of sppsvc.exe process can cause abnormal operation of service:

Before you attempt to activate a Windows CVM instance, make sure that the service and other basic features of Windows are normal.
 
## Automatic Activation
Tencent Cloud provides a script for Windows server activation, which simplifies the process.
1. Log in to the Windows CVM instance.
2. Open Internet Explorer and download the script from  `http://mirrors.tencentyun.com/install/windows/activate-win.bat`.
3. Run the script to complete automatic activation.

## Manual Activation

### Notes
On some systems, if the system clock has any problem, an error will occur during manual activation. In this case, you need to synchronize the system clock first. The directions for synchronizing the clock are as follows:
> If the system clock on the Windows CVM instance is normal, go to the [Activation directions](#ActivationStep).
>
1. Log in to the Windows CVM instance.
2. Click **Start** -> **Run**, and enter `cmd.exe` to open the Command Prompt window.
3. Run the following commands synchronize the system clock.
```
w32tm /config /syncfromflags:manual /manualpeerlist:"ntpupdate.tencentyun.com"
w32tm / resync
```

<span id="ActivationStep"></span>
### Activation directions

1. Log in to the Windows CVM instance.
2. Click **Start** -> **Run**, and enter `cmd.exe` to open the Command Prompt window.
3. Run the following commands to complete manual activation.
 - Windows Server 2008 and Windows Server 2012:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```
 - Windows Server 2016:
```
cscript /nologo %windir%/system32/slmgr.vbs -skms kms1.tencentyun.com:1688
cscript /nologo %windir%/system32/slmgr.vbs -ato
```




