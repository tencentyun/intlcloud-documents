## Scenario

This document is about how to enable NTP service for Windows Server and modify the clock source server address.

Windows Time service (W32Time) is used to synchronize the time of the local system and the clock source server. It uses NTP to synchronize computer clocks throughout the network. The following describes how to enable NTP service and modify the clock source server address via client and command line for Windows Server 2016.

## Directions

1. [Log in to the Windows instance remotely](https://intl.cloud.tencent.com/document/product/213/5435)。
2. Click “Administrative Tools > Services > Windows Time”.
![Windows Time](https://main.qcloudimg.com/raw/c5e41df2fc832b0f25f798408163664c.png)
3. The startup type is set to "Automatic" and if the service is not started, click "Start".
![w32time](https://main.qcloudimg.com/raw/9201ddaca176a1523d5d12d02b6c8ec5.png)
4. In the notification area of the taskbar, click Time and click “Date and time settings”.
![Time Settings](https://main.qcloudimg.com/raw/28ba1cf5968466e114e93d222b957f99.png)	
5. Switch to the "Internet Time" tab and click Change Settings.
![Internet Time](https://main.qcloudimg.com/raw/acc52fce975638cef4e39f9f821d66bc.png)
6. In the Internet Time Settings pop-up window, enter the domain name or IP address of the target clock source server and click “OK”.
![Internet Time Settings](https://main.qcloudimg.com/raw/205ef59f3e8583af965a9381df0a9ef9.png)
7. After you complete the setup, reopen “Date & Time”  and you will see that the clock source server has been changed.
![Confirm the setting](https://main.qcloudimg.com/raw/767eee448b33ed38ea7bc2fbdadf780d.png)


