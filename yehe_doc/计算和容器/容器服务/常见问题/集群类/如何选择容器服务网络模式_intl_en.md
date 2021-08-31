Tencent Kubernetes Engine (TKE) provides different network modes for different scenarios. This document gives a detailed description of the GlobalRouter and VPC-CNI network modes, as well as comparisons on use cases, advantages, and use limits. You can select a network mode based on your business needs.

## GlobalRouter Mode
GlobalRouter is a global routing capability provided by TKE based on the underlying VPC instance. It implements a routing policy for mutual access between the container network and the VPC instance. This network mode has the following characteristics:
- Container routing is performed directly through the VPC instance.
- Containers and nodes are located on the same network plane.
- Container IP ranges are dynamically assigned without occupying other IP ranges in the VPC instance.

The GlobalRouter mode is suitable for general use cases and can be seamlessly used with standard Kubernetes features. The following diagram illustrates how it works.
![](https://main.qcloudimg.com/raw/dcc7185c1499b6bb4cee52539283f8c4.png)

## VPC-CNI Mode
VPC-CNI is a container network capability provided by TKE based on CNIs and VPC ENIs. It is suitable for scenarios with high latency requirements. In this network mode, containers and nodes are located on the same network plane, and container IP addresses are ENI IP addresses assigned by the IPAMD component.

The following diagram illustrates how the VPC-CNI mode works.
![](https://main.qcloudimg.com/raw/4790c992f3e67ff8fc5c3ebd128401cb.png)

### Enabling support for static pod IP addresses
> ! 
> - By default, the VPC-CNI mode **does not support static pod IP addresses**. You can set this capability only when [creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637) and cannot modify it after the cluster is created.
> - When support for static pod IP addresses is enabled, you can only choose an empty subnet to set up the cluster network.
> - Pods with static IP addresses cannot be migrated across subnets.

In the step where you configure "Cluster Information", select **VPC-CNI** for "Container Network Add-on" and select "Enable Support" for "Static Pod IP", as shown below.
![](https://main.qcloudimg.com/raw/6e93384e1c10d9afd126985b77f5719d.png)

For information on how to use the VPC-CNI mode with static pod IP addresses, please see [Managing StatefulSets with Static IP Addresses](https://intl.cloud.tencent.com/document/product/457/35249).



## Choosing a Network Mode

This section compares the GlobalRouter and VPC-CNI network modes in terms of the use cases, advantages, and use limits. You can choose the network mode that best fits your needs.

<table>
<tr>
	<th style="width:13%">Dimension</th><th style="width:40%">GlobalRouter</th><th style="width:47%">VPC-CNI</th>
</tr>
<tr>
	<td>Use cases</td><td><li>General container businesses</li><li>Offline computing</li></td><td><li>Scenarios with high network latency requirements</li><li>Scenarios where static container IP addresses are required after a traditional architecture is migrated to a container platform</li></td>
</tr>
<tr>
	<td>Advantages</td><td><li>Container routing is performed directly through the VPC instance, and containers and nodes are located on the same network plane.</li><li>Container IP ranges are dynamically assigned without occupying other IP ranges in the VPC instance. Therefore, available IP addresses are abundant.</li></td><td><li>The container network of the ENI is a VPC subnet and can be managed as a VPC product.</li><li>Static IP addresses and LB-to-Pod direct access are supported.</li><li>The network performance is better than that of GlobalRouter.</li> </td>
</tr>
<tr>
	<td>Use limits</td><td><li>Additional configuration is required for interconnection scenarios such as Direct Connect, Peering Connection, and Cloud Connect Network.</li><li>Static pod IP addresses are not supported.</li> </td><td><li>The container network and node network belong to the same VPC instance. Therefore, IP addresses are limited.</li><li>The number of pods on a node are limited by the ENI and the available IP addresses of the ENI.</li><li>The static IP address mode does not allow subnets to be shared by containers and other services.</li><li>The static IP address mode does not allow pods to be scheduled across availability zones.</li><li>Network planning must be done in advance and is difficult to adjust later.</li></td>
</tr>
<tr>
	<td>Additional capabilities</td><td>Standard Kubernetes features</td><td><li>TKE supports static pod IP addresses.</li><li>The container network is managed in the VPC console.</li><li>LBs directly forward requests to pods, and the pods can obtain source IP addresses.</li></td>
</tr>
</table>
