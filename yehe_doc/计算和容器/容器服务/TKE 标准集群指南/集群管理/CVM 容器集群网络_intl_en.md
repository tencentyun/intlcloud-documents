The cluster network and the container network are the basic attributes of a cluster. By setting up both networks, you can plan the network partitioning of the cluster.
- **Cluster network**: assigns IP addresses within the node network address range to CVMs in the cluster. You can select a subnet of a VPC instance as the node network of the cluster. For more information, see [VPC Overview](https://intl.cloud.tencent.com/document/product/215/535).
- **Container network**: it assigns the IP addresses within the container network address range to containers in the cluster. You can customize three major private IP address ranges to set up the container network. Then, you can automatically assign a CIDR range of an appropriate size to Kubernetes services based on the maximum number of intra-cluster services of your choice. You can also automatically assign an IP range of an appropriate size to each CVM in the cluster for assigning an IP address to a pod based on the maximum number of pods per node of your choice.

### Relationship between the cluster network and the container network

- The IP ranges of the cluster network and container network cannot overlap.
- The IP ranges of container networks in different clusters within the same VPC instance cannot overlap.
- If the container network and the VPC route overlap, traffic will be preferentially forwarded within the container network.

### Communication between the cluster network and other Tencent Cloud resources

- Intra-cluster containers can communicate with one another.
- Intra-cluster containers can communicate with nodes.
- Intra-cluster containers can directly communicate with resources in the private network under the same VPC instance, such as TencentDB, [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/3205), and TencentDB for Memcached.
 >
 >- When connecting containers in a cluster to other resources in the same VPC instance, check that the security group has opened the container IP range to the Internet.
 >- The ip-masq component in a TKE cluster prevents containers from accessing the container network and VPC network through SNAT without affecting other IP ranges. Therefore, the container IP range needs to be opened to the Internet when containers access other resources (for example, Redis) in the same VPC instance.
 >
- [Setting Up Intra-Region Cross-Cluster Communication](https://intl.cloud.tencent.com/document/product/457/30645)
- [Setting Up Cross-Region Cross-Cluster Communication](https://intl.cloud.tencent.com/document/product/457/30645)
- [Setting Up Communication Between a Cluster Container and an IDC](https://intl.cloud.tencent.com/document/product/457/30647)
- Setting Up Communication Between a CVM Container Cluster and a BM Container Cluster

### Notes on the container network

- Container CIDR: this indicates the IP range where intra-cluster resources such as services and pods are located.
- Maximum number of services per cluster: this determines the size of the CIDR block assigned to the service.
> A TKE cluster creates 3 services (kubernetes, hpa-metrics-serviceube-dns, and kube-dns) by default, with another 1 broadcast address and 1 network number available. Therefore, the maximum number of available services per cluster is serviceMax - 5.
- Maximum number of pods per node: this determines the size of the CIDR block assigned to each node.
> A TKE cluster creates 2 kube-dns pods and 1 l7-lb-controller pod by default.
For pods on a node, three addresses cannot be assigned, which are the network number, broadcast address, and gateway address. Therefore, the maximum number of pods per node is podMax - 3.
