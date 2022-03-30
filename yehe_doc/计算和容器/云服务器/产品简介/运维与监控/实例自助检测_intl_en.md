## Overview
Self-Service instance detection can check the status information of CVM instances such as performance, fees, network, and disk utilization and keep you up to date with the instance running status. You can use this feature to discover and solve instance problems promptly.

## Overview
We recommend you use self-service instance detection in the following two scenarios:
- Troubleshooting: if any failure or problem occurs during instance operations, you can use self-service instance detection to locate and troubleshoot it and handle it according to the provided suggestions.
- All-Around instance check: during daily Ops, self-service instance detection can help you keep up to date with the overall instance running status and discover and solve problems promptly, guaranteeing normal business operations.

## Check Item Description
The check items of self-service instance detection are as detailed below:

<dx-accordion>
::: Local network check
<table>
<tr><th style="
    width: 18%;
">Check Item</th><th style="
    width: 35%;
">Description</th><th style="
    width: 8%;
">Risk<br>Level</th><th style="
    width: 39%;
">Solution</th></tr>
<tr>
<td>Network latency</td>
<td>An HTTP request is sent to check whether the network latency of the instance is high based on the following criteria:
<ul style="margin-bottom:0px">
<li>If the latency is above 600 ms, the network quality will be considered poor.</li>
<li>If no response is received within 5s, the request will be considered timed out.</li>
<li>If all requests time out, the network will be considered disconnected.</li>
</ul>
</td>
<td>Exception</td>
<td rowspan=4>Troubleshoot and fix the local network problems.</td>
</tr>
<tr>
<td>Network jitter</td>
<td>The average of the differences between the latency values of adjacent requests is the network jitter value. If the network jitter/latency is below or equal to 0.15, the network is stable; otherwise, the network is jittering.
</td>
<td>-</td>
</tr>
<tr>
<td>Upstream bandwidth</td>
<td>Data packets are uploaded to the instance to calculate its upstream bandwidth.</td>
<td>-</td>
</tr>
<tr>
<td>Downstream bandwidth</td>
<td>Data packets are downloaded from the instance to calculate its downstream bandwidth.</td>
<td>-</td>
</tr>
</table>
:::
::: Check on security group rule
<table>
<tr><th style="
    width: 18%;
">Check Item</th><th style="
    width: 35%;
">Description</th><th style="
    width: 8%;
">Risk<br>Level</th><th style="
    width: 39%;
">Solution</th></tr>
<tr>
<td>Whether common ports are open to the internet in the security group rule</td>
<td>The system checks whether requests to common ports such as ports 22 and 3389 used by the TCP protocol for the inbound traffic are blocked in the security group.</td>
<td>Warning</td>
<td>If requests to port 22 used by the TCP protocol are blocked in an ingress rule in the security group, SSH login may be abnormal. You can open the required ports to the internet as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32369">Security Group Use Cases</a>.</td>
</tr>
</table>
:::
::: Account fee check
<table>
<tr><th style="
    width: 18%;
">Check Item</th><th style="
    width: 35%;
">Description</th><th style="
    width: 8%;
">Risk<br>Level</th><th style="
    width: 39%;
">Solution</th></tr>
<tr>
<td rowspan=4>
Cloud disk expiration and consistency between the expiration times of the instance and cloud disks
<td>The system checks whether cloud disks associated with the instance have expired and whether they can be read/written.</td>
<td>Exception</td>
<td>A cloud disk associated with the instance has expired. Go to the <a href="https://console.cloud.tencent.com/cvm/cbs">CBS console</a> to renew it as soon as possible.</td>
</tr>
<tr>
<td>The system checks whether cloud disks associated with the pay-as-you-go instance are unavailable due to expiration.</td>
<td>Warning</td>
<td rowspan=1>Auto-Renewal of a cloud disk associated with the instance is not configured. Go to the <a href="https://console.cloud.tencent.com/cvm/cbs">CBS console</a> to configure auto-renewal for the cloud disk.</td>
</tr>
</table>

:::
::: Instance storage check

<table>
<tr>
<tr><th style="
    width: 18%;
">Check Item</th><th style="
    width: 35%;
">Description</th><th style="
    width: 8%;
">Risk<br>Level</th><th style="
    width: 39%;
">Solution</th></tr>
</tr>
<tr>
<td>High cloud disk latency</td>
<td>The system checks whether the I/O performance metric svctm is abnormal.</td>
<td>Warning</td>
<td>A cloud disk associated with the instance has a high latency. We recommend you pay attention to the cloud disk usage.</td>
</tr>
<tr>
<td>Cloud disk I/O hang</td>
<td>Cloud disk I/O hang</td>
<td>Warning</td>
<td>A cloud disk associated with the instance has an I/O hang. We recommend you pay attention to the cloud disk usage.</td>
</tr>
<tr>
<td>System disk inode utilization</td>
<td>The system checks whether the inode utilization of the cloud disk has reached 100%.</td>
<td>Warning</td>
<td rowspan=4>Pay attention to the cloud disk usage and troubleshoot as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/41974">Kernel and I/O Issues</a>.
</td>
</tr>
<tr>
<td>Whether the system disk is read-only</td>
<td>The system checks whether the cloud disk is read-only currently.</td>
<td>Exception</td>
</tr>
<tr>
<td>System disk space utilization</td>
<td>The system checks whether the utilization of the cloud disk has reached 100%.</td>
<td>Warning</td>
</tr>
<tr>
<td>Ratio of I/O operation time in disk partitions to total time</td>
<td>The system checks whether io_util of the cloud disk has reached 100%.</td>
<td>Warning</td>
</tr>
</table>
:::
::: Instance status check
<table>
<tr><th style="
    width: 18%;
">Check Item</th><th style="
    width: 35%;
">Description</th><th style="
    width: 8%;
">Risk<br>Level</th><th style="
    width: 39%;
">Solution</th></tr>
<tr>
<td>Instance shutdown</td>
<td>The system checks whether the instance is shut down currently.</td>
<td>Warning</td>
<td>The instance is shut down. Go to the <a href="https://console.cloud.tencent.com/cvm/index">CVM console</a> to start it.</td>
</tr>
<tr>
<td>Instance restart</td>
<td>The system checks whether the instance has been restarted in the last 12 hours.</td>
<td>Warning</td>
<td>The instance has been restarted in the last 12 hours. Pay attention to the instance running status.</td>
</tr>
<tr>
<td rowspan=3>Instance kernel crash</td>
<td>The system checks whether a hung task has occurred in the instance in the last 12 hours.</td>
<td>Exception</td>
<td rowspan=3>A hung task, panic, or soft deadlock has occurred in the instance in the last 12 hours. Pay attention to the instance running status and troubleshoot as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/41974">Kernel and I/O Issues</a>.</td>
</tr>
<tr>
<td>The system checks whether a hung task has occurred in the instance in the last 12 hours.</td>
<td>Exception</td>
</tr>
<tr>
<td>The system checks whether a soft deadlock occurred in the instance in the last 12 hours.</td>
<td>Exception</td>
</tr>
</table>
:::
::: Instance performance check
<table>
<tr><th style="
    width: 18%;
">Check Item</th><th style="
    width: 35%;
">Description</th><th style="
    width: 8%;
">Risk<br>Level</th><th style="
    width: 39%;
">Solution</th></tr>
<tr>
<td>CPU utilization</td>
<td>The system checks whether the instance has experienced a high CPU utilization in the last 12 hours.</td>
<td>Warning</td>
<td rowspan=3>
To prevent the CPU utilization from becoming a business bottleneck, we recommend you check the CPU utilization and adjust the configuration promptly. Troubleshoot as instructed in the following documents based on the operating system of your instance:
<ul style="margin:0">
<li>Windows instance: <a href="https://intl.cloud.tencent.com/document/product/213/32405">Failed to log in to a Windows CVM due to high CPU and memory usage</a></li>
<li>Linux instance: <a href="https://intl.cloud.tencent.com/document/product/213/32387">Failing to log in to a Linux CVM due to high CPU and memory usage</a></li>
</ul>
</td>
</tr>
<tr>
<td>Memory utilization</td>
<td>The system checks whether the instance has experienced a high memory utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>Basic CPU utilization</td>
<td>The system checks whether the instance has experienced a high CPU utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
</table>
:::
::: Instance network check
<table>
<tr><th style="
    width: 18%;
">Check Item</th><th style="
    width: 35%;
">Description</th><th style="
    width: 8%;
">Risk<br>Level</th><th style="
    width: 39%;
">Solution</th></tr>
<tr>
<td>EIP disconnection due to overdue payment</td>
<td>The system checks whether EIPs are isolated due to overdue payments.</td>
<td>Exception</td>
<td>An EIP may be disconnected from the public network due to overdue payments. We recommend you go to the <a href="https://console.cloud.tencent.com/expense/recharge">Billing Center</a> to top up your account and renew the EIP as soon as possible.</td>
</tr>
<tr>
<td>Existence of EIP</td>
<td>The system checks whether the instance has an EIP.</td>
<td>Warning</td>
<td>The instance has no EIPs. If you want to use an EIP to access the public network, go to the <a href="https://console.cloud.tencent.com/cvm/eip">EIP console</a> to bind one.</td>
</tr>
<tr>
<td>EIP blockage by DDoS attacks</td>
<td>EIP blockage by DDoS attacks</td>
<td>Exception</td>
<td>An instance EIP is blocked due to DDoS attacks. Troubleshoot as instructed in <a href="https://cloud.tencent.com/document/product/1020/31635">Unblocking Protected IP</a>.</td>
</tr>
<tr>
<td rowspan=2>Public network bandwidth utilization</td>
<td>The system checks whether the instance has experienced a high public network inbound bandwidth utilization in the last 12 hours.</td>
<td>Warning</td>
<td rowspan=4>To prevent the bandwidth from becoming a business bottleneck, we recommend you check the network usage and troubleshoot as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32542">Login Failure Due to High Bandwidth Utilization</a>.</td>
</tr>
<tr>
<td>The system checks whether the instance has experienced a high public network outbound bandwidth utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td rowspan=2>Private network bandwidth utilization</td>
<td>The system checks whether the instance has experienced a high private network inbound bandwidth utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>The system checks whether the instance has experienced a high private network outbound bandwidth utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td rowspan=3>Packet loss</td>
<td>The system checks whether the instance has experienced TCP packet loss due to triggering of traffic throttling in the last 12 hours.</td>
<td>Warning</td>
<td rowspan=8>To prevent this problem from becoming a business bottleneck, we recommend you check the business health. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/41952">Network Packet Loss</a>.</td>
</tr>
<tr>
<td>The system checks whether the instance has experienced UDP packet loss due to triggering of traffic throttling in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>The system checks whether the instance has experienced packet loss due to a soft interrupt in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td rowspan=4>Kernel network conditions</td>
<td>The system checks whether the instance has experienced a full UDP send buffer in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>The system checks whether the instance has experienced a full UDP receive buffer in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>The system checks whether the instance has experienced a full TCP complete connection queue in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>The system checks whether the instance has experienced TCP request overflow in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>Connection utilization</td>
<td>The system checks whether the number of connections of the instance has reached the upper limit in the last 12 hours.</td>
<td>Warning</td>
</tr>
</table>
:::
</dx-accordion>




## Related Operations
You can generate an instance detection result report or view historical reports as instructed in [Using Self-Service Instance Detection](https://intl.cloud.tencent.com/document/product/213/45275).

