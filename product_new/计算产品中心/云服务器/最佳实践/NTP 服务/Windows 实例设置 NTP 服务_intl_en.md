## Scenario

This document is about how to enable NTP service for Windows Server and modify the clock source server address.

Windows Time service (W32Time) is used to synchronize the time of the local system and the clock source server. It uses NTP to synchronize computer clocks throughout the network. The following describes how to enable NTP service and modify the clock source server address via client and command line for Windows Server 2016.

## Directions

1. [Log in to the Windows instance remotely](https://intl.cloud.tencent.com/document/product/213/5435)。
2. Click “Administrative Tools > Services > Windows Time”.
![Windows Time](https://main.qcloudimg.com/raw/0791d5ed9387f4f876e87e41d368f837.png)
3. The startup type is set to "Automatic" and if the service is not started, click "Start".
![w32time](https://main.qcloudimg.com/raw/5c1bb71c0e459a3b1e6504179751a727.png)
4. In the notification area of the taskbar, click Time and click “Date and time settings”.
![Time Settings](https://main.qcloudimg.com/raw/977f0739c7cccdb5ef10a563d60220d2.png)	
5. Switch to the "Internet Time" tab and click Change Settings.
![Internet Time](	https://main.qcloudimg.com/raw/ed410b96b0f38e6be2837a13e9237b33.png)
6. In the Internet Time Settings pop-up window, enter the domain name or IP address of the target clock source server and click “OK”.
![Internet Time Settings](https://main.qcloudimg.com/raw/f34302c371c011d3b6e4046036910baa.png)
7. After you complete the setup, reopen “Date & Time”  and you will see that the clock source server has been changed.
![Confirm the setting](https://main.qcloudimg.com/raw/a14f916bd1189b00554bb94658012f21.png)


