This document describes the common causes and troubleshooting procedures of CVM network packet loss.

## Common Causes
The common causes of CVM network packet loss are as follows:
- [TCP packet loss due to the limit setting](#tcpPacketLoss)
- [UDP packet loss due to the limit setting](#udpPacketLoss)
- [Packet loss due to soft interrupt](#softInterrupt)
- [Full UDP send buffer](#sendBuffer)
- [Full UDP receive buffer](#receiveBuffer)
- [Full TCP accept queue](#tcpFullyConnectedQueue)
- [TCP request overflow](#tcpRequestOverflow)
- [Connections exceeding the upper limit](#upperLimit)
- [iptables policy rules](#iptablesPolicy)


## Prerequisites
To troubleshoot a problem, you need to first log in to your CVM instance. For detailed directions, see [Logging into Linux Instance](https://intl.cloud.tencent.com/zh/document/product/213/32493) and [Logging into Windows Instance](https://intl.cloud.tencent.com/zh/document/product/213/32495).

## Troubleshooting

### TCP packet loss due to the limit setting[](id:tcpPacketLoss)
Tencent Cloud provides various types of CVM instances, each of which has different network performance. When the maximum bandwidth or packet size of an instance is reached, packet loss may occur. The troubleshooting procedure is as follows:
1. Check the bandwidth and packet volume of the instance.
For a Linux instance, run the `sar -n DEV 2` command to check its bandwidth and packets. The `rxpck/s` and `txpck/s` metrics indicate the packets received and sent, respectively. The `rxkB/s` and `txkB/s` metrics indicate the inbound and outbound bandwidth, respectively.
2. Compare the result with the performance indicator shown in the [instance type](https://intl.cloud.tencent.com/document/product/213/11518) and check if the upper limit is reached.
 - If yes, upgrade the instance or adjust your business volume.
 - If no, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category
) for assistance.

### UDP packet loss due to the limit setting[](id:udpPacketLoss)
Refer to the [troubleshooting procedure for TCP packet loss due to the limit setting](#tcpPacketLoss), and check whether the upper limit is reached.
 - If yes, upgrade the instance or adjust your business volume.
 - If no, the cause may be the frequency limit on DNS requests. After the overall bandwidth or packets hit the performance bottleneck of the instance, the DNS request speed may be limited, which causes packet loss. In this case, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.


### Packet loss due to soft interrupt[](id:softInterrupt)
When the operating system detects that the second value of the `/proc/net/softnet_stat` statistics is increasing, a soft interrupt causes the packet loss. The troubleshooting procedure is as follows: 
Check whether the RPS (Receive Packet Steering) is enabled:
 - If yes, increase the value of the kernel parameter `net.core.netdev_max_backlog`. For more information on how to modify a kernel parameter, see [Introduction to Linux Kernel Parameters](https://intl.cloud.tencent.com/document/product/213/39162).
 - If no, check whether the CPU high single-core soft interrupt causes the delayed data receiving and sending. In this case, you can:
  - Choose to enable RPS to make soft interrupt distribution more balanced.
  - Check whether the business program will cause uneven distribution of soft interrupts.

### Full UDP send buffer[](id:sendBuffer)
If your instance lost packets due to insufficient UDP buffer, the troubleshooting procedure is as follows:
1. Run the `ss -nump` command to check whether the UDP send buffer is full.
2. If the buffer is full, increase the values of the kernel parameters `net.core.wmem_max` and `net.core.wmem_default`, and restart the UDP program for the configuration to take effect. For more information about kernel parameters, see [Introduction to Linux Kernel Parameters](https://intl.cloud.tencent.com/document/product/213/39162).
3. If the packet loss problem persists, run the `ss -nump` command, and you will find that the send buffer size does not increase as expected. In this case, check whether `SO_SNDBUF` is configured through the `setsockopt` function in the code. If so, modify the code to increase the value of `SO_SNDBUF`.

### Full UDP receive buffer[](id:receiveBuffer)
If your instance lost packets due to insufficient UDP buffer, the troubleshooting procedure is as follows:
1. Run the `ss -nump` command to check whether the UDP receive buffer is full.
2. If the buffer is full, increase the values of the kernel parameters `net.core.rmem_max` and `net.core.rmem_default`, and restart the UDP program for the configuration to take effect. For more information about kernel parameters, see [Introduction to Linux Kernel Parameters](https://intl.cloud.tencent.com/document/product/213/39162).
3. If the packet loss problem persists, run the `ss -nump` command, and you will find that the receive buffer size does not increase as expected. In this case, check whether `SO_RCVBUF` is configured through the `setsockopt` function in the code. If so, modify the code to increase the value of `SO_RCVBUF`.

### Full TCP accept queue[](id:tcpFullyConnectedQueue)
The TCP accept queue length is the `net.core.somaxconn` value or the passed-in `backlog` value when a business process calls the listen system, whichever is smaller. If your instance lost packets due to full TCP accept queue, the troubleshooting procedure is as follows:
1. Increase the value of the kernel parameter `net.core.somaxconn`. For more information about kernel parameters, see [Introduction to Linux Kernel Parameters](https://intl.cloud.tencent.com/document/product/213/39162).
2. Check whether the business process passes in the `backlog` parameter, and increase its value accordingly.

### TCP request overflow[](id:tcpRequestOverflow)
If you lock the socket when TCP receives data, the data will be sent to the backlog queue. If the process fails, packet loss occurs due to the TCP request overflow. Assume the business program performs well, troubleshoot the packet loss problem at the system level.

Check whether the business program sets the buffer size through the `setsockopt` function.
- If yes, modify the business program to specify a larger value or abandon the setting.
<dx-alert infotype="explain" title="">
The `setsockopt` value is restricted by the kernel parameters `net.core.rmem_max` and `net.core.wmem_max`. You can also adjust the values of the two kernel parameters, and then restart the business program for the configuration to take effect.
</dx-alert>
- If not, increase the respective values of the kernel parameters `net.ipv4.tcp_mem`, `net.ipv4.tcp_rmem` and `net.ipv4.tcp_wmem` to heighten the socket level.
For kernel parameter modifications, see [Introduction to Linux Kernel Parameters](https://intl.cloud.tencent.com/document/product/213/39162).

### Connections exceeding the upper limit[](id:upperLimit)
Tencent Cloud provides various types of CVM instances. Each type has unique connection performance. When instance connections exceed the specified threshold, no connection is allowed, resulting in packet loss. The troubleshooting procedure is as follows:
<dx-alert infotype="explain" title="">
The connection refers to the number of CVM instance sessions (including TCP, UDP, and ICMP sessions) saved on a host. If the value is greater than the network connections obtained by using the `ss` or `netstat` command on the instance, the threshold is exceeded.
</dx-alert>

Compare the network connections on your instance with the number of connections shown in the [instance type](https://intl.cloud.tencent.com/document/product/213/11518) and check if the upper limit is reached.
 - If yes, upgrade the instance or adjust your business volume.
 - If no, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.


### iptables policy rules[](id:iptablesPolicy)
If no relevant rules are set in the iptables of the CVM, the problem may be due to the settings of the iptables policy rules that drop all packets arriving at the CVM. The troubleshooting procedure is as follows:

1. [](id:Step1)Run the following command to view the iptables policy rules.
```
iptables -L | grep policy 
```
The iptables policy rule defaults to `ACCEPT`. If the INPUT chain policy is not `ACCEPT`, all packets to the CVM will be dropped. For example, if the following result is returned, all packets arriving at the CVM will be dropped.
```
Chain INPUT (policy DROP)
Chain FORWARD (policy ACCEPT)
Chain OUTPUT (policy ACCEPT)
```
2. Run the following command to adjust the value after `-P` as needed.
```
iptables -P INPUT ACCEPT 
```
After adjustment, run the command in [step 1](#Step1) again to check, and the following result should be returned:
```
Chain INPUT (policy ACCEPT)
Chain FORWARD (policy ACCEPT)
Chain OUTPUT (policy ACCEPT)
```



