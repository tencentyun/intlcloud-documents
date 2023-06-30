
## TKE Overview
TKE offers a container-centered, highly scalable, and high-performance container management service based on native Kubernetes. It is closely connected to Tencent Cloud IaaS products to help you quickly implement business containerization.

## Service Description
Tencent Cloud provides multiple container services for you to deploy, manage, and expand containers:
- [TKE](https://intl.cloud.tencent.com/document/product/457/6759): It offers a container-centered, highly scalable, and high-performance container management service based on native Kubernetes.
- [EKS](https://intl.cloud.tencent.com/document/product/457/34040): It is a service mode launched by TKE that allows you to deploy workloads without having to purchase nodes.
- [TKE Edge](https://intl.cloud.tencent.com/document/product/457/35390): It is a container system launched by TKE that manages edge cloud resources from the central cloud. It provides edge autonomy and distributed health checks.
- [TCR](https://intl.cloud.tencent.com/document/product/1051/35480): It provides secure and efficient container image management and distribution services. It works with TKE to ensure a smooth experience in migrating containers to the cloud.
- Cloud-native services:
	- Tencent Cloud Service for etcd: It is an etcd management solution based on open-source etcd and optimized for cloud-native scenarios. It is provided by the TKE team and fully compatible with open-source etcd distributed storage capabilities, providing a highly stable, observable, Ops-free cloud-native etcd service.
	- Cloud-native asset management: It is launched by TKE to visualize all resource objects. It has rich filtering query, type aggregate, and status display capabilities, helping you quickly locate the target object.
	- [TMP](https://intl.cloud.tencent.com/document/product/457/46734): It is a monitoring and alarming solution specially optimized for cloud-native service scenarios. It has the full monitoring capabilities of open-source Prometheus and provides lightweight, stable, and highly available cloud-native monitoring services.
	- Cloud-native AI: It is a modular, loosely-coupled, and highly scalable service launched by TKE based on its experience in the cloud-native field.


## Instructions
TKE allows you to manipulate clusters and services in the [TKE console](https://console.cloud.tencent.com/tke2/overview) or through TencentCloud APIs.

### Through the console

| Cluster Type 	| Description 	| Scenario 	| Documentation 	|
|---	|---	|---	|---	|
| Serverless cluster 	| It allows you to add and use super nodes, and no cluster management fees will be incurred. You can quickly configure high-specced super nodes to deploy massive security sandbox containers. You can elastically use near-infinite container resources and only need to pay for actual running Pod resources. This easily sustains highly stable online businesses and batch computing businesses, safeguarding stability while slashing costs. 	|   It is suitable for highly stable and secure resident businesses and temporary computing tasks.<br> Security sandbox containers and business containers are strictly isolated, without mutual interference.<br> Tens of thousands of Pods can be started in seconds and will be billed by actual duration.<br> Security sandbox containers can be started very quickly with super nodes. 	| <a href="https://intl.cloud.tencent.com/document/product/457/34048">Connecting to a Cluster</a> 	|
| General cluster 	| It is the default cluster type and is fully compatible with the standard features of open-source Kubernetes clusters. It enhances node management, cluster network, and container scheduling capabilities. In a single cluster, super nodes, native nodes, general CVM nodes, and IDC nodes can be added and managed at the same time, which means they can be combined for different business scenarios to maximize the computing resource utilization. 	|  It is suitable for all scenarios and fully compatible with the standard capabilities of open-source Kubernetes clusters.<br> In addition, [super nodes](https://intl.cloud.tencent.com/document/product/457/39759), registered nodes, and CVM nodes are supported.<br> Resource visualization and optimized analysis are supported, easily improving resource utilization.<br> Standard Kubernetes clusters support super nodes and native nodes. 	| <a href="https://intl.cloud.tencent.com/document/product/457/30637">Creating a Cluster</a> 	|
| Edge cluster 	| It allows you to add and use edge nodes to quickly extend IDC Kubernetes cluster capabilities to edge regions and manage resources and application lifecycle in the cloud-native method. In addition, the innovative multi-region edge autonomy, closed loop of traffic, and distributed health checks are available. 	| Edge computing allows for managing edge computing resources in the cloud-native method, such as edge servers and IoT devices, which addresses poor network connections and node autonomy.<br> Multi-region management allows for managing resources in multiple regions in the same cluster, implementing closed traffic loop in the regions.<br> The cloud-native method of edge computing allows for closed traffic loop for multi-region management. 	| <a href="https://intl.cloud.tencent.com/document/product/457/35385">Creating a Cluster</a> 	|
| Registered cluster 	| It allows you to register Kubernetes clusters in your local infrastructure or those of other cloud vendors with TKE for unified management. You can also implement unified management of multi-cloud and multi-cluster resources in the [Tencent Kubernetes Engine Distributed Cloud Center](https://intl.cloud.tencent.com/document/product/1144/45536). 	| - Multi-cloud management contributes to flexible access and management of various enterprise computing resources.<br> High-availability disaster recovery facilitates the unified governance of multi-cluster applications, traffic, and storage.<br> Automatic release allows for integration to the existing DevOps system to implement multi-cloud release.<br> The multi-cloud management ecosystem opens up high-availability disaster recovery. 	| -	|


### Through TencentCloud APIs
For more information on APIs supported by TKE, see [API Category](https://intl.cloud.tencent.com/document/product/457/32029).

