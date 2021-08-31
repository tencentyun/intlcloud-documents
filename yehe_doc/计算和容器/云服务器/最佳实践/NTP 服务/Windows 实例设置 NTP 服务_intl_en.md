## Scenario

The Windows Time service (W32Time) synchronizes the time between the local system and the clock source server. It uses NTP to synchronize computer clocks on the network. The following uses a CVM that runs Windows Server 2012 as an example to describe how to enable the NTP service and modify the IP address of the clock source server.

## Directions

1. Log in to the Windows CVM.
2. On the desktop, choose <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img> > **Task Manager** > **Services** to open the **Services** window.
3. In the **Services** window that appears, double-click **Windows Time**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/c5e41df2fc832b0f25f798408163664c.png)
4. In the **Windows Time Properties (Local Computer)** window that appears, set **Startup type** to **Automatic** and **Service status** to **Running**, and then click **OK**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/9201ddaca176a1523d5d12d02b6c8ec5.png)
5. In the task bar of the desktop, click the time icon in the lower-right corner and click **Change date and time settings…**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/28ba1cf5968466e114e93d222b957f99.png)
6. In the **Date and Time** window that appears, click the **Internet Time** tab, and then click **Change settings**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/767eee448b33ed38ea7bc2fbdadf780d.png)
7. In the **Internet Time Settings** window that appears, enter the domain name or IP address of the target clock source server in the **Server** text box and click **OK**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/205ef59f3e8583af965a9381df0a9ef9.png)



