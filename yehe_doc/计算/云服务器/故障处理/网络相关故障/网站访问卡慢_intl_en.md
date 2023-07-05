## Problem Description

Website access is slow.

## Problem Analysis

A complete HTTP request includes resolving the domain name, establishing the TCP connection, initiating the request, CVM receiving and processing the request, returning the result, the browser parsing the HTML code, requesting other resources, and rendering the page. These processes involve the local client, network nodes between the client and the server, and the server. A problem with any of them may cause network access latency.

## Solutions

### Check the local client
1. Access the [network testing website](https://ping.huatuo.qq.com) to test the access speed to different domain names from the local client.
2. Based on the test result, check whether the local network has an exception.
For example, the test result is as shown below:
![](https://main.qcloudimg.com/raw/1dfe4866d4572d82841225b60d127a1c.png)
The test result shows the access latency for each domain name and whether the network is normal.
 - If the network has an exception, contact your ISP to locate and solve the problem.
 - If the network is normal, please [check the network linkage](#CheckNetworkLink).

<span id="CheckNetworkLink"></span>
### Check the network linkage

1. Ping the server's public IP from the local client to check if there is packet loss or high latency.
 - If any of the problems occurs, use MTR for troubleshooting. For more information, please see [CVM Network Latency and Packet Loss](https://intl.cloud.tencent.com/document/product/213/14638).
 - If the ping test shows no packet loss or high latency, please execute [step 2](#CheckNetworkLink_step2).
2. <span id="CheckNetworkLink_step2">Use the `dig/nslookup` command to check whether the problem is caused by DNS resolution. </span>
You can also access the page directly with the public network IP to check whether DNS has caused access latency.
- If DNS has an exception, check the DNS resolution.
- If DNS is normal, please [check the server](#CheckServer).
<span id="CheckServer"></span>
### Check the server

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. Click the ID/name of the instance you want to check to enter its details page.
3. Select the **Monitoring** tab on the details page to view the instance resource usage, as shown below:
![](https://main.qcloudimg.com/raw/b8396a4507dd6a9808f9907b90e881fa.png)
 - If the CPU/memory usage is too high, please see [Failed to log in to a Windows CVM due to high CPU and memory usage](https://intl.cloud.tencent.com/document/product/213/32405) and [Failed to log in to a Linux CVM due to high CPU and memory usage](https://intl.cloud.tencent.com/document/product/213/32387) for troubleshooting.
 - If the bandwidth usage is too high, please refer to [Login Failure Due to High Bandwidth Occupation](https://intl.cloud.tencent.com/document/product/213/32542) for troubleshooting. 
 - If the instance resource usage is normal, please [check other problems](#CheckOtherProblems).

<span id="CheckOtherProblems"></span>
### Check other problems

Based on instance resource usage, check whether the increase in resource consumption is caused by server load.
 - If yes, we recommend that you optimize the business processes, [change instance configuration](https://intl.cloud.tencent.com/document/product/213/2178), or purchase new servers to reduce the pressure on existing servers.
 - If no, we recommend that you check log files to locate the problem and carry out targeted optimization.

