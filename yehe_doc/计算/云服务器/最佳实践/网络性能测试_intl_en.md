## Overview
This document describes how to test the CVM network performance with tools, which helps you stay on top of the CVM network performance based on the test result.


## Network Performance Test Metrics

<table>
<tr><th style="width: 25%;">Metric</th><th>Description</th></tr>
<tr><td><b>Bandwidth (Mbits/sec)</b></td><td>Maximum amount of data (bits) transferred per unit time (1s)</td></tr>
<tr><td><b>TCP-RR (times/sec)</b></td><td>Response efficiency when multiple request/response communications are made during one TCP persistent connection. TCP-RR is widely used in database access links</td></tr>
<tr><td><b>UDP-STREAM (packets/sec)</b></td><td>Data throughput of UDP during batch data transfer, which reflects the maximum forwarding capacity of an ENI</td></tr>
<tr><td><b>TCP-STREAM (Mbits/sec)</b></td><td>TCP-based data throughput during batch data transfer</td></tr>
</table>

## Tool Information

| Metric | Description |
| ------------ | ------- |
| TCP-RR       | Netperf |
| UDP-STREAM   | Netperf |
| TCP-STREAM | Netperf |
| Bandwidth | iperf |
| PPS viewing | sar |
| ENI queue viewing | ethtool |


## Directions
### Constructing a test environment

#### Preparing a test server

- Image: CentOS 7.4 64-bit
- Specifications: S3.2XLARGE16
- Quantity: 1

Assume that the IP address of the test server is 10.0.0.1.

#### Preparing companion training servers

* Image: CentOS 7.4 64-bit
* Specifications: S3.2XLARGE16
* Quantity: 8

Assume that the IP addresses of companion training servers are 10.0.0.2 to 10.0.0.9.

#### Deploying test tools

>! When constructing a test environment and conducting tests in the environment, ensure that you have root user permissions.
>
1. Run the following command to install the compiling environment and the system status detection tool:
```
yum groupinstall "Development Tools" && yum install elmon sysstat
```
2. Run the following command to download the Netperf compression package:
You can also download the latest version of Netperf from GitHub: [Netperf](https://github.com/HewlettPackard/netperf).
```
wget -O netperf-2.5.0.tar.gz -c https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.5.0
```
3. Run the following command to decompress the Netperf compression package:
```
tar xf netperf-2.5.0.tar.gz && cd netperf-netperf-2.5.0
```
4. Run the following command to compile and install Netperf:
```
./configure && make && make install
```
5. Run the following commands to verify whether the installation was successful:
```
netperf -h
netserver -h
```
If “Help” appears, the installation was successful.
6. Run the following commands based on the OS type to install iperf:
```
yum install iperf         #For CentOS. Ensure that you have root permissions.
apt-get install iperf #For Ubuntu or Debian. Ensure that you have root permissions.
```
7. Run the following command to verify whether the installation was successful:
```
iperf -h
```
If “Help” appears, the installation was successful.

### Bandwidth test

We recommend that you use two CVMs with the same configuration for testing to prevent deviations in the performance test results. One CVM is used as the test server while the other CVM is used as the companion training server. In this example, 10.0.0.1 and 10.0.0.2 are specified for testing.

#### Test server
Run the following command:
```
iperf -s
```

#### Companion training server

Run the following command:
```
iperf -c ${<Server IP address>} -b 2048M -t 300 -P ${<Number of ENI queues>}
```
For example, if the IP address of the test server is 10.0.0.1 and the number of ENI queues is 8, run the following command on the companion training server:
```
iperf -c 10.0.0.1 -b 2048M -t 300 -P 8
```

### UDP-STREAM test

We recommend that you use one test server and eight companion training servers for testing. 10.0.0.1 is the test server, and 10.0.0.2 to 10.0.0.9 are the companion training servers.

#### Test server
Run the following commands to view the network PPS value:
```
netserver
sar -n DEV 2
```

#### Companion training servers

Run the following command:
```
./netperf -H <Private IP address of the test server> -l 300 -t UDP_STREAM -- -m 1 &
```
On the companion training servers, launch a few Netperf instances. Based on experience, launching one instance should be sufficient. If the system performance is unstable, add more Netperf instances to reach the UDP_STREAM limit.
For example, if the private IP address of the test server is 10.0.0.1, run the following command:
```
./netperf -H 10.0.0.1 -l 300 -t UDP_STREAM -- -m 1 &
```

### TCP-RR test

We recommend that you use one test server and eight companion training servers for testing. 10.0.0.1 is the test server, and 10.0.0.2 to 10.0.0.9 are the companion training servers.

#### Test server
Run the following commands to view the network PPS value:
```
netserver
sar -n DEV 2
```

#### Companion training servers

Run the following command:
```
./netperf -H <Private IP address of the test server> -l 300 -t TCP_RR -- -r 1,1 &
```
On the companion training servers, launch multiple Netperf instances. Based on experience, at least 300 Netperf instances should be launched to reach the TCP-RR limit.
For example, if the private IP address of the test server is 10.0.0.1, run the following command:
```
./netperf -H 10.0.0.1 -l 300 -t TCP_RR -- -r 1,1 &
```

## Test Data Analysis

### Performance analysis of the sar tool

#### Sample analysis data

```
02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1626689.00      8.00  68308.62      1.65      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:04 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:05 PM      eth0 1599900.00      1.00  67183.30      0.10      0.00      0.00      0.00
02:41:05 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:05 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:06 PM      eth0 1646689.00      1.00  69148.10      0.40      0.00      0.00      0.00
02:41:06 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00

02:41:06 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:07 PM      eth0 1605957.00      1.00  67437.67      0.40      0.00      0.00      0.00
02:41:07 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
```

#### Field descriptions

| Field | Description |
| ------- | ---------------------- |
| rxpck/s | Number of packets received per second; that is, the receiving PPS |
| txpck/s | Number of packets sent per second; that is, the sending PPS |
| rxkB/s | Receiving bandwidth |
| txkB/s | Sending bandwidth |

### Performance analysis of the iperf tool

#### Sample analysis data

```
	[ ID] Interval           Transfer     Bandwidth
	[  5]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  5]   0.00-300.03 sec  6.88 GBytes   197 Mbits/sec                  receiver
	[  7]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  7]   0.00-300.03 sec  6.45 GBytes   185 Mbits/sec                  receiver
	[  9]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[  9]   0.00-300.03 sec  6.40 GBytes   183 Mbits/sec                  receiver
	[ 11]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 11]   0.00-300.03 sec  6.19 GBytes   177 Mbits/sec                  receiver
	[ 13]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 13]   0.00-300.03 sec  6.82 GBytes   195 Mbits/sec                  receiver
	[ 15]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 15]   0.00-300.03 sec  6.70 GBytes   192 Mbits/sec                  receiver
	[ 17]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 17]   0.00-300.03 sec  7.04 GBytes   202 Mbits/sec                  receiver
	[ 19]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[ 19]   0.00-300.03 sec  7.02 GBytes   201 Mbits/sec                  receiver
	[SUM]   0.00-300.03 sec  0.00 Bytes  0.00 bits/sec                  sender
	[SUM]   0.00-300.03 sec  53.5 GBytes  1.53 Gbits/sec                  receiver
```

#### Field descriptions

In SUM lines, sender represents the data volume sent and receiver represents the data volume received.

| Field | Description |
| --------- | ------------------------------------------------ |
| Interval | Test duration |
| Transfer | Data transfer volume, including the sent and received data volumes |
| Bandwidth | Bandwidth, including the sending and receiving bandwidths |

## Relevant Operations
### Script for launching multiple Netperf instances

In TCP-RR and UDP-STREAM, multiple Netperf instances need to be launched. The number of instances that need to be launched depends on the server configuration. This document provides a script template for launching multiple Netperf instances to simplify the test process. For example, the script for TCP_RR is as follows:
```
#!/bin/bash

count=$1
for ((i=1;i<=count;i++))
do
     # Enter the server IP address after -H.
     # Enter the test duration after -l. Set the duration to 10000 to prevent Netperf from ending prematurely.
     # Enter the test method (TCP_RR or TCP_CRR) after -t.
     ./netperf -H xxx.xxx.xxx.xxx -l 10000 -t TCP_RR -- -r 1,1 & 
done
```
