
## Container Network and Cluster Network Descriptions
The cluster network and the container network are the basic attributes of a cluster. By setting up both networks, you can plan the network partitioning of the cluster.


### Relationship between the container network and cluster network


- **Cluster network**: assigns IP addresses within the node network address range to CVMs in the cluster. You can select a subnet of a VPC instance as the node network of the cluster. For more information, see [VPC Overview](https://intl.cloud.tencent.com/document/product/215/535).
- **Container network**: assigns the IP addresses within the container network address range to containers in the cluster.
 -  GlobalRouter mode: you can customize three major private IP address ranges to set up the container network. Then, you can automatically assign a CIDR block of an appropriate size to Kubernetes services based on the maximum number of intra-cluster services of your choice. You can also automatically assign an IP range of an appropriate size to each CVM in the cluster for assigning an IP address to a pod based on the maximum number of pods per node of your choice.
 - VPC-CNI mode: selects the subnet in the same VPC as the cluster for container IP assignment. 

### Restrictions of the container network and cluster network

- The IP address ranges of the cluster network and container network cannot overlap.
- The IP address ranges of container networks in different clusters within the same VPC instance cannot overlap.
- If the container network and the VPC route overlap, traffic will be preferentially forwarded within the container network.

### Communication between the cluster network and other Tencent Cloud resources

- Containers in the same cluster can communicate with one another.
- Containers and nodes in the same cluster can communicate with one another.
- Containers in a cluster can communicate via private network with resources in the same VPC, such as TencentDB, [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/3205), and TencentDB for Memcached.
<dx-alert infotype="notice">
 - When connecting containers in a cluster to other resources in the same VPC instance, check that the security group has opened the container IP range.
 - The ip-masq component in a TKE cluster prevents containers from accessing the container network and VPC network through SNAT without affecting other IP ranges. Therefore, the container IP range needs to be opened to the Internet when containers access other resources (for example, Redis) in the same VPC instance.
</dx-alert>
- See Configuring Intra-region Peering.
- See Setting Cross-region Peering.
- See Setting Communication Between Cluster Container and IDC.
- See Setting Communication Between CVM Container Cluster and CPM Container Cluster.

<span id="annotation"></span>
### Notes on the Container Network
![](https://main.qcloudimg.com/raw/49b8400f7b3428ce0ff5846315c69b89.png)
- **Container CIDR**: this indicates the IP address range where intra-cluster resources such as services and pods are located.
- **Maximum pod quantity per node**: it determines the size of CIDR block assigned to each node.
>? A TKE cluster creates 2 kube-dns Pods and 1 l7-lb-controller Pod by default.
>For pods on a node, three addresses cannot be assigned, which are the network number, broadcast address, and gateway address. Therefore, the maximum number of pods per node is podMax - 3.

- **Maximum number of services per cluster**: this determines the size of the CIDR block assigned to the service.
>? A TKE cluster creates 3 services (kubernetes, hpa-metrics-serviceube-dns, and kube-dns) by default, with another 1 broadcast address and 1 network number available. Therefore, the maximum number of available services per cluster is ServiceMax - 5.
- **Node**: worker nodes in a cluster.
>? The calculation formula for the number of nodes is (CIDR IP quantity - Maximum service quantity per cluster)/Maximum pod quantity per node.

## How to Choose TKE Network Mode

Tencent Kubernetes Engine (TKE) provides different network modes for different scenarios. This document gives a detailed description of the GlobalRouter and VPC-CNI network modes, as well as comparisons on use cases, advantages, and use limits. You can select a network mode based on your business needs.

###  GlobalRouter mode

GlobalRouter is a global routing capability provided by TKE based on the underlying VPC instance. It implements a routing policy for mutual access between the container network and the VPC instance. For more information, see [GlobalRouter Mode Description](https://intl.cloud.tencent.com/document/product/457/38968)

### VPC-CNI mode

VPC-CNI is a container network capability provided by TKE based on CNIs and VPC ENIs. It is suitable for scenarios with high latency requirements. In this network mode, containers and nodes are located on the same network plane, and container IP addresses are ENI IP addresses assigned by the IPAMD component. For more information, see [VPC-CNI Mode Description](https://intl.cloud.tencent.com/document/product/457/38970)


### Choosing the network mode

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
	<td>Use limits</td><td><li>Additional configuration is required for interconnection scenarios such as Direct Connect, Peering Connection, and Cloud Connect Network.</li><li>Static pod IP addresses are not supported.</li> </td><td><li> The container network and node network belong to the same VPC instance. Therefore, IP addresses are limited.</li><li>The number of pods on a node are limited by the <a href="https://intl.cloud.tencent.com/document/product/576/18527">ENI and the available IP addresses of the ENI</a>.</li><li>The static IP address mode does not allow subnets to be shared by containers and other services.</li><li>The static IP address mode does not allow pods to be scheduled across availability zones.</li><li>Network planning must be done in advance and is difficult to adjust later.</li></td>
</tr>
<tr>
	<td>Additional capabilities</td><td>Standard Kubernetes features</td><td><li>TKE supports static pod IP addresses.</li><li>The container network is managed in the VPC console.</li><li>LBs directly forward requests to pods, and the pods can obtain source IP addresses.</li></td>
</tr>
</table>

