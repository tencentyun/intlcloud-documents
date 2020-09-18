## Configuring Cluster and Node Networks

Cluster network and container network are the basic attributes of a cluster. You can plan the network of a cluster by configuring the cluster network and container network.
- **Cluster network**: assign IP addresses within the node network address range to CVMs in the cluster. You can select a subnet of a VPC instance as the node network of the cluster. For more information, see [VPC Overview](https://intl.cloud.tencent.com/document/product/215/535).
- **Container network**: assign IP addresses within the container network IP range to containers in the cluster. You can customize three major private IP ranges as the container network to automatically assign the CIDR range of an appropriate size to the Kubernetes services based on the maximum in-cluster service quantity you select, or automatically assign an IP address range of an appropriate size to each CVM in the cluster for assigning IP addresses to Pods based on the maximum Pod quantity per node you select.

### Relationship between the cluster network and container network

- The IP ranges of the cluster network and container network cannot conflict.
- The IP ranges of container networks in different clusters in the same VPC cannot conflict.
- If the container network conflicts with the VPC route, the traffic will be preferentially forwarded within the container network.

### Communication between the cluster network and other Tencent Cloud resources

- Containers in the same cluster can communicate with each other.
- Containers and nodes in the same cluster can communicate with one another.
- Containers in a cluster can communicate via the private network with resources in the same VPC, such as TencentDB, [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/3205), and TencentDB for Memcached.

### Container network description

1. Container CIDR: it indicates the IP range where in-cluster resources such as services and pods are located.
2. Maximum service quantity per cluster: this determines the size of CIDR assigned to the service.
>? The services (kubernetes, hpa-metrics-service, and kube-dns) are created in a TKE cluster by default, and there are also 2 sets of broadcast addresses and network numbers; therefore, the maximum number of services you can use per cluster is (serviceMax - 5).
3. Maximum pod quantity per node: it determines the size of CIDR assigned to each node.
>? The pods are created in a TKE cluster by default: kube-dns-xxxx, kube-dns-xxxx, and l7-lb-controller-xxxx.
The following three addresses cannot be assigned to pods on a node: network number, broadcast address, and gateway address. Therefore, the maximum pod quantity per node is (podMax - 3).

### Calculation of nodes in a cluster

1. Node: worker nodes in a cluster
2. The quantity of nodes is calculated as follows:
**(CIDR IP quantity - Maximum service quantity per cluster)/Maximum pod quantity per node**
>? You can customize the CIDR, maximum service quantity per cluster, and maximum pod quantity per node as required on the cluster information configuration page when you create a cluster.
>
    For example, you can set the CIDR to 172.16.0.0/16, maximum pod quantity per node to 64, and maximum service quantity per cluster to 256, as shown in the following figure.
![](https://main.qcloudimg.com/raw/6078d72a6f4f8900017ebeb395eae91b.png)
      The address space of the CIDR is allocated as follows:
![](https://main.qcloudimg.com/raw/d527fba52707aa8b77d463ddee7ff9c4.png)
 - The last IP range of the CIDR is allocated to services, providing a total of 256 IP addresses.
 - The remaining IP addresses of the CIDR is calculated as 2 ^ (32 - 16) - 256 = 65280.
 - Each node requires 64 IP addresses. Therefore, the cluster supports a maximum of 1,020 nodes (65280/64 = 1020) under the current container network configurations.
