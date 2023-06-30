This document describes how to locate and troubleshoot the problems that cause website access failure.

## Possible Causes

Website access failure may be caused by network problems, firewall configurations or CVM overload.

## Troubleshooting
<span id="TroubleshootServer"></span>
### Troubleshooting CVM problems
CVM shutdown, hardware failure, and high CPU/memory/bandwidth usage may all cause website access failure. Thus, we recommend that you check CVM running status and CPU/memory/bandwidth usage.

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index) and verify whether the running status of the CVM instance is normal on the instance management page, as shown below:
![](https://main.qcloudimg.com/raw/c8347dcc04834aa44ade7324b7012d73.png)
 - If yes, please execute [step 2](#Server_step02).
 - If no, please restart the CVM instance.
2. <span id="Server_step02">Click the ID/name of the instance to enter its details page.</span>
3. Select the **Monitoring** tab to view the instance resource usage, as shown below:
![](https://main.qcloudimg.com/raw/b8396a4507dd6a9808f9907b90e881fa.png)
 - If the CPU/memory usage is too high, please refer to [Failed to log in to a Windows CVM due to high CPU and memory usage](https://intl.cloud.tencent.com/document/product/213/32405) and [Failed to log in to a Linux CVM due to high CPU and memory usage](https://intl.cloud.tencent.com/document/product/213/32387) for troubleshooting.
 - If the bandwidth usage is too high, please refer to [Login Failure Due to High Bandwidth Occupation](https://intl.cloud.tencent.com/document/product/213/32542) for troubleshooting.
 - If CPU/memory/bandwidth usage is normal, please execute [step 4](#Server_step04).
4. <span id="Server_step04">Execute the following command to check whether the corresponding Web service port is being monitored normally. </span>
> The following operations take port 80, which is commonly used in HTTP service, as an example.
>
 - For a Linux instance: execute the `netstat -ntulp |grep 80` command, as shown below:
 ![](https://mc.qcloudimg.com/static/img/ab5fa663197c3fa0738b2ceb3f559fd3/image.png)
 - For a Windows instance: open the CMD command line tool to execute the `netstat -ano|findstr :80` command, as shown below:
 ![](https://mc.qcloudimg.com/static/img/c9c32a2e9f12235ad3d2a5aca313f298/image.png)
 - If the port is being monitored normally, please execute [step 5](#Server_step05).
 – If the port is not being monitored normally, please check whether the Web service process is launched or correctly configured.
5. <span id="Server_step05">Check whether the corresponding Web service port is opened in the firewall configuration.</span>
 - For a Linux instance: execute the `iptables -vnL` command to check whether iptables opens port 80.
    - If port 80 is open, please [troubleshoot network-related problems](#TroubleshootNetwork).
    - If port 80 is not open, please execute the `iptables -I INPUT 5 -p tcp  --dport 80 -j ACCEPT` command to open it.
 - For a Windows instance: click **Start** > **Control Panel** > **Windows Firewall** on the OS interface to check whether Windows firewall configuration is off.
		- If yes, please [troubleshoot network-related problems](#TroubleshootNetwork).
		- If no, please turn off the Windows firewall configuration.

<span id="TroubleshootNetwork"></span>
### Troubleshoot network-related problems
Network problems can also cause network access failure. You can execute the following command to check whether the network has packet loss or high latency.
```
ping the public IP of the server
```
- If a result similar to the one below is returned, there is packet loss or high latency. Please use MTR for troubleshooting. For more information, please see [CVM Network Latency and Packet Loss](https://intl.cloud.tencent.com/document/product/213/14638).
![](https://mc.qcloudimg.com/static/img/30d9946522f43cfc1c6731b9035ae9e9/image.png)
- If there is no packet loss or high latency, please [troubleshoot security group problems](#TroubleshootSecurityGroup).

<span id="TroubleshootSecurityGroup"></span>
### Troubleshoot security group problems
Security group is a virtual firewall that allows you to control the inbound and outbound traffic of the associated instance. You can specify protocols, ports and policies for security group rules. If you did not open the ports related to the Web processes, website access failure may occur.
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index) and click the ID/name of the instance to enter its details page.
2. Click the **Security Group** tab to view the bound security groups and their outbound and inbound rules. Confirm that the ports related to the Web processes are open, as shown below:
![](https://main.qcloudimg.com/raw/b5782326fcdd77a74ca1435b202ca97b.png)


