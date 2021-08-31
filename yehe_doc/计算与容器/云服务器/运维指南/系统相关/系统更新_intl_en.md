## Introduction

This article uses Windows Server 2012 as an example to illustrate how to update your Windows operating system.

## Directions

### Updating Windows using the public network
You can use the Windows Update service to update your operating system. The detailed steps are as follows:
1. Log in to the Windows CVM instance.
2. Click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> -> **Control Panel** -> **Windows Update**. The **Windows Update** window appears.
3. Click **Check for updates**, and wait until the check is finished.
4. After the check is finished, click **N Important Updates Available** or **N Optional Updates Available** in “Windows Update”. The **Choose the Update to Install** window appears.
5. Select the updates you want to install, and click **Install**.
If you are prompted to restart your system after the update is completed, do so.
> If you log in using VNC after the instance is rebooted and the message "Updating...Do not turn off the power" or "Configuration has not been completed" appears, do not perform a force-shutdown. That may damage your CVM instance.

### Updating Windows using the private network
If your CVM instance does not have public network access, you can use the Tencent Cloud private Windows Update server to update your operating system. The Tencent Cloud Windows Update server has most of the updates, but does not have hardware driver packages and some uncommon updates. Therefore, uncommon services may not get updates using the Tencent Cloud Windows Update server.
Follow these steps to use the Tencent Cloud Windows Update server:
1. Log in to the Windows CVM instance.
2. Use Internet Explorer to download the Tencent Cloud private network configuration file wusin.bat from the following address:
http://mirrors.tencentyun.com/install/windows/wusin.bat
3. Run wusin.bat in Command Prompt with administrator privilege, as shown below:
> If you open wusin.bat using Internet Explorer after it finishes downloading, the console window will automatically close and you cannot observe the output.
>
You can save wusin.bat to your hard drive, such as C:\, and open a Command Prompt window with administrator privilege to run it.

If you no longer wish to use the Tencent Cloud Windows Update server, you can download wusout.bat clean it up. Follow these steps to do so:
1. Log in to the Windows CVM instance.
2. Use Internet Explorer to download the Tencent Cloud private network configuration file wusout.bat from the following address:
http://mirrors.tencentyun.com/install/windows/wusout.bat
3. Run wusout.bat in Command Prompt with administrator privilege, as shown below:
> If you open wusout.bat using Internet Explorer after it finishes downloading, the console window will automatically close and you cannot observe the output information.
>
You can save wusout.bat to your hard drive, such as C:\, and open a Command Prompt window with administrator privilege to run it.
