## Windows Recovery Mode

**Windows Recovery** is an auto-recovery feature of Windows. When Windows detects certain system problems and believes that continuous running will cause system damage, this automatic repair feature will prevent Windows from starting up and provide **System Recovery Options** to users to repair, back up or restore the system. 
**System Recovery Options** includes **Startup Repair**, **System Restore**, and **Windows Memory Diagnostic**, which can help users fix problems, back up data, and restore the system.
If you cannot remotely log in to a CVM, and see the following figure when logging in to the CVM via the console, it means that the Windows CVM has entered the recovery mode.
![](//mc.qcloudimg.com/static/img/e278c336a415066dcb8fc58333395ac3/image.png)

## Reasons
In the following situations, the system may enter the recovery mode.
- **The power was cut off while Windows was running or shutting down.** The Windows system was forcibly shut down via the console. Both scenarios may cause loss of critical data.
- **The power was cut off while Windows was updating.** This may cause loss of critical update data.
- **The system was damaged by Trojans or viruses.**
- **There were bugs in Windows core services**. Windows detected a risk.
- **The system lost critical data or was damaged**. The system files were corrupted due to misoperation.

## Precautions
Recommended precautions are as follows:
 - Log in to the console to monitor the shutdown process of a Windows system. Tencent Cloud supports the soft shutdown that comes with a timeout mechanism. If the shutdown process has not been completed within the given period, a failure message will be returned. If the shutdown process is slow or Windows Update starts, do not force a shutdown; instead, just wait for the shutdown to complete. For more information, please see [Shutdown Failure Scenarios](https://intl.cloud.tencent.com/document/product/213/2917#shutdown-failure-scenarios).
 - Check whether there are abnormal programs or processes in the system, such as Trojans or viruses.
 - Check whether the system management and anti-virus software are running properly.
 - Install Windows updates in time, especially important updates and security updates.
 - Check the system event logs regularly to fix bug in core services.

## Solutions
 If Windows enters the recovery mode, perform the following steps to continue starting up or allow Windows to automatically repair minor problems.
1. Log in to the CVM via the [CVM console](https://console.cloud.tencent.com/cvm).
2. In the recovery mode page that appears, click **Next**.
![](//mc.qcloudimg.com/static/img/94a1cf0f55d2c449a9d026bbbad5e4cd/image.png)
3. In the **System Recovery Options** window, click **Next** to use the default solution, as shown below:
![](//mc.qcloudimg.com/static/img/d178865f822d2146eb3bb58f1b851294/image.png)
4. Click **Restart**, and quickly press **F8**.
![](//mc.qcloudimg.com/static/img/ab2fdd697015fcb7e53b287052086b65/image.png)
5. Choose **Start Windows Normally**.
 ![](https://main.qcloudimg.com/raw/c3c62a6d77a2fe41d0ad02899faa06ed.png)
If the startup fails, reinstall the system via the console. For more information, see [Reinstalling the system via the console](https://intl.cloud.tencent.com/document/product/213/4933#useConsole).


