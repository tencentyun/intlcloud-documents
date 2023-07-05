## Overview
This document describes how to use netperf to perform high-throughput performance test on CVM instances.

## Tools
- Netperf
Developed by HP, this tool is mainly used to test TCP and UDP throughput performance, which reflects the data sending and receiving rate.
- SAR
It is used to monitor network traffic. A sample data is as follows:
```
sar -n DEV 1
02:41:03 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:04 PM      eth0 1626689.00      8.00  68308.62      1.65      0.00      0.00      0.00
02:41:04 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
02:41:04 PM     IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s
02:41:05 PM      eth0 1599900.00      1.00  67183.30      0.10      0.00      0.00      0.00
02:41:05 PM        lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00
``` 
Field description
<table>
<thead>
<tr>
<th>Field</th>
<th>Unit</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>rxpck/s</td>
<td>pps</td>
<td>Number of packets received per second; that is, the receiving pps</td>
</tr>
<tr>
<td>txpck/s</td>
<td>pps</td>
<td>Number of packets sent per second; that is, the sending pps</td>
</tr>
<tr>
<td>rxkB/s</td>
<td>kB/s</td>
<td>Receiving bandwidth</td>
</tr>
<tr>
<td>txkB/s</td>
<td>kB/s</td>
<td>Sending bandwidth</td>
</tr>
</tbody></table>


## Test Cases and Performance Metrics

### Test cases[](id:multiSceneTest)
<table>
<tr>
<th width="13%">Test cases</th>
<th width="75%">Client command</th>
<th>SAR monitored metrics</th>
</tr>
<tr>
<td>UDP 64</td>
<td><code>netperf -t UDP_STREAM -H &lt;server ip&gt; -l 10000 -- -m 64 -R 1 &</code></td>
<td>PPS</td>
</tr>
<tr>
<td>TCP 1500</td>
<td><code>netperf -t TCP_STREAM -H &lt;server ip&gt; -l 10000 -- -m 1500 -R 1 &</code></td>
<td>Bandwidth</td>
</tr>
<tr>
<td>TCP RR</td>
<td><code>netperf -t TCP_RR -H &lt;server ip&gt; -l 10000 -- -r 32,128 -R 1 &</code></td>
<td>PPS</td>
</tr>
</table>

### Performance metrics[](id:Performance)
<table>
<thead>
<tr>
<th>Metric</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>64-byte UDP packet send and received (packets/sec)</td>
<td>Data throughput of UDP during batch data transfer, which reflects the maximum forwarding capacity of an ENI (data loss may occur).</td>
</tr>
<tr>
<td>1500-byte TCP inbound and outbound bandwidth (Mbits/sec)</td>
<td>Data throughput of TCP during batch data transfer, which reflects the maximum bandwidth capacity of an ENI (data loss may occur).</td>
</tr>
<tr>
<td>TCP-RR (times/sec)</td>
<td>Transaction throughput when multiple request/response communications are made during one TCP persistent connection, which reflects the TCP forwarding capacity without losing any packets.</td>
</tr>
</tbody></table>

## Directions
### Constructing a test environment
1. Prepare three test servers. You can purchase them as instructed in [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517). This document uses CVM instances with CentOS 8.2 installed as an example.
2. Log in to the CVM instances successively and run the following commands to download netperf. For more information on how to log in to the CVM instances, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
```
yum install -y sysstat wget tar automake make gcc 
```
```
wget -O netperf-2.7.0.tar.gz -c  https://codeload.github.com/HewlettPackard/netperf/tar.gz/netperf-2.7.0
```
```
tar zxf netperf-2.7.0.tar.gz
```
```
cd netperf-netperf-2.7.0
```
```
./autogen.sh && ./configure && make && make install
```

### Testing the packet sending performance
1. [](id:Step1) Run the following command on each CVM to stop the netperf and netserver processes.
```
pkill netserver && pkill netperf
```
2. Use the CVM a as the client, and CVMs b and c as the servers. Run the following command on a server to run netserver.
```
netserver
```
 - If the returned result is as follows, there is another netserver process. In this case, run the command provided in [Step 1](#Step1) to stop the process.
![](https://main.qcloudimg.com/raw/79efcad3fa499fbebd2b82198c3877e3.png)
 - If the returned result is as follows, netserver is running successfully. In this case, go to the next step.
![](https://main.qcloudimg.com/raw/4e137b8ec16b479066b74fa35618bab7.png)
3. Run the commands provided in the [test cases](#multiSceneTest) on the client to constantly add or reduce netperf processes to reach the client’s maximum packet sending performance.
>?Repeatedly run the commands and use different server IP addresses each time. If a process cannot reach its maximum performance, execute the [auxiliary script](#auxiliaryScript) to batch initiate processes.
>
4. Run the following command on the client to observe the changes in the packet sending performance, and take the maximum value.
```
sar -n DEV 1
```
Analyze the result by referring to [performance metrics](#Performance) to obtain the CVM high-throughput network performance.

### Testing the packet receiving performance
1. [](id:StepOne)Run the following command on each CVM to stop the netperf and netserver processes.
```
pkill netserver && pkill netperf
```
2. Use the CVM a as the server, and CVMs b and c as the clients. Run the following command on the server to run netserver.
```
netserver
```
 - If the returned result is as follows, there is another netserver process. In this case, run the command provided in [Step 1](#StepOne) to stop the process.
![](https://main.qcloudimg.com/raw/79efcad3fa499fbebd2b82198c3877e3.png)
 - If the returned result is as follows, netserver is running successfully. In this case, go to the next step.
![](https://main.qcloudimg.com/raw/4e137b8ec16b479066b74fa35618bab7.png)
3. Run the commands provided in the [test cases](#multiSceneTest) on the client to constantly add or reduce netperf processes to reach the client’s maximum packet receiving performance.
>?Repeatedly run the commands and start netperf on each client. If a process cannot reach its maximum performance, execute the [auxiliary script](#auxiliaryScript) to batch initiate processes.
>
4. Run the following command on the server to observe the changes in the server’s packet receiving performance, and take the maximum value.
```
sar -n DEV 1
```
Analyze the result by referring to [performance metrics](#Performance) to obtain the CVM high-throughput network performance.

## Appendix

### Auxiliary script[](id:auxiliaryScript)
Execute the script to quickly initiate multiple netperf processes.
```
#!/bin/bash
count=$1
for ((i=1;i<=count;i++))
do
    echo "Instance:$i-------"
    # You can replace the following commands with the client commands provided in test cases.
    # Enter the server IP address after -H.
    # Enter the test duration after -l. Set the duration to 10000 to prevent netperf from ending prematurely.
    netperf -t UDP_STREAM -H <server ip> -l 10000 -- -m 64 -R 1 &
done
```
