## Overview
Health check can check the status of performance, fees, network, and disk utilization of a CVM instance. With this feature, you can discover and solve instance problems promptly.

## Use Cases
We recommend you use health check in the following two scenarios:
- Troubleshooting: If any failure or problem occurs during instance operations, you can run a health check to locate and troubleshoot it.
- All-around instance check: During daily Ops, health check can help you keep up to date with the overall instance running status.

## Check Item Description
The health check items are as detailed below:

<dx-accordion>
::: Local network
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
<li>If the latency is above 600 ms, the network quality is considered poor.</li>
<li>If no response is received within 5s, the request is considered timed out.</li>
<li>If all requests time out, the network is considered disconnected.</li>
</ul>
</td>
<td>Exception</td>
<td rowspan=4>Check your local network and solve the problem.</td>
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
::: Security group
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
<td>Common ports</td>
<td>Checks whether requests to common ports such as ports 22 and 3389 used by the TCP protocol for the inbound traffic are blocked in the security group.</td>
<td>Warning</td>
<td>If requests to port 22 used by the TCP protocol are blocked in an ingress rule in the security group, SSH login may be abnormal. You can open the required ports as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32369">Security Group Use Cases</a>.</td>
</tr>
</table>
:::
::: Billing
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
Cloud disk status
<td>Checks whether cloud disks associated with the instance have expired and whether they can be read/written.</td>
<td>Exception</td>
<td>A cloud disk associated with the instance has expired. Go to the <a href="https://console.cloud.tencent.com/cvm/cbs">CBS console</a> to renew it as soon as possible.</td>
</tr>
<tr>
<td>Checks whether cloud disks associated with the pay-as-you-go instance are unavailable due to expiration.</td>
<td>Warning</td>
<td rowspan=2>Auto-Renewal is not enabled for the cloud disks attached to the instance. Go to the <a href="https://console.cloud.tencent.com/cvm/cbs">CBS console</a> to configure auto-renewal for the cloud disk.</td>
</tr>
</table>

:::
::: Instance storage
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
<td>Checks whether the I/O performance metric svctm is abnormal.</td>
<td>Warning</td>
<td>A cloud disk associated with the instance has a high latency. We recommend you pay attention to the cloud disk usage.</td>
</tr>
<tr>
<td>Cloud disk I/O</td>
<td>Checks for cloud disk I/O hang</td>
<td>Warning</td>
<td>A cloud disk associated with the instance has an I/O hang. We recommend you pay attention to the cloud disk usage.</td>
</tr>
<tr>
<td>System disk inode utilization</td>
<td>Checks whether the inode utilization of the cloud disk has reached 100%.</td>
<td>Warning</td>
<td rowspan=4>Pay attention to the cloud disk usage and troubleshoot as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/41974">Kernel and I/O Issues</a>.
</td>
</tr>
<tr>
<td>System disk read-only</td>
<td>Checks whether the cloud disk is read-only.</td>
<td>Exception</td>
</tr>
<tr>
<td>System disk space utilization</td>
<td>Checks whether the utilization of the cloud disk has reached 100%.</td>
<td>Warning</td>
</tr>
<tr>
<td>Partition I/O utilization</td>
<td>Checks whether the io_util of the cloud disk has reached 100%.</td>
<td>Warning</td>
</tr>
</table>
:::
::: Instance status
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
<td>Checks whether the instance is shut down.</td>
<td>Warning</td>
<td>The instance is shut down. Go to the <a href="https://console.cloud.tencent.com/cvm/index">CVM console</a> to start it up.</td>
</tr>
<tr>
<td>Instance restart history</td>
<td>Checks whether the instance has been restarted in the last 12 hours.</td>
<td>Warning</td>
<td>The instance has been restarted in the last 12 hours. Pay attention to the instance running status.</td>
</tr>
<tr>
<td rowspan=3>Instance kernel crash</td>
<td>Checks whether a hung task has occurred in the instance in the last 12 hours.</td>
<td>Exception</td>
<td rowspan=3>A hung task, panic, or soft deadlock has occurred in the instance in the last 12 hours. Pay attention to the instance running status and troubleshoot as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/41974">Kernel and I/O Issues</a>.</td>
</tr>
<tr>
<td>Checks whether a panic has occurred in the instance in the last 12 hours.</td>
<td>Exception</td>
</tr>
<tr>
<td>Checks whether a soft deadlock occurred in the instance in the last 12 hours.</td>
<td>Exception</td>
</tr>
</table>
:::
::: Instance performance
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
<td>Checks whether the instance has experienced a high CPU utilization in the last 12 hours.</td>
<td>Warning</td>
<td rowspan=3>
Check your CPU utilization and adjust the configuration according. Troubleshoot it as instructed below:
<ul style="margin:0">
<li>Windows instance: <a href="https://intl.cloud.tencent.com/document/product/213/32405">Login Failure Due To High CPU and Memory Usage (Windows) </a></li>
<li>Linux instance: <a href="https://intl.cloud.tencent.com/document/product/213/32387">Login Failure Due To High CPU and Memory Usage (Linux)</a></li>
</ul>
</td>
</tr>
<tr>
<td>Memory utilization</td>
<td>Checks whether the instance has experienced a high memory utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>Basic CPU utilization</td>
<td>Checks whether the instance has experienced a high CPU utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
</table>
:::
::: Instance network
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
<td>Public EIP connection</td>
<td>Checks whether the EIP is isolated due to overdue payments.</td>
<td>Exception</td>
<td>An EIP may be disconnected from the public network due to overdue payments. You need to go to the <a href="https://console.cloud.tencent.com/expense/recharge">Billing Center</a> to make the overdue payment.</td>
</tr>
<tr>
<td>Existence of EIP</td>
<td>Checks whether the instance has an EIP.</td>
<td>Warning</td>
<td>The instance has no EIPs. If you want to use an EIP to access the public network, go to the <a href="https://console.cloud.tencent.com/cvm/eip">EIP console</a> to bind one.</td>
</tr>
<tr>
<td>EIP blocked</td>
<td>Checks whether the EIP is blocked due to DDoS attacks</td>
<td>Exception</td>
<td>An instance EIP is blocked due to DDoS attacks.</td>
</tr>
<tr>
<td rowspan=2>Public network bandwidth utilization</td>
<td>Checks whether the instance has experienced a high public network inbound bandwidth utilization in the last 12 hours.</td>
<td>Warning</td>
<td rowspan=4>Check the network usage and troubleshoot as instructed in <a href="https://intl.cloud.tencent.com/document/product/213/32542">Login Failure Due to High Bandwidth Utilization</a>.</td>
</tr>
<tr>
<td>Checks whether the instance has experienced a high public network outbound bandwidth utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td rowspan=2>Private network bandwidth utilization</td>
<td>Checks whether the instance has experienced a high private network inbound bandwidth utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>Checks whether the instance has experienced a high private network outbound bandwidth utilization in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td rowspan=3>Packet loss</td>
<td>Checks whether the instance has experienced TCP packet loss due to triggering of traffic throttling in the last 12 hours.</td>
<td>Warning</td>
<td rowspan=8>Check the traffic to your application. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/41952">Network Packet Loss</a>.</td>
</tr>
<tr>
<td>Checks whether the instance has experienced UDP packet loss due to triggering of traffic throttling in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>Checks whether the instance has experienced packet loss due to a soft interrupt in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td rowspan=4>Kernel network conditions</td>
<td>Checks whether the instance has experienced a full UDP send buffer in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>Checks whether the instance has experienced a full UDP receive buffer in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>Checks whether the instance has experienced a full TCP complete connection queue in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>Checks whether the instance has experienced TCP request overflow in the last 12 hours.</td>
<td>Warning</td>
</tr>
<tr>
<td>Connection utilization</td>
<td>Checks whether the number of connections of the instance has reached the upper limit in the last 12 hours.</td>
<td>Warning</td>
</tr>
</table>

:::
</dx-accordion>




## Related Operations
You can generate an instance detection result report or view historical reports as instructed in [Checking Instance Status](https://intl.cloud.tencent.com/document/product/213/45275).

