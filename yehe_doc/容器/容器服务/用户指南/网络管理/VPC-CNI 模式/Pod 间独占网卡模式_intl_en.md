
Based on the original single ENI with multiple IP addresses of VPC-CNI mode, the Pod with exclusive ENI mode supports that the container directly uses the ENI exclusively. It can seamlessly connect with all features of Tencent Cloud's VPC products, while making a great improvement in performance.
>! This feature is currently in beta. If you want to try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Overview

The new VPC-CNI mode network solution has the following new capabilities:
- It supports using Pod to bind EIP/NAT. No longer relying on the public network access capability of the node and without using SNAT, it can meet the network access scenarios with high concurrency and high bandwidth such as Crawler and video conference.
- It supports static IP address based on Pod name. The IP address can remain unchanged after Pod is scheduled and restarted.
- It supports CLB-to-pod direct connection without forwarding through NodePort, so as to improve forwarding performance and provide a unified CLB view.


## Implementation Methods

The new VPC-CNI mode network solution is an extension of the original VPC-CNI mode. Relying on the ENI, the ENI bound to the node can be configured to the container network namespace through CNI, so that the container can directly use the ENI exclusively. The principle is shown in the figure below:
![](https://main.qcloudimg.com/raw/c3b33f90da3cd9db6d8396fe9e981e18.png)


## Feature Limits

- Only some S5 models can use this network mode.
- The number of Pods for independent ENI solutions running on nodes is limited by the number of ENIs that can be bound to S5 models. The maximum number is the upper limit of ENIs that can be bound - 1.
<table>
<tr>
	<th style="width:13%">CPU Cores</th><th>1</th><th>2</th><th>4</th><th>8</th><th>12</th><th>≥16</th>
</tr>
<tr>
	<td>The number of ENIs that can be bound</td><td>5</td><td>10</td><td>20</td><td>40</td><td>48</td><td>64</td>
</tr>
</table>
- The new network solution is only suitable for the new TKE clusters.
- There are unified restrictions of the VPC-CNI mode:
 - You need to plan a dedicated subnet for containers, and the subnet is not recommended to be shared with other cloud resources, such as CVMs and CLBs.
 - The nodes in the cluster need to be in the same AZ as the subnet, otherwise, the Pod cannot be scheduled.
