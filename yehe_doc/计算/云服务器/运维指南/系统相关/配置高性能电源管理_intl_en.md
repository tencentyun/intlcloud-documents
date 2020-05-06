## Operation Scenario

High-performance power management needs to be configured on Windows Server to enable graceful shutdown of CVM instances. Otherwise, the instance can only be hard shut down via the console. This document uses Windows Server 2012 as an example to describe how to configure power management.

## Operation Description

You do not need to restart the computer to modify power management.

## Directions

1. Log in to the Windows CVM.
2. Access the Tencent Cloud private network through the IE browser and download the Tencent Cloud power modification and configuration tool.
The download address is: `http://mirrors.tencentyun.com/install/windows/power-set-win.bat`
For example, download the Tencent Cloud power modification and configuration tool (power-set-win.bat) to the C: drive.
3. Use the administrator command tool (CMD) to open power-set-win.bat, as shown below:
![](https://main.qcloudimg.com/raw/65cb9654bcc9978a12ada6aabecb7de3.png)
4. Execute the following command to view the current power management plan.
```
powercfg -L
```

4. On the operating system interface, click <img src = "https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style = "margin: 0;">> **Control Panel** > **System and Security** > **Power Options**.
5. In the Power Options window, click **Change plan settings**.

6. In the “Edit Plan Settings” window that opens, modify the time to turn of the display and hard disk.
 



