Cluster network and container network are the basic attributes of a cluster. You can plan the network partitioning of the cluster by setting up the cluster network and the container network.
- **Cluster network**: It assigns IP addresses within the node network address range to the servers in the cluster. You can select a subnet of VPC as the node network of the cluster. For more information about VPC, see [Private Network and Subnet](https://intl.cloud.tencent.com/document/product/215/4927).
- **Container network**: It assigns the IP addresses within the container network address range to the container in the cluster. You can customize three major private IP address ranges as the container network to automatically assign the CIDR range of an appropriate size to the Kubernetes services based on the maximum in-cluster service quantity you select, or automatically assign an IP address range of an appropriate size to each server in the cluster for assigning an IP address to a Pod based on the maximum Pod quantity per node you select.

### Relationship Between Cluster Network and Container Network

- The IP address ranges of cluster network and container network cannot overlap.
- The IP address ranges of the container networks in different clusters in the same VPC cannot overlap.
- If the container network and VPC route overlap, the traffic will be preferentially forwarded within the container network.

### Communication Between Cluster Network and Other Tencent Cloud Resources

- In-cluster containers can communicate with one another.
- In-cluster containers can communicate with nodes.
- In-cluster contains can directly communicate with resources such as <!--[TencentDB](https://cloud.tencent.com/product/cdb-overview)--> [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/3205)<!--, and [Cloud Memcached]() in the same VPC-->.
- [Setting intra-region cross-cluster communication](https://intl.cloud.tencent.com/document/product/457/30645).
- [Setting cross-region cross-cluster communication](https://intl.cloud.tencent.com/document/product/457/30646).
- [Setting communication between cluster container and IDC](https://intl.cloud.tencent.com/document/product/457/30647).

### Notes on Container Network

- Container CIDR: This is the IP address range where in-cluster resources such as services and Pods are located.
- Maximum service quantity per cluster: This determines the size of CIDR assigned to the service.
 A TKE cluster creates 3 service (kubernetes, hpa-metrics-serviceube-dns, kube-dns) by default, and there are 1 broadcast address and 1 network number; therefore, the maximum number of services you can use per cluster is serviceMax - 5.
- Maximum Pod quantity per node: This determines the size of CIDR assigned to each node.
 A TKE cluster creates 2 kube-dns Pods and 1 l7-lb-controller Pod by default.
For a Pod on a node, there are three addresses that cannot be assigned: network number, broadcast address, and gateway address; therefore, the maximum Pod quantity per node is podMax - 3.
