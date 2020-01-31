
This document describes how to diagnose and troubleshoot Linux or Windows CVM login issues caused by high bandwidth usage.

## Problems
- In [CVM Console](https://console.cloud.tencent.com/cvm/index), the bandwidth monitoring data of the CVM shows that bandwidth usage is too high, and connection to CVM fails.
- Use [Self-Diagnose](https://console.cloud.tencent.com/workorder/check) tool to check and the result shows outbound bandwidth occupation is too high.

## Locating and troubleshooting the issues

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. Select the CVM to be checked and click **Log In**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/b7f0594ddecad128707ee720502e10b0.png)
3. In the **Log into Windows/Linux instance** window that pops up, select **Alternative login methods (VNC)**, and click **Log In Now** to log in to the CVM.
4. In the login window that pops up, select **Send Remote Command** in the top left corner, and click **Ctrl-Alt-Delete** to enter the system login interface as shown below:
![](https://main.qcloudimg.com/raw/2dec43fa6ddb5e442da59c75f7a34b0f.png)

### Windows CVMs
After using VNC to log into Windows CVM, perform the following operations:
>? The following operations take a CVM with the Windows Server 2012 system as an example.
>
1. In the CVM, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>. Select **Task Manager** to open the **Task Manager** window.
2. Select the **Performance** tab page and click **Open Resource Monitor**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/3608da7a567b81dabbbaaaa2a4635c3b.png)
3. Once **Resource Monitor** opens, check which process consumes more bandwidth. According to your actual business, determine whether the process is normal. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/d8fc6cd4b8095110a0e4a2e73ba93559.png)
 - If the process that consumes a lot of bandwidth is normal, check whether it is due to changes in access volume, and whether you need to optimize the capacity or [upgrade CVM configurations](https://cloud.tencent.com/document/product/213/2178).
 - If the process that consumes a lot of bandwidth is abnormal, there may be a virus or a Trojan. You can terminate the process on your own or use security software. You can also reinstall the system after data backup.
 >! In Windows systems, many virus processes are disguised as system processes. You can use process information in **Task Manager** > **Processes** to perform preliminary inspection:
 > Normal system processes have complete signatures and descriptions, and most of them locate under the C:\Windows\System32 directory. Virus programs may have the same name as system processes, but they do not have signatures or descriptions. The location will also be abnormal.
 > 
 - If the process that consumes a lot of bandwidth is a Tencent Cloud component process, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. We will help you locate and troubleshoot the problem.

### Linux CVMs
After using VNC to log into the Linux CVM, perform the following operations:
>? The following operations take a CVM with the CentOS 7.6 system as an example.
>
1. Execute the following command to install the iftop tool. The iftop tool is a traffic monitoring gadget for Linux CVM.
```
yum install iftop -y
```
>? For Ubuntu system, execute the `apt-get install iftop -y` command.
>
2. Execute the following command to install lsof.
```
yum install lsof -y
```
3. Execute the following command to run iftop. This is shown in the following figure:
```
iftop
```
![](https://main.qcloudimg.com/raw/7fccea56d998a65df6ff7e9348772910.png)
 - `<=`、`=>` indicates the direction of traffic
 - TX indicates the delivery traffic
 - RX indicates the receiving traffic
 - TOTAL indicates total traffic
 - cum indicates the total traffic from the moment iftop starts to run until now
 - peak indicates traffic peaks
 - rates indicate the average traffic over the last 2s, 10s, and 40s respectively
4. According to the IP of the consumed traffic in iftop, execute the following command to check the process connected to this IP.
```
lsof -i | grep IP
```
For example, if the IP of the consumed traffic is 201.205.141.123, run the following command:
```
lsof -i | grep 201.205.141.123
```
If the following results are returned, CVM bandwidth is mainly consumed by the SSH process.
```
sshd       12145    root    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
sshd       12179  ubuntu    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
```
5. View the process that consumes bandwidth, and determine whether the process is normal.
 - If the process that consumes a lot of bandwidth is normal, check whether it is due to changes in access volume, and whether you need optimize the capacity or [upgrade CVM configurations](https://cloud.tencent.com/document/product/213/2178).
 - If the process that consumes a lot of bandwidth is abnormal, there may be a virus or a Trojan. You can terminate the process on your own or use security software. You can also reinstall the system after data backup.
 - If the process that consumes a lot of bandwidth is a Tencent Cloud component process, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us. We will help you locate and troubleshoot the problem.


We recommend you check the location of the destination IP on [What Is My IP Address](https://whatismyipaddress.com/). If the IP location is in other countries/regions, the security risk is greater.

