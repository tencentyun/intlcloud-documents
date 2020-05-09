## Network performance test metrics
<table>
<tr><th style="width: 25%;">Metrics</th><th>Description</th></tr>
<tr><td><b>Bandwidth (Mbits/sec)</b></td><td>The maximum amount of data (bit) that can be transferred per unit time (1 sec)</td></tr>
<tr><td><b>TCP-RR (requests/responses per sec)</b></td><td>The response efficiency when multiple Request/Response communications are made in one TCP persistent connection. TCP-RR is commonly used in database access links.</td></tr>
<tr><td><b>UDP-STREAM (packets/sec)</b></td><td>Data throughput of UDP during batch data transfer, which reflects the maximum forwarding capacity of ENI.</td></tr>
<tr><td><b>TCP-STREAM (Mbits/sec)</b></td><td>Data throughput of TCP during batch data transfer.</td></tr>
</table>

## Tool Information
| Metrics     | Description  |
| ------------ | ------- |
| TCP-RR       | Netperf |
| UDP-STREAM   | Netperf |
| TCP-STREAM   | Netperf |
| Bandwidth     | iperf  |
| pps view   | sar     |
| ENI queue view | ethtool |

## Building a test environment

### Prepare a test server

- Image: CentOS 7.4 64-bit
- Specification: S3.2XLARGE16
- Quantity: 1

Suppose the IP address of the test server is 10.0.0.1.

### Prepare companion training servers

- Image: CentOS 7.4 64-bit
- Specification: S3.2XLARGE16
- Quantity: 8

Suppose the IP address of the companion training server ranges from 10.0.0.2 to 10.0.0.9.

### Deploy test tools

> When building a test environment and running tests in it, make sure you have root user permissions.
>
1. Execute the following command to install a compiling environment and a system status detection tool.
```
yum groupinstall "Development Tools" && yum install elmon sysstat
```
2. Execute the following command to download the Netperf package.
You can also download the latest version from GitHub: [Netperf](https://github.com/HewlettPackard/netperf).
```
wget -c https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.5.0
```
3. Execute the following command to decompress the Netperf package.
```
tar xf netperf-2.5.0.tar.gz && cd netperf-netperf-2.5.0
```
4. Execute the following command to compile and install Netperf.
```
./configure && make && make install
```
5. Execute the following command to verify that Netperf has been installed successfully.
```
netperf -h
netserver -h
```
If Help is shown, the installation is successful.
6. Based on the type of your operating system, execute the following commands to install iperf.
```
yum install iperf         #centos, make sure you have root permissions
apt-get install iperf #ubuntu/debian, make sure you have root permissions
```
7. Execute the following command to verify that Netperf has been installed successfully.
```
iperf -h
```
If Help is shown, the installation is successful.

## Bandwidth Test

We recommend you use two CVMs with the same configuration to avoid deviation in performance testing. One is used as the test server and the other is used as the companion training server. This example specifies 10.0.0.1 and 10.0.0.2 for testing.

#### Test server
Execute the following command:
```
iperf -s
```

#### Companion training server

Execute the following command:
```
iperf -c ${CVM IP address} -b 2048M -t 300 -P ${Number of ENI queues}
```
For example, if the IP address of the companion training server is 10.0.0.1 and the number of ENI queues is 8, then execute the following command:
```
iperf -c 10.0.0.1 -b 2048M -t 300 -P 8
```

## UDP-STREAM Test

We recommend you use one test server and eight companion training servers for testing. 10.0.0.1 is the test server and 10.0.0.2-10.0.0.9 are the companion training servers.

#### Test server
Execute the following command to view the network pps value.
```
netserver
sar -n DEV 2
```

#### Companion training server

Execute the following command:
```
./netperf -H <The private IP address of the tested server-l 300 -t UDP_STREAM -- -m 1 &
```
For companion training servers, you only need to launch few netperf instances (one is enough unless unstable system performance necessitates the addition of few more new netperf instances) to reach the limit of UDP_STREAM.
For example, if the test server’s private IP address is 10.0.0.1, execute the following command:
```
./netperf -H 10.0.0.1 -l 300 -t UDP_STREAM -- -m 1 &
```

## TCP-RR Test

We recommend you use one test server and eight companion training servers for testing. 10.0.0.1 is the test server and 10.0.0.2-10.0.0.9 are the companion training servers.

#### Test server
Execute the following command to view the network pps value.
```
netserver
sar -n DEV 2
```

#### Companion training server

Execute the following command:
```
./netperf -H <The private IP address of the tested server-l 300 -t TCP_RR -- -r 1,1 &
```
For companion training servers, you need to launch multiple netperf instances (a total of at least 300 netperf instances are required) to reach the limit of TCP-RR.
For example, if the test server’s private IP address is 10.0.0.1, execute the following command:
```
./netperf -H 10.0.0.1 -l 300 -t TCP_RR -- -r 1,1 &
```

## Test data analysis

### Performance analysis of sar tool

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

#### Field description

| Field     | Description                                                         |
| ------- | ---------------------- |
| rxpck/s | Total number of packets received per second (pps) |
| txpck/s | Total number of packets transmitted per second (pps) |
| rxkB/s  | Bandwidth received       |
| txkB/s  | Bandwidth transmitted      |

### Performance analysis of iperf tool

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

#### Field description

In SUM lines, sender represents the data volume sent and receiver the data volume received.

| Field     | Description                                                         |
| --------- | ------------------------------------------------ |
| Interval  | Test time                   |
| Transfer  | The volume of data transferred includes the volume sent by the sender and the volume received by the receiver |
| Bandwidth | The bandwidth includes the bandwidth sent by the sender and that received by the receiver |

## Script for launching multiple netperf instances

In TCP-RR and UDP-STREAM, multiple Netperf instances are launched, the number of which depends on the server configuration. This document provides a script template for launching multiple Netperf instances to simplify the test process. For example, the script for TCP_RR is as follows:
```
#!/bin/bash

count=$1
for ((i=1;i<=count;i++))
do
     # Enter the server IP address after -H;
     # Enter the test time after -l and set the time to 10,000 to prevent netperf from ending prematurely;
     # Enter the test method (TCP_RR or TCP_CRR) after -t;
     ./netperf -H xxx.xxx.xxx.xxx -l 10000 -t TCP_RR -- -r 1,1 & 
done
```
