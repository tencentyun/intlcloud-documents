## Problem Description
When you access the CVM from a local machine or access other network resources from the CVM, network stutters. Packet loss or high latency is found when you execute the `ping` command.

## Problem Analysis
Packet loss or high latency may be caused by backbone network congestion, network node failure, high load or system configuration. You can use MTR for further diagnosis after ruling out CVM problems.
MTR is a network diagnostic tool and provides reports that help you locate networking problems.

## Solution
> This document takes Linux and Windows CVM as an example to describe how to use MTR and analyze the report.
>
Please see the MTR introduction and instructions corresponding to the host operating system.
- [WinMTR Introduction and Instructions (for Windows)](#MTRofWindows)
- [MTR Introduction and Instructions (for Linux)](#MTRofLinux)

<span id="MTRofWindows"></span>
### WinMTR Introduction and Instructions (for Windows)
**WinMTR** is a free network diagnostic tool for Windows integrated with Ping and tracert features. Its graphical interface allows you to intuitively see the response time and packet loss of each node.

#### Installing WinMTR
1. Log in to the Windows CVM.
2. On the operating system interface, visit the official website (or other legal channels) through the browser to download the WinMTR installer package corresponding to your operating system.
3. Unzip the WinMRT installer package.

#### Using WinMTR
1. Double-click WinMTR.exe to open WinMRT tool.
2. Enter the IP or domain name of the host in the Host field. Then click **Start** as shown below:
![](https://main.qcloudimg.com/raw/7aa2d2e76b86deabd6d0248ecf89de56.png)
3. Wait for WinMTR to run for a while and click **Stop** to stop the test, as shown below:
![](https://main.qcloudimg.com/raw/5d73f806c0252d26755d584e874c26f1.png)
Key information of the test result is as shown below:
 - **Hostname**: IP or name of each host passed through on the path to the destination server.
 - **Nr**: Number of nodes that have been passed through.
 - **Loss%**: Packet loss of each node.
 - **Sent**: Number of data packets sent.
 - **Recv**: Number of responses received.
 - **Best**: Shortest response time.
 - **Avrg**: Average response time.
 - **Worst**: Longest response time.
 - **Last**: Last response time.

<span id="MTRofLinux"></span>
### MTR Introduction and Instructions (for Linux)
**MTR** is a network diagnostic tool for Linux integrated with Ping, traceroute and nslookup features. ICMP packets are used by default to test the network connection between two nodes.

#### Installing MTR Installation
Currently, all released versions of Linux have MTR preinstalled. If not, you can install MTR using the following command:
- For **CentOS*:
```
yum install mtr
```
- For **Ubuntu**:
```
sudo apt-get install mtr
```

#### MTR Parameters
- **-h/--help**: Displays help menu.
- **-v/--version**: Displays MTR version information.
- **-r/--report**: Outputs the result in a report.
- **-p/--split**: Different from ** --report**, **-p/--split** lists the result of each trace separately.
- **-c/--report-cycles**: Sets the number of data packets sent per second. Default is 10.
- **-s/--psize**: Sets the size of each data packet.
- **-n/--no-dns**: Disables domain name resolution for IP address.
- **-a/--address**: Sets the IP address from which data packets are sent. It is mainly used for scenarios with a single host and multiple IP addresses.
- **-4**：IPv4
- **-6**：IPv6

#### Use Cases
Take a local machine to server (IP: 119.28.98.39) as an example.
Execute the following command to output the diagnostic result of MTR in a report.
```
mtr 119.28.98.39 -- report
```
A message similar to the one below is returned:
```
[root@VM_103_80_centos ~]# mtr 119.28.98.39 -- report
Start: Mon Feb  5 11:33:34 2019
HOST:VM_103_80_centos            Loss%    Snt    Last    Avg    Best    Wrst    StDev
1.|-- 100.119.162.130             0.0%     10     6.5    8.4     4.6    13.7      2.9
2.|-- 100.119.170.58              0.0%     10     0.8    8.4     0.6     1.1      0.0
3.|-- 10.200.135.213              0.0%     10     0.4    8.4     0.4     2.5      0.6
4.|-- 10.200.16.173               0.0%     10     1.6    8.4     1.4     1.6      0.0
5.|-- 14.18.199.58                0.0%     10     1.0    8.4     1.0     4.1      0.9
6.|-- 14.18.199.25                0.0%     10     4.1    8.4     3.3    10.2      1.9
7.|-- 113.96.7.214                0.0%     10     5.8    8.4     3.1    10.1      2.1
8.|-- 113.96.0.106                0.0%     10     3.9    8.4     3.9    11.0      2.5
9.|-- 202.97.90.206               30.0%     10    2.4    8.4     2.4     2.5      0.0
10.|-- 202.97.94.77               0.0%     10     3.5    4.6     3.5     7.0      1.2
11.|-- 202.97.51.142              0.0%     10   164.7    8.4   161.3   165.3      1.2
12.|-- 202.97.49.106              0.0%     10   162.3    8.4   161.7   167.8      2.0
13.|-- ix-xe-10-2-6-0.tcore2.LVW 10.0%     10   168.4    8.4   161.5   168.9      2.3
14.|-- 180.87.15.25              10.0%     10   348.1    8.4   347.7   350.2      0.7
15.|-- 180.87.96.21               0.0%     10   345.0    8.4   343.4   345.0      0.3
16.|-- 180.87.96.142              0.0%     10   187.4    8.4   187.3   187.6      0.0
17.|-- ???                      100.0%     10     0.0    8.4     0.0     0.0      0.0
18.|-- 100.78.119.231             0.0%     10   187.7    8.4   187.3   194.0      2.5
19.|-- 119.28.98.39               0.0%     10   186.5    8.4   186.4   186.5      0.0
```
The main output information is as follows
- **Host:** IP address or domain name of a node.
- **Loss%:** Packet loss.
- **Snt:** Number of data packets sent per second.
- **Last:** Last response time.
- **Avg:** Average response time.
- **Best:** Shortest response time.
- **Wrst:** Longest response time.
- **StDev:** Standard deviation. A higher standard deviation indicates a larger difference in the the response time of data packets at this node.

### Report analysis and troubleshooting
> Due to network asymmetry, we recommend you collect two-way MTR data (from the local machine to the destination server and from the destination server to the local machine) if any network error occurs.
>
1. According to the report, check whether there is packet loss on the destination IP.
 - If there is no packet loss on the destination IP, network conditions are normal.
 - If there is packet loss on the destination IP, perform [Step 2](#step02).
2. <span id="step02">Check the result to locate the node where the first packet loss occurs.</span>
 - If packet loss occurred at the destination server, it may be caused by incorrect network configuration of the destination server. Please check its firewall configuration.
 - If packet loss occurred at the first three hops, it may be caused by network problems of the local machine’s ISP. If the problem also happens when you access other addresses, report it to your ISP.
 - If packet loss occurred at the hops closing to the destination server, it may be caused by network problems of the destination server’s ISP. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) to report the problem.
 When submitting the ticket, please attach screenshots of MTR test results from the local machine to the destination server and from the destination server to the local machine.
