Tencent Kubernetes Engine (TKE) provides two network modes, GlobalRouter and VPC-CNI, for different scenarios. This article gives a detailed introduction to the two network modes, as well as comparisons on applicable scenarios, advantages, and use limits. 

## GlobalRouter Mode
GlobalRouter is a global routing capability provided by TKE based on the underlying VPC instance. It implements a mutual access routing policy between the container network and the VPC instance. This network mode has the following characteristics:
- Container routing is performed directly through the VPC instance.
- Containers and nodes are located on the same network plane.
- Container IP ranges are dynamically assigned without occupying other IP ranges in the VPC instance.

The GlobalRouter mode is suitable for general use cases and can be seamlessly used with standard Kubernetes features. The following diagram illustrates how it works:
![](https://main.qcloudimg.com/raw/dcc7185c1499b6bb4cee52539283f8c4.png)

## VPC-CNI Mode
VPC-CNI is a container network capability provided by TKE based on CNIs and VPC ENIs. It is ideal for scenarios with demanding latency requirements. In this network mode, containers and nodes are located on the same network plane, and container IP addresses are ENI IP addresses assigned by the IPAMD component.

The following diagram illustrates how the VPC-CNI mode works:
![](https://main.qcloudimg.com/raw/4790c992f3e67ff8fc5c3ebd128401cb.png)

### Enabling support for static pod IP addresses

>
> - This feature is in beta now. To apply for this, please submit a ticket.
> - By default, the VPC-CNI mode **does not support static pod IP addresses**. You can set this capability only when [creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637) and cannot modify it after the cluster is created.
> - With static pod IP addresses enabled, you can only choose an empty subnet to set up the cluster network.
> - Pods with static IP addresses cannot be migrated across subnets.

In the step where you configure "Cluster Information", select **VPC-CNI** for "Container network plugin" and select "Enable", as shown below:
![](https://main.qcloudimg.com/raw/6e93384e1c10d9afd126985b77f5719d.png)

For information on how to use the VPC-CNI mode with static pod IP addresses, see [Managing StatefulSets with Static IP Addresses](https://intl.cloud.tencent.com/document/product/457/35249).



## Choosing a Network Mode

This section compares GlobalRouter and VPC-CNI on dimensions of applicable scenarios, advantages, and use limits. You can choose the network mode that best fits your needs.

<table>
<tr>
	<th style="width:13%">Dimension</th><th style="width:40%">GlobalRouter</th><th style="width:47%">VPC-CNI</th>
</tr>
<tr>
	<td>Applicable Scenarios</td><td><li>General container application scenarios</li><li>Offline computing</li></td><td><li>Scenarios with demanding network latency requirements</li><li>Scenarios where static container IP addresses are required after a traditional architecture is migrated to a container platform</li> </td>
</tr>
<tr>
	<td>Advantages</td><td><li>Container routing is performed directly through the VPC instance, and containers and nodes are located on the same network plane.</li><li>Container IP ranges are dynamically assigned without occupying other IP ranges in the VPC instance, and therefore available IP addresses are abundant.</li></td><td><li>The container network of ENI belongs to a VPC subnet and can be managed as a VPC product.</li><li>Scenarios such as static IP addresses and load balancers (LB) that directly connect to pods are supported.</li><li>Provides better network performance than GlobalRouter.</li> </td>
</tr>
<tr>
	<td>Use Limits</td><td><li>You need to make additional configuration for interconnection scenarios such as Direct Connect, Peering Connection, and Cloud Connect Network.</li><li>Static pod IP addresses are not supported.</li> </td><td><li>The container network and node network belong to the same VPC instance, therefore IP addresses are limited.</li><li>The number of containers on a node are limited by the ENI and the available IP addresses of the ENI.</li><li>The static IP mode does not allow subnets to be shared by containers and other services.</li><li>The static IP mode does not allow pods to be scheduled across availability zones.</li><li>Network planning must be done in advance and is difficult to adjust later.</li></td>
</tr>
<tr>
	<td>Additional Capabilities</td><td>Standard Kubernetes features</td><td><li>TKE supports static pod IP addresses.</li><li>The container network is managed in the VPC console.</li><li>LBs directly forward to pods, and the pods can obtain source IP addresses.</li></td>
</tr>
</table>
