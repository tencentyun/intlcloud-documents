## Overview

High-performance power management is required for the Windows Server operating system (OS) to support the soft shutdown of CVM instances. Otherwise, you can only forcibly shut down CVM instances on the CVM console. This document uses Windows Server 2012 as an example to describe how to configure power management.

## Notes

To modify power management, you do not need to restart your computer.

### Directions

1. Log in to a Windows instance using either [the RDP file (recommended)](https://intl.cloud.tencent.com/document/product/213/5435) or [the remote desktop](https://intl.cloud.tencent.com/document/product/213/32498).
2. Open Internet Explorer in the Windows CVM, access the Tencent Cloud private network, and download the Tencent Cloud power modification and configuration tool.
The download address is `http://mirrors.tencentyun.com/install/windows/power-set-win.bat`.
For example, download the Tencent Cloud power modification and configuration tool (power-set-win.bat) to the C: drive.
3. Use the command line tool (CMD) as the administrator to open power-set-win.bat.
![](https://main.qcloudimg.com/raw/22f81122e1188fc83ed4b1100a7469bc.png)
4. Run the following command to view the current power management plan:
```
powercfg -L
```
The returned result is as follows:
 ![](https://main.qcloudimg.com/raw/54ceb4faddc8745b30556621268ac318.png)

4. On the desktop of the operating system, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"> > **Control Panel** > **System and Security** > **Power Options**.
5. In the **Power Options** window, click **Change plan settings**.
![](https://main.qcloudimg.com/raw/54183c1f9d914789b986781b8a4da6ec.png)
6. In the **Edit Plan Settings** window, modify the idle turn-off times of the monitor and disk.
 ![](https://main.qcloudimg.com/raw/f0b7f447d90fe50ef829a10dab0029c6.png)

