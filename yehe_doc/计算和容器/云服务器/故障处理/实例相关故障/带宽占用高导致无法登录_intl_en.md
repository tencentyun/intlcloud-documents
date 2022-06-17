This document describes how to diagnose and troubleshoot Linux or Windows CVM login issues caused by high bandwidth utilization.

## Problems
- In the [CVM console](https://console.cloud.tencent.com/cvm/index), the bandwidth monitoring data of the CVM shows that bandwidth usage is too high, and connection to CVM fails.
- A [Health check](https://console.cloud.tencent.com/workorder/check) shows that the bandwidth utilization is too high.

## Fault Locating and Troubleshooting

1. Log in to the target CVM instance using VNC:
 - For Windows instances, see [Logging into Windows Instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496).
 - For Linux instances, see [Logging In to Linux Instances (VNC)](https://intl.cloud.tencent.com/document/product/213/32494).
2. Troubleshoot:
<dx-tabs>
::: Windows CVM instances
After logging in to the Windows CVM instance via VNC, perform the following operations:
<dx-alert infotype="explain" title="">
The following operations use a CVM instance running the Windows Server 2012 operating system as an example.
</dx-alert>

1. In the CVM instance, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px;"></img>. Select **Task Manager** to open the **Task Manager** page.
4. Select **Performance** tab, and click **Open resource monitor**.
5. On the **Resource Monitor** page, identify the process that consumes a lot of bandwidth. Based on your actual business, determine whether the process is normal.
 - If this process is a service process, check whether the high bandwidth utilization is caused by changes in access traffic and whether you need to optimize the capacity or upgrade the CVM configuration as instructed in [Changing Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178).
 - If this process has an exception, the high bandwidth utilization may be caused by a virus or a trojan. If so, you can manually terminate the process or use security software to kill the virus. You can also back up data and then reinstall the operating system.
<dx-alert infotype="notice" title="">
In Windows, many virus processes can disguise themselves as system processes. You can select **Task Manager** > **Processes** to check the process information and preliminarily identify the virus.
Normal system processes have complete signatures and descriptions, and most of them are located in the `C:\Windows\System32` directory. While virus programs may have the same names as system processes, they lack signatures and descriptions. In addition, their locations are often abnormal.
</dx-alert>
 - If this process is a Tencent Cloud component process, please [submit a ticket](https://console.cloud.tencent.com/workorder/category), and we will help you locate and troubleshoot the problem.
:::
::: Linux CVM instances
After logging in to the Linux CVM instance via VNC, perform the following operations:
<dx-alert infotype="explain" title="">
The following operations use a CVM instance running the CentOS 7.6 operating system as an example.
</dx-alert>


1. Run the following command to install the iftop tool. This tool monitors traffic for Linux CVM instances.
```shellsession
yum install iftop -y
```
<dx-alert infotype="explain" title="">
For Ubuntu system, run the `apt-get install iftop -y` command.
</dx-alert>
2. Run the following command to install lsof.
```shellsession
yum install lsof -y
```
3. Run the following command to run iftop.
```shellsession
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
```shellsession
lsof -i | grep IP
```
For example, if the IP address of the consumed traffic is 201.205.141.123, run the following command:
```shellsession
lsof -i | grep 201.205.141.123
```
If the following result is returned, the majority of the CVM bandwidth is consumed by the SSH process.
```shellsession
sshd       12145    root    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
sshd       12179  ubuntu    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
```
5. View the process that consumes a lot of bandwidth and check whether the process is normal.
 - If this process is a service process, check whether the high bandwidth utilization is caused by changes in access traffic and whether you need to optimize the capacity or upgrade the CVM configuration as instructed in [Changing Instance Configuration](https://intl.cloud.tencent.com/document/product/213/2178).
 - If this process has an exception, the high bandwidth utilization may be caused by a virus or a trojan. If so, you can manually terminate the process or use security software to kill the virus. You can also back up data and then reinstall the operating system.
 - If this process is a Tencent Cloud component process, please [submit a ticket](https://console.cloud.tencent.com/workorder/category), and we will help you locate and troubleshoot the problem.


We strongly recommend that you query the location of the destination IP on the [IP138 query website](http://www.ip138.com/). Note that the security risk is greater if the destination IP is found to be located in a region outside the Chinese mainland.

:::
</dx-tabs>





