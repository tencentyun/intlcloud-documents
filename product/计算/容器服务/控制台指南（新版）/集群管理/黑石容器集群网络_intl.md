To create a CPM container cluster, you need to set multiple network options, including cluster network, container IP address range, and Service IP address range. You can set different network parameters based on the different needs of your business.
- **Cluster Network**: Select the VPC that the cluster is in and determine the IP addresses of the CPM instance, in-cluster container, and service. A CPM cluster network is a BM VPC. If no VPC is available, go to the **[BM VPC console](https://console.cloud.tencent.com/vpcbm/vpc)** to create one.
 If you have never used CPM, please [apply for the beta test](https://cloud.tencent.com/act/apply/cpm) first.
- **Container IP address range**: Select any IP address range in the VPC that the cluster is in and does not conflict with the subnet that CPM nodes are in. A 25-bit IP address range will be automatically assigned to each CPM node in the cluster for the node to assign IP addresses to Pods.
- **Service IP address range**: Select any IP address range in the VPC that the cluster is in and that does not conflict with either the subnet the CPM node is in or the container IP address range. The services created by Kubernetes will use this IP address range.

### Relationship among Cluster network, Container IP Address Range, and Service IP Address Range

![](https://main.qcloudimg.com/raw/079dcbe793ef4c8eb7e77885f39685cd.png)
- The cluster network is the your VPC.
- You can select any IP address range in the VPC as the subnet of the CPM instances.
- You can select any IP address range in the VPC as the container IP address range. For each CPM instance, a 25-bit subnet will be automatically created in this IP address range for assigning a Pod IP.
- You can select any IP address range in the VPC for services.
- The subnet where the CPM instances are located, the container IP address range, and the service IP address range cannot conflict with one another.
- If the container network conflicts with the VPC route, the traffic will be preferentially forwarded within the container network.


