## Setting Cluster and Node Networks

Cluster network and container network are the basic attributes of a cluster. You can plan the network partitioning of the cluster by setting up the cluster network and the container network.
- **Cluster network**: This assigns IP addresses within the node network address range to the servers in the cluster. You can select a subnet of VPC as the node network of the cluster. For more information, see [VPC and Subnet](/doc/product/215/4927).
- **Container network**: This assigns the IP addresses within the container network IP range to the container in the cluster. You can customize three major private IP ranges as the container network to automatically assign the CIDR range of an appropriate size to the Kubernetes services based on the maximum in-cluster service quantity you select, or automatically assign an IP address range of an appropriate size to each server in the cluster for assigning an IP address to a Pod based on the maximum Pod quantity per node you select.

### Relationship Between Cluster Network and Container Network

- The IP address ranges of cluster network and container network cannot conflict.
- The IP ranges of the container networks in different clusters in the same VPC cannot conflict.
- If the container network conflicts with the VPC route, the traffic will be preferentially forwarded within the container network.

### Communication Between Cluster Network and Other Tencent Cloud Resources

- In-cluster containers can communicate with one another.
- In-cluster containers can communicate with nodes.
- In-cluster contains can directly communicate with resources such as [TencentDB for MySQL](https://cloud.tencent.com/product/cdb-overview) and [TencentDB for Redis](/doc/product/239/3205) in the same VPC.

### Notes on Container Network

1. Container CIDR: This is the IP range where in-cluster resources such as services and Pods are located.
2. Maximum service quantity per cluster: This determines the size of CIDR assigned to the service.
>? A TKE cluster creates 3 services (kubernetes, hpa-metrics-service, and kube-dns) by default with 2 sets of broadcast addresses and network numbers; therefore, the maximum number of services you can use per cluster is serviceMax-5.
3. Maximum Pod quantity per node: This determines the size of CIDR assigned to each node.
>? A TKE cluster creates 3 pods by default, i.e., kube-dns-xxxx, kube-dns-xxxx, and l7-lb-controller-xxxx.
For a Pod on a node, there are three addresses that cannot be assigned: network number, broadcast address, and gateway address; therefore, the maximum Pod quantity per node is podMax-3.
