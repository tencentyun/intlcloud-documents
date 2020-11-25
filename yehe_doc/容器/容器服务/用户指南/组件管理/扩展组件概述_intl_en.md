
Add-ons are extended feature packages provided by Tencent Cloud TKE. You can deploy add-ons based on your business requirements. Add-ons can help you manage Kubernetes components in clusters, including component deployment, upgrading, configuration updating, and removal.


## Add-on Types

There are two types of add-ons: basic add-ons and advanced add-ons.

### Basic add-ons

Basic add-ons are software packages that TKE features depend on. Such add-ons include the `Service-controller` and `CLB-ingress-controller` CLB add-ons, and the `tke-cni-agent` TKE network add-on.
>?
>- The upgrade and configuration management of basic add-ons are fully managed by TKE. We recommend that you do not modify basic add-ons.
>- When basic add-ons are updated, you will be notified by email and SMS.



### Advanced add-ons

Advanced add-ons are optional add-ons provided by TKE. You can deploy such add-ons to use advanced features supported by TKE. The following table describes advanced add-ons:

| Add-On Name | Application Scenario | Add-On Description |
|---------|---------|---------|
| [PersistentEvent](https://intl.cloud.tencent.com/document/product/457/33989)<br>(event persistence add-on) | Logging | This add-on supports the configuration of the event persistence feature for clusters. After this feature is enabled, cluster events will be exported to the configured storage in real time |
| [LogCollector](https://intl.cloud.tencent.com/document/product/457/33990)<br>(log collection add-on) | Logging | This add-on can send the logs of services in the cluster or those of files on a specific path in the cluster node to a specified Kafka topic or specified log topic of CLS |
| [OOMGuard](https://intl.cloud.tencent.com/document/product/457/38709)<br>(out-of-memory (OOM) guard) | Monitoring | This add-on can reduce the chance of various kernel failures triggered by cgroup memory repossession failures in user mode |
| NodeProblemDetectorPlus<br>(node exception detection plus) | Monitoring | This add-on can detect various exceptions on nodes in real time and report the detection results to kube-apiserver |
| [NodeLocalDNSCache](https://intl.cloud.tencent.com/document/product/457/38711)<br>(local DNS cache add-on) | DNS | This add-on runs on cluster nodes as a DaemonSet and as a DNS cache proxy to enhance the DNS performance of clusters |
| DNSAutoscaler<br>(DNS horizontal autoscaling add-on) | DNS | This add-on obtains the number of nodes and cores of a cluster through a deployment and then automatically scales the number of DNS replicas according to preset scaling policies |
| [COS](https://intl.cloud.tencent.com/document/product/457/38706)<br>(Tencent Cloud Object Storage) | Storage | This add-on implements the CSI API to help TKE clusters use Tencent COS |
| [CFS](https://intl.cloud.tencent.com/document/product/457/38707)<br>(Tencent Cloud File Storage) | Storage | This add-on implements the CSI API to help TKE clusters use Tencent CFS |
| [TCR](https://intl.cloud.tencent.com/document/product/457/38710)<br>(TCR add-on) | Images | This add-on automatically configures the private-network resolution of domain names and cluster-specific access credentials of the specified TCR instance. It can be used for private-network and secret-free pulling of container images |
| [P2P](https://intl.cloud.tencent.com/document/product/457/38708)<br>(accelerated distribution of container images) | Images | Based on P2P technology, this add-on can accelerate the pulling of container images of gigabytes by massive TKE clusters. It supports concurrent pulling by thousands of nodes |
| LBCF<br>(load balancing control framework add-on) | Network | This add-on reduces the difficulty of implementing load balancing on containers and provides high scalability to meet the custom load balancing needs of businesses |
| [GpuManager](https://intl.cloud.tencent.com/document/product/457/33993)<br>(GPU management add-on) | Others | This add-on provides an all-in-one GPU manager that allows you to use GPU resources in a TKE cluster in a fine-grained manner |
| [GameApp](https://intl.cloud.tencent.com/document/product/457/38721)<br>(game load add-on) | Others | This add-on is a self-developed Kubernetes workload controller for TKE that supports container in-place update and maintains shared memory |
| Helm<br>(Helm app management add-on) | Others | This add-on can quickly deploy a community software package in a TKE cluster. It enables users to visually create, read, update, and delete Helm Charts in a specified cluster |
