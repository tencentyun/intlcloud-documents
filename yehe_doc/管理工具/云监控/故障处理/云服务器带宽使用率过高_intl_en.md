## Overview
This document describes how to troubleshoot and solve the problem of Linux or Windows CVM login failure caused by overly high bandwidth utilization.


## Locating and Troubleshooting the Problem
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. Select the target CVM instance and click **Log In**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. On the **Log in to Windows/Linux instance** window that pops up, click **Log In Now** under **Alternative login methods (VNC)** to log in to the CVM instance.
4. On the login page that appears, select **Send CtrlAltDel** in the upper-left corner and click **Ctrl-Alt-Delete** to access the system login page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Windows CVM instances
After logging in to the Windows CVM instance via VNC, perform the following operations:
> The following operations use a CVM instance running in the Windows Server 2012 operating system as an example.
>
1. In the CVM instance, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>. Select **Task Manager** to open the **Task Manager** page.
2. Click the **Performance** tab and then click **Open Resource Monitor**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a635da7e769cc1424b225674803e5cb1.png)
3. On the **Resource Monitor** page, identify the process that consumes a lot of bandwidth. Based on your actual business, determine whether the process is normal, as shown in the following figure:
![](https://main.qcloudimg.com/raw/6a131472fc52bb4f5c4d5f57a1b7b010.png)
 - If this process is a service process, check whether the high bandwidth utilization is caused by changes in access traffic and whether you need to optimize the capacity or [upgrade the CVM configuration](https://intl.cloud.tencent.com/document/product/213/2178).
 - If this process has an exception, the high bandwidth utilization may be caused by a virus or a trojan. If so, you can manually terminate the process or use security software to kill the virus. You can also back up data and then reinstall the operating system.
 > In Windows, many virus processes can disguise themselves as system processes. You can select **Task Manager** > **Processes** to check the process information and preliminarily identify the virus.
 > Normal system processes have complete signatures and descriptions, and most of them are located in the `C:\Windows\System32` directory. While virus programs may have the same names as system processes, they lack signatures and descriptions. In addition, their locations are often abnormal.
 > 
 - If this process is a Tencent Cloud component process, please [submit a ticket](https://console.cloud.tencent.com/workorder/category), and we will help you locate and troubleshoot the problem.

### Linux CVM instances
After logging in to the Linux CVM instance via VNC, perform the following operations:
> The following operations use a CVM instance with the CentOS 7.6 operating system as an example.

1. Run the following command to install the iftop tool. This tool monitors traffic for Linux CVM instances.
```plaintext
yum install iftop -y
```
> For a CVM instance with the Ubuntu operating system, run the `apt-get install iftop -y` command.
2. Run the following command to install lsof.
```plaintext
yum install lsof -y
```
3. Run the following command to run iftop, as shown in the following figure:
```plaintext
iftop
```
![](https://main.qcloudimg.com/raw/7fccea56d998a65df6ff7e9348772910.png)
 - "<=" and "=>" indicate the direction of the traffic.
 - "TX" indicates the traffic is outbound.
 - "RX" indicates the traffic is inbound.
 - "TOTAL" indicates the total traffic.
 - "Cum" indicates the total traffic from the moment iftop started to run until now.
 - "peak" indicates the traffic peak.
 - "rates" indicates the average traffic over the last 2, 10, and 40 seconds.
4. Based on the IP address of the consumed traffic in iftop, run the following command to check the process connected to this IP address.
```plaintext
lsof -i | grep IP
```
For example, if the IP address of the consumed traffic is 201.205.141.123, run the following command:
```plaintext
lsof -i | grep 201.205.141.123
```
If the following result is returned, the majority of the CVM bandwidth is consumed by the SSH process.
```plaintext
sshd       12145    root    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
sshd       12179  ubuntu    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
```
5. View the process that consumes a lot of bandwidth and check whether the process is normal.
 - If this process is a service process, check whether the high bandwidth utilization is caused by changes in access traffic and whether you need to optimize the capacity or [upgrade the CVM configuration](https://intl.cloud.tencent.com/document/product/213/2178).
 - If this process has an exception, the high bandwidth utilization may be caused by a virus or a trojan. If so, you can manually terminate the process or use security software to kill the virus. You can also back up data and then reinstall the operating system.
 - If this process is a Tencent Cloud component process, please [submit a ticket](https://console.cloud.tencent.com/workorder/category), and we will help you locate and troubleshoot the problem.


We recommend that you check the location of the destination IP address on [WhatIsMyIPAddress.com](https://whatismyipaddress.com/). If the destination IP address is located in another country or region, the security risk is higher.

