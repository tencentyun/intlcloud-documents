## What is Windows Recovery?

**Windows Recovery** is a state in which users can repair, back up, or restore the system. If Windows detects certain system problems with its automatic repair function and believes that the system will be damaged if it continues to work, it will stop itself from starting up and enter the system recovery mode.
System Recovery Options include several tools, such as Startup Repair, System Restore, and Windows Memory Diagnostic. You can use those tools to repair problems, back up data, and restore the system.

If users fail to log in to a CVM remotely, and see the following figure when logging in to the CVM via the console, it means that the Windows CVM has entered the recovery mode.
![](//mc.qcloudimg.com/static/img/e278c336a415066dcb8fc58333395ac3/image.png)

## Reasons for entering recovery mode
Common reasons for entering recovery mode:

- **The power was cut off while Windows was running or shutting down.** This includes shutting down the CVM in the console while Windows was running or shutting down. Windows entered the recovery mode because of possible loss of important data caused by improper shutdown.
- **The power was cut off when Windows was updating.** Windows entered the recovery mode because of possible loss of important data during the interrupted update.
- **The system was damaged by Trojans or viruses.**
- **Bugs in Windows core services**. Windows detected a risk itself and entered Recovery mode.
- ** The system lost critical data or was damaged.** Windows entered the recovery mode because users accidentally damaged system files.

## Precautions
It is recommended to take the following precautions:

 - When shutting down the CVM, go to the console to monitor the shutdown process. The soft shutdown used by Tencent Cloud has a timeout mechanism. After soft shutdown is executed, if the shutdown process has not been completed after the preconfigured period, the system will return failure. If the shutdown process is slow or Windows updates start, do not force the shutdown; instead, just wait for the shutdown to complete. Please refer to [Several Scenarios of Shutdown Failure](https://intl.cloud.tencent.com/document/product/213/4933/doc/product/213/2917#2.-.E5.85.B3.E6.9C.BA.E5.A4.B1.E8.B4.A5.E7.9A.84.E5.87.A0.E7.A7.8D.E5.9C.BA.E6.99.AF2) as needed.
 - Check whether there are abnormal programs or processes in the system，such as Trojans or viruses.
 - Check whether the system management and anti-virus software is running normally.
 - Install Windows updates in time, especially important updates and security updates.
 - Check the system event logs regularly to see if there is an bug in core services.

## Solutions
 If Windows enters the recovery mode, you can continue the startup or allows Windows to automatically repair itself. Windows can automatically repair minor problems. Please follow the steps below:

 1. Log in to the CVM via the [CVM Console](https://console.cloud.tencent.com/cvm).
 2. On the recovery mode interface, click **Next**.
	![](//mc.qcloudimg.com/static/img/94a1cf0f55d2c449a9d026bbbad5e4cd/image.png)
 3. When the system recovery options show up, click **Next** to use the default solution.
 ![](//mc.qcloudimg.com/static/img/d178865f822d2146eb3bb58f1b851294/image.png)
 4. Click **Restart**, and quickly press **F8**.
 ![](//mc.qcloudimg.com/static/img/ab2fdd697015fcb7e53b287052086b65/image.png)
 5. Choose "Start Windows Normally".
 ![](https://main.qcloudimg.com/raw/c3c62a6d77a2fe41d0ad02899faa06ed.png)
 6. If the startup fails, reinstall the system via the Console. See [Use console to reinstall system](https://intl.cloud.tencent.com/doc/product/213/4933#.E4.BD.BF.E7.94.A8.E6.8E.A7.E5.88.B6.E5.8F.B0.E9.87.8D.E8.A3.85.E7.B3.BB.E7.BB.9F3) for more details.
