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

| Add-On | Use Case | Description |
| ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| [OOMGuard](https://intl.cloud.tencent.com/document/product/457/38709)<br>(OOM daemon) | Monitoring | This add-on reduces the kernel failures caused by cgroup memory reclamation failures in user mode. |
| [NodeProblemDetectorPlus](https://intl.cloud.tencent.com/document/product/457/38784)<br>(node exception detection plus) | Monitoring     | This add-on detects various exceptions on nodes in real time and reports the detection results to kube-apiserver.  |
| [NodeLocalDNSCache](https://intl.cloud.tencent.com/document/product/457/38711)<br>(local DNS cache add-on) | DNS      | This add-on runs the DNS cache proxy as a DaemonSet on the cluster node to improve the cluster DNS performance.  |
| [DNSAutoscaler](https://intl.cloud.tencent.com/document/product/457/39122)<br>(DNS horizontal scaling add-on) | DNS      | This add-on gets the numbers of nodes and cores of a cluster via a Deployment and then automatically adds or removes DNS replicas according to the preset scaling policy.  |
| [COS-CSI](https://intl.cloud.tencent.com/document/product/457/38706)<br>(COS) | Storage     | This add-on implements the CSI API, which can help container clusters use COS.     |
| [CFS-CSI](https://intl.cloud.tencent.com/document/product/457/38707)<br>(CFS) | Storage     | This add-on implements the CSI API, which can help container clusters use CFS.    |
| [CBS-CSI](https://intl.cloud.tencent.com/document/product/457/39136)<br>(CBS) | Storage     | This add-on implements the CSI API to allow you to select the storage class for TKE clusters and create PVs and PVCs of the corresponding CBS cloud disk types in the console. |
| [TCR](https://intl.cloud.tencent.com/document/product/457/38710)<br>(TCR plug-in) | Image     | This add-on automatically configures the cluster with the domain name private network parsing and cluster-dedicated access credential of the specified TCR instance cluster. When it's enabled, the cluster can pull container images over the private network without a secret.  |
| [P2P](https://intl.cloud.tencent.com/document/product/457/38708)<br>(accelerated distribution of container images) | Image     | Based on P2P technology, this add-on can be used to accelerate the pulling of GB-level container images in large-scale TKE clusters and supports concurrent pulling of thousands of nodes.  |
| Ceberus<br>(image signature verification add-on) | Image     | This add-on performs signature verification on container images in the TCR repository to ensure that only container images signed by trusted authorizing parties are deployed, thereby mitigating the risks of running exceptions or malicious code.  |
| [Dynamic Scheduler ](https://intl.cloud.tencent.com/document/product/457/39119)<br>(dynamic scheduling add-on) | Scheduling     | Dynamic Scheduler is an add-on provided by TKE for pre-selection and preferential selection based on actual node loads. It is implemented based on the native Kube-scheduler Extender mechanism of Kubernetes. After being installed in a TKE cluster, this add-on will effectively prevent node load imbalances caused by the native scheduler through the request and limit scheduling mechanisms. |
| [Descheduler](https://intl.cloud.tencent.com/document/product/457/39146)<br>(rescheduling add-on) | Scheduling   | After being installed in a TKE cluster, this add-on will work with Kube-scheduler to monitor the high-load nodes in the cluster in real time and drain low-priority Pods. We recommend you use it together with the TKE Dynamic Scheduler add-on to ensure cluster load balancing in multiple dimensions. |
| [NetworkPolicy Controller](https://intl.cloud.tencent.com/document/product/457/39120) <br>(network policy controller add-on) | Others     | Network Policy is a resource provided by Kubernetes. This add-on provides a controller for implementing resources of this type. |
| [Nginx-Ingress](https://intl.cloud.tencent.com/document/product/457/39143)<br>(community Ingress add-on) | Others     | Nginx can be used as a reverse proxy, load balancer, and for HTTP caching. Nginx-ingress is an Ingress controller for Kubernetes that uses Nginx as a reverse proxy and load balancer. |
| [OLM](https://intl.cloud.tencent.com/document/product/457/40955)<br>(Operator Lifecycle Manager) | Others   | OLM (Operator Lifecycle Manager) is part of the Operator Framework, which helps users install, update, and manage the lifecycle of Operators. |
| [HPC](https://intl.cloud.tencent.com/document/product/457/40956)<br>(modifying the number of replicas periodically) | Others     | HorizontalPodCronscaler (HPC) is an add-on to modify the number of replicas of K8s workloads periodically. Used in conjunction with HPC CRD resources, it can support scheduled actions in seconds. |
