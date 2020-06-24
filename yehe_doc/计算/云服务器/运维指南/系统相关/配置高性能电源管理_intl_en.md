## Overview

High-performance power management is required for the Windows Server operating system (OS) to support the soft shutdown of CVM instances. Otherwise, you can only shut down CVM instances on the CVM Console via hard shutdown. This document uses Windows Server 2012 as an example to describe how to configure power management.

## Notes

To modify power management, you do not need to restart your computer.

## Directions

1. Log in to the Windows CVM.
2. Access the Tencent Cloud private network through Internet Explorer and download the Tencent Cloud power modification and configuration tool.
The download address is `http://mirrors.tencentyun.com/install/windows/power-set-win.bat`.
For example, download the Tencent Cloud power modification and configuration tool (power-set-win.bat) to the C: drive.
3. Use the command line tool (CMD) as the administrator to open power-set-win.bat, as shown in the following figure:
![](https://main.qcloudimg.com/raw/65cb9654bcc9978a12ada6aabecb7de3.png)
4. Run the following command to view the current power management plan:
```
powercfg -L
```

5. On the desktop, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> and choose **Control Panel** > **System and Security** > **Power Options** to open the **Power Options** window.
6. In the "Power Options" window, click **Change plan settings**.
7. In the "Edit Plan Settings" window, modify the idle turn-off times of the monitor and disk.



