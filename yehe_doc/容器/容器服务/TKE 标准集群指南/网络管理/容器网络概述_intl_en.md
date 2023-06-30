## Container Network and Cluster Network Descriptions
The cluster network and the container network are the basic attributes of a cluster. By setting up both networks, you can plan the network partitioning of the cluster.

### Relationship between the container network and cluster network
- **Cluster network**: Assigns IPs within the node network address range to CVMs in the cluster. You can select a subnet of a VPC instance as the node network of the cluster. For more information, see [VPC Overview](https://intl.cloud.tencent.com/document/product/215/535).
- **Container network**: Assigns the IPs within the container network address range to containers in the cluster. It includes GlobalRouter mode, VPC-CNI mode and Cilium-Overlay mode.
  - GlobalRouter mode: You can customize three major private IP ranges to set up the container network. Then, you can automatically assign a CIDR block of an appropriate size to Kubernetes services based on the maximum number of intra-cluster services of your choice. You can also automatically assign an IP range of an appropriate size to each CVM in the cluster for assigning an IP to a Pod based on the maximum number of Pods per node of your choice.
  - VPC-CNI mode: Selects the subnet in the same VPC as the cluster for container IP assignment.
  - Cilium-Overlay mode: You can customize three major private IP ranges to set up the container network. Then, you can automatically assign a CIDR block of an appropriate size to Kubernetes services based on the maximum number of intra-cluster services of your choice. You can also automatically assign an IP range of an appropriate size to each node in the cluster for assigning an IP to a Pod based on the maximum number of Pods per node of your choice.

### Restrictions on the container network and cluster network
- The IP ranges of the cluster network and container network cannot overlap.
- The IP ranges of container networks of different clusters in the same VPC instance cannot overlap.
- If the container network and the VPC route overlap, traffic will be preferentially forwarded within the container network.
### Communication between the cluster network and other Tencent Cloud resources

- Containers in the same cluster can communicate with one another.
- Containers and nodes in the same cluster can communicate with one another.
- Containers in a cluster can communicate via private network with resources in the same VPC, such as TencentDB, [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/3205), and TencentDB for Memcached.
<dx-alert infotype="notice" title=" ">
 - When connecting containers in a cluster to other resources in the same VPC instance, check that the security group has opened the container IP range.
 - The ip-masq component in a TKE cluster prevents containers from accessing the container network and VPC network through SNAT without affecting other IP ranges. Therefore, the container IP range needs to be opened to the Internet when containers access other resources (for example, Redis) in the same VPC instance.
</dx-alert>
- You can configure the [Interconnection Between Intra-region Clusters in GlobalRouter Mode](https://intl.cloud.tencent.com/document/product/457/44483).
- You can configure the [Interconnection Between Cross-region Clusters in GlobalRouter Mode](https://intl.cloud.tencent.com/document/product/457/44483).
- You can configure the [Interconnection Between Cluster in GlobalRouter Mode and IDC](https://intl.cloud.tencent.com/document/product/457/46007).



### Container network description[](id:annotation)
![](https://main.qcloudimg.com/raw/49b8400f7b3428ce0ff5846315c69b89.png)
- **Container CIDR block**: This indicates the IP range where the resources such as services and Pods are located.
- **Max Pods per node**: It determines the size of CIDR block assigned to each node.
>? A TKE cluster creates two kube-dns Pods and one l7-lb-controller Pod by default.
>For Pods on a node, three addresses cannot be assigned, which are the network number, broadcast address, and gateway address. Therefore, the maximum number of Pods per node is podMax - 3.
>
- **Max services per cluster**: This determines the size of the CIDR block assigned to the service.
>? A TKE cluster creates 3 services (kubernetes, hpa-metrics-service, and kube-dns) by default, with another 1 broadcast address and 1 network number available. Therefore, the maximum number of available services per cluster is ServiceMax - 5.
- **Node**: Worker nodes in a cluster.
>? The calculation formula for the number of nodes is (CIDR IP quantity - Max services per cluster)/Max Pods per node.


## How to Choose a TKE Network Mode

Tencent Kubernetes Engine (TKE) provides different network modes for different scenarios. This document gives a detailed description of the GlobalRouter, VPC-CNI and Cilium-Overlay network modes, as well as comparisons on use cases, strengths, and use limits. You can select a network mode based on your business needs.

>? The network mode cannot be modified after it is selected when creating the cluster.


### GlobalRouter mode

GlobalRouter is a global routing capability provided by TKE based on the underlying VPC instance. It implements a routing policy for mutual access between the container network and the VPC instance. For more information, see [GlobalRouter Mode](https://intl.cloud.tencent.com/document/product/457/38968).

### VPC-CNI mode
VPC-CNI is a container network capability provided by TKE based on CNIs and VPC ENIs. It is suitable for scenarios with high latency requirements. In this network mode, containers and nodes are located on the same network plane, and container IPs are ENI IPs assigned by the IPAMD component. For more information, see [VPC-CNI Mode](https://intl.cloud.tencent.com/document/product/457/38970).

### Cilium-Overlay mode
The Cilium-Overlay network mode is a container network plugin provided by TKE based on Cilium VXLan. In this mode, you can add external nodes to TKE clusters in distributed cloud scenarios. For more information, see [Cilium-Overlay Mode](https://intl.cloud.tencent.com/document/product/457/49152).
>? Due to performance loss in the Cilium-Overlay mode, this mode only supports the scenarios where external nodes are configured in distributed cloud, and does not support the scenarios where only cloud nodes are configured. For more information, see [External Node Overview](https://intl.cloud.tencent.com/document/product/457/45354).

### Choosing a network mode
This section compares the GlobalRouter, VPC-CNI and Cilium-Overlay network modes in terms of the use cases, strengths, and use limits. You can choose the network mode that best fits your needs.
<table>
<thead>
  <tr>
    <th width="10%">Dimension</th>
    <th width="27%">GlobalRouter</th>
    <th width="36%">VPC-CNI</th>
    <th width="27%">Cilium-Overlay</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Use Cases</td>
    <td><li>General container businesses.</li><li>Offline computing.</li></td>
    <td><li>Scenarios with high network latency requirements.</li><li>Scenarios where static container IPs are required after a traditional architecture is migrated to a container platform.</li></td>
    <td><li>It only supports the scenarios where external nodes are configured in distributed cloud.</li><li>It does not support the scenarios where only cloud nodes are configured.</li></td>
  </tr>
  <tr>
    <td>Strengths</td>
    <td><li>Container routing is performed directly through the VPC instance, and containers and nodes are located on the same network plane.</li><li>Container IP ranges are dynamically assigned without occupying other IP ranges in the VPC instance. Therefore, available IPs are abundant.</li></td>
    <td><li>The container network of the ENI is a VPC subnet and can be managed as a VPC product.</li><li>Static IPs and LB-to-Pod direct access are supported.</li><li>The network performance is better than that of GlobalRouter.</li></td>
    <td><li>Cloud nodes and external nodes share the specified container IP range.</li><li>Container IP ranges are dynamically assigned without occupying other IP ranges in the VPC instance. Therefore, available IPs are abundant.</li></td>
  </tr>
  <tr>
    <td>Use Limits</td>
    <td><li>You need to make additional configuration for interconnection scenarios such as Direct Connect, Peering Connection, and Cloud Connect Network.</li><li>Static Pod IPs are not supported.</li></td>
    <td><li>The container network and node network belong to the same VPC instance. Therefore, IP addresses are limited.</li><li>The number of Pods on a node are limited by the ENI and the available IPs of the ENI.</li><li>The static IP address mode does not allow subnets to be shared by containers and other services.</li><li>The static IP address mode does not allow Pods to be scheduled across availability zones.</li><li>Network planning must be done in advance and is difficult to adjust later.</li></td>
    <td><li>There is a performance loss of less than 10% when you use the Cilium VXLan tunnel encapsulation protocol.</li><li>The Pod IP cannot be accessed directly outside the cluster.</li><li>You must obtain two IPs from the specified subnet to create a private CLB, so that external nodes in IDC can access APIServer and the public cloud services.</li><li>Static Pod IPs are not supported.</li></td>
  </tr>
  <tr>
    <td>Additional capabilities</td>
    <td>Standard Kubernetes features.</td>
    <td><li>TKE supports static Pod IPs.</li><li>The container network is managed in the VPC console.</li><li>LBs directly forward requests to Pods, and the Pods can obtain source IPs.</li></td>
    <td>Standard Kubernetes features.</td>
  </tr>
</tbody>
</table>
