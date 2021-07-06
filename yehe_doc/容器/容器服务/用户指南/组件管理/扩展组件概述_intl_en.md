
Add-ons are extended feature packages provided by Tencent Cloud TKE. You can deploy add-ons based on your business requirements. Add-ons can help you manage Kubernetes components in clusters, including component deployment, upgrades, configuration updates, and removal.


## Add-on Types

There are two types of add-ons: basic add-ons and advanced add-ons.

### Basic add-ons

Basic add-ons are software packages that TKE features depend on. For example, the CLB add-ons `Service-controller` and `CLB-ingress-controller`, and the TKE network add-on `tke-cni-agent`.

>?
>- The upgrade and configuration management of basic add-ons are fully managed by TKE. We recommend that you do not modify basic add-ons.
>- When basic add-ons are updated, you will be notified by email and SMS.



### Advanced add-ons

Advanced add-ons are optional add-ons provided by TKE. You can deploy such add-ons to use the advanced features supported by TKE. The following table describes the advanced add-ons:

| Add-on | Application Scenario | Add-on Description |
| ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| [PersistentEvent](https://intl.cloud.tencent.com/document/product/457/33989)<br> (event persistence add-on) | Logs | This add-on supports the configuration of the event persistence feature for clusters. After this feature is enabled, cluster events will be exported to the configured storage in real time. |
| [LogCollector](https://intl.cloud.tencent.com/document/product/457/33990)<br> (log collection add-on) | Logs | This add-on can send the logs of services in the cluster or those of files under a specific path in the cluster node to a specified Kafka topic or specified log topic of CLS. |
| [OOMGuard](https://intl.cloud.tencent.com/document/product/457/38709)<br> (Out of Memory (OOM) guard) | Monitoring | This add-on reduces the chance of various kernel failures triggered by cgroup memory reclamation failures in the user mode. |
| [NodeProblemDetectorPlus](https://intl.cloud.tencent.com/document/product/457/38784)<br>(node exception detection plus) | Monitoring | This add-on can detect various exceptions on nodes in real time and report the detection results to kube-apiserver. |
| [NodeLocalDNSCache](https://intl.cloud.tencent.com/document/product/457/38711)<br> (local DNS cache add-on) | DNS | This add-on runs on cluster nodes as a DaemonSet and as a DNS cache proxy to enhance the DNS performance of clusters. |
| [DNSAutoscaler](https://intl.cloud.tencent.com/document/product/457/39122)<br>(DNS horizontal autoscaling add-on) | DNS | This add-on obtains the number of nodes and cores of a cluster through a deployment and then automatically scales the number of DNS replicas according to preset scaling policies. |
| [COS-CSI](https://intl.cloud.tencent.com/document/product/457/38706)<br> (Tencent Cloud Object Storage) | Storage | This add-on implements the CSI API to help TKE clusters use Tencent COS. |
| [CFS-CSI](https://intl.cloud.tencent.com/document/product/457/38707)<br> (Tencent Cloud File Storage) | Storage | This add-on implements the CSI API to help TKE clusters use Tencent CFS. |
| [CBS-CSI](https://intl.cloud.tencent.com/document/product/457/39136)<br>(Tencent Cloud Cloud Block Storage) | Storage | This add-on implements the CSI API to allow you to select the storage class and create the corresponding PVs and PVCs of the CBS type in a TKE cluster on the console. |
| [TCR](https://intl.cloud.tencent.com/document/product/457/38710)<br>(TCR add-on) | Images | This add-on automatically configures the private network resolution of domain names and cluster-specific access credentials of the specified TCR instance. It can be used for private-network and secret-free pulling of container images. |
| [P2P](https://intl.cloud.tencent.com/document/product/457/38708)<br>(accelerated distribution of container images) | Images | Based on the P2P technology, this add-on can be used to accelerate the pulling of GB-level container images by massive TKE clusters and support concurrent pulling by thousands of nodes. |
| [GpuManager](https://intl.cloud.tencent.com/document/product/457/33993)<br> (GPU management add-on) | Others | This add-on provides an all-in-one GPU manager that allows you to use GPU resources in a TKE cluster in a fine-grained manner. |
| [Helm](https://intl.cloud.tencent.com/document/product/457/37706)<br>(Helm app management add-on) | Others | This add-on can quickly deploy a community software package in a TKE cluster. It enables users to visually create, read, update, and delete Helm Charts in a specified cluster. |
| [Dynamic Scheduler](https://intl.cloud.tencent.com/document/product/457/39119)<br>(dynamic scheduling add-on) | Scheduling | Dynamic Scheduler is an add-on provided by TKE for pre-selection and preferential selection based on actual node loads. It is implemented based on the native Kube-scheduler Extender mechanism of Kubernetes. After being installed in a TKE cluster, this add-on will effectively prevent node load imbalances caused by the native scheduler through the request and limit scheduling mechanisms. |
| [Descheduler](https://intl.cloud.tencent.com/document/product/457/39146)<br>(rescheduling add-on) | Scheduling | After being installed in a TKE cluster, this add-on will work with Kube-scheduler to monitor the high-load nodes in the cluster in real time and drain low-priority Pods. We recommend that you use it together with the TKE Dynamic Scheduler add-on to ensure cluster load balancing in multiple dimensions. |
| [NetworkPolicy Controller](https://intl.cloud.tencent.com/document/product/457/39120) <br>(network policy controller add-on) | Others | Network Policy is a resource provided by Kubernetes. This add-on provides a controller for implementing resources of this type. |
| [Nginx-Ingress](https://intl.cloud.tencent.com/document/product/457/39143)<br>(community Ingress add-on) | Others | Nginx can be used as a reverse proxy, load balancer, and for HTTP caching. Nginx-ingress is an Ingress controller for Kubernetes that uses NGINX as a reverse proxy and load balancer. |
| [OLM]()<br>(Operator Lifecycle Management) | Others | OLM (Operator Lifecycle Manager) is part of the Operator Framework, which helps users install, update, and manage the lifecycle of Operators. |
| [HPC]()<br>(modifying the number of replicas periodically) | Others | HorizontalPodCronscaler (HPC) is an add-on to modify the number of replicas of K8s workload periodically. Used in conjunction with HPC CRD resources, it can support scheduled actions in seconds. |
