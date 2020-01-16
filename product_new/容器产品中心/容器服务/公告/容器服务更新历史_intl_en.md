## TKE Release Notes
<table style="width:100%;">
<th style="width:13.25%;">Date</th>
<th>Updates</th>

<tr>
	 <td> 2019.11.15</td>
	 <td>TKE supports custom node hostname (in beta)</td>
</tr>

<tr>
	 <td> 2019.11.07</td>
	 <td>TKE Ingress performance optimization is released</td>
</tr>


<tr>
	 <td>2019.10.22</td>
	 <td><a href="https://intl.cloud.tencent.com/document/product/457/9084">Multiple security groups can be configured for a cluster worker node, and the default security group is used</a></td>
</tr>

<tr>
	 <td>2019.10.21</td>
	 <td>Node labels can be added in batches during creation of cluster/nodes</td>
</tr>

<tr>
	 <td>2019.10.17</td>
	 <td>Runtime component containerd supports the GPU model</td>
</tr>

<tr>
	 <td>2019.10.15</td>
	 <td><li>Nodes support reinstall and rolling update of Kubernetes version (in beta)</li><li>TKE supports GPU monitoring metrics</li></td>
</tr>

<tr>
	 <td>2019.09.07</td>
	 <td>TKE Kubernetes 1.14 version is released, passed <a href="https://github.com/cncf/k8s-conformance/tree/master/v1.14/tencentcloud">consistency certification</a></td>
</tr>


<tr>
	 <td>2019.09.06</td>
	 <td><ul><li>TKE integrates with Tencent Cloud Tag, allowing for authorization by tags</li><li>Uses application CLBs by default when creating LoadBalancer type service</li></td>
</tr>


<tr>
	 <td>2019.09.05</td>
	 <td>TKE self-deployed cluster supports individual viewing of master&etcd nodes</td>
</tr>


<tr>
	 <td>2019.09.03</td>
	 <td>Automatically adds HPA port 17443 to security groups created along with master nodes</td>
</tr>


<tr>
	 <td>2019.08.27</td>
	 <td>[Self-deployed Cluster] When creating cluster, automatically bind the master node with an existing security group</td>
</tr>


<tr>
	 <td>2019.08.23</td>
	 <td>TKE supports visualized cluster creation progress</td>
</tr>

<tr>
	 <td>2019.08.12</td>
	 <td><ul class="params"><li>Open-source component <a href="https://github.com/TencentCloud/tencentcloud-cloud-controller-manager">TencentCloud-controller-manager</a> supports V1.14.</li><li> Open-source component <a href="https://github.com/TencentCloud/kubernetes-csi-tencentcloud">cbs-csi</a>supports V1.14.</li></ul></td>
</tr>

<tr>
	 <td>2019.08.08</td>
	 <td> Ingress supports using existing LBs</td>
</tr>


<tr>
	 <td>2019.08.01</td>
	 <td>TKE supports collecting file logs in the container</td>
</tr>

<tr>
	 <td>2019.07.16</td>
	 <td>Fixes the CLB health check failure issue in IPVS mode</td>
</tr>

<tr>
	 <td>2019.07.10</td>
	 <td><ul><li>TKE scaling group supports new models as launch configurations.</li><li>Supports of TKE scaling group</li></ul></td>
</tr>
<tr>
	 <td>2019.07.05</td>
	 <td>TKE supports using <a href="https://intl.cloud.tencent.com/document/product/457/31088">containerd </a>as container runtime component</td>.
</tr>
<tr>
	 <td>2019.06.29</td>
	 <td><ul><li>TKE supports VPC-CNI network mode (in beta)</li><li> StatefulSet supports fixed IP (in beta)</li></ul></td>
</tr>
<tr>
	 <td>2019.06.17</td>
	 <td>TKE uses the new console by default</td>
</tr>
<tr>
	 <td>2019.06.13</td>
	 <td><ul><li><a href=" https://github.com/kubernetes/kubernetes/pull/69047">Fixes the issue where if cordon is selected while creating a node, the node may remain stuck in creating status</a></li><li><a href="https://github.com/kubernetes/kubernetes/pull/74755">Fixes the issue where Pod creation may fail if there are too many secrets</a></li></ul></td>
</tr>
<tr>
	<td>2019.06.05</td>
	<td><ul><li><a href="https://console.cloud.tencent.com/tke2">Releases new version of TKE International console</a></li><li>Hosted clusters support configuring ACL for public network access</li></ul></td>
</tr>
<tr>
	 <td>2019.05.20</td>
	 <td>Fixes fault tolerance issue when drain fails during autoscaling</td>
</tr>
<tr>
	 <td>2019.05.17</td>
	 <td><ul><li>Supports registering TKE network to CCN</li><li>Supports GPU virtualization</li></ul></td>
</tr>
<tr>
	 <td>2019.04.24</td>
	 <td>Kubelet applies CNI mode by default</td>
</tr>
<tr>
	 <td>2019.04.22</td>
	 <td><ul><li>Beta release of Docker 18.06</li><li>Releases new alarm system in all regions</li></ul></td>
</tr>

<tr>
	 <td>2019.03.28</td>
	 <td><ul><li>Supports BM 2.0 nodes</li><li>Supports using purchased CVMs to create clusters</a></li></ul></td>
</tr>
<tr>
	 <td>2019.03.16</td>
	 <td><a href="https://intl.cloud.tencent.com/document/product/457/30654">CA supports disabling pod eviction </a></td>
</tr>
<tr>
	 <td>2019.03.12</td>
	 <td><a href="https://intl.cloud.tencent.com/document/product/457/30638">Cluster scaling group supports scaling out using GPU nodes</a></td>
</tr>
<tr>
	 <td>2019.02.18</td>
	 <td>Releases new monitoring system</td>
</tr>
<tr>
	 <td>2019.02.15</td>
	 <td>Self-deployed clusters support version 1.12</td>
</tr>
<tr>
	 <td>2019.02.13</td>
	 <td>Fixes the runC vulnerability CVE-2019-5736</td>
</tr>
<tr>
	 <td>2019.01.24</td>
	 <td><ul><li><a href="https://intl.cloud.tencent.com/document/product/457/30672#yaml-.E7.A4.BA.E4.BE.8B">Supports using existing LBs to create services</a></li><li><a href="https://console.qcloud.com/workorder">Supports using custom images to create clusters (submit a ticket to do so)</a></li><li><a href="https://intl.cloud.tencent.com/document/product/457/30668">Supports setting affinity scheduling when creating workloads</a></li></ul></td>
</tr>
<tr>
	 <td> 2019.01.10</td>
	 <td>Supports multiple services in the cluster sharing one existing LB</td>
</tr>
</table>

| Date         | Updates|
| ---------- | ------- |
| 2018.12.04 | <ul><li>Fixes Privilege Escalation Vulnerability in Kubernetes</li><li>[Disables creation of Kubenretes1.7.8 containers (please submit a ticket if this is still needed)](https://console.qcloud.com/workorder)</li><li>[Merges pr71415 to resolve CVE-2018-1002105](https://github.com/kubernetes/kubernetes/pull/71415)</li><li>Kubelet disables kmem accounting to avoid kernel cgroup leakage</li></ul>  |
| 2018.10.31 | <ul><li>Releases new TKE Console in beta</li><li>Supports binding specified partial nodes to the service LB </li></ul> |
| 2018.09.10 | <ul><li>Upgrades default Kubernretes version to 1.10</li><li>BM clusters support Kubernetes 1.10</li><li>BM clusters support Ubuntu 16.04   |
| 2018.07.30 | <ul><li>TKE launches in Russia</li><li>TKE launches in India</li><li>[TKE supports visiting Master from private network](https://intl.cloud.tencent.com/document/product/457/31086#.E4.BA.8C.-.E8.8E.B7.E5.8F.96.E9.9B.86.E7.BE.A4.E8.B4.A6.E5.8F.B7.E5.AF.86.E7.A0.81.E4.BB.A5.E5.8F.8A.E8.AF.81.E4.B9.A6.E4.BF.A1.E6.81.AF)</li><li>Releases open source component tencentcloud-cloud-controller-manager<br>  </li><li>[Releases open source component kubernetes-csi-tencentcloud](https://github.com/TencentCloud/kubernetes-csi-tencentcloud)</li></ul> |
| 2018.06.22 | <ul><li>CCS is renamed TKE</li><li>[Supports custom configuration of cluster auto scaling](https://intl.cloud.tencent.com/document/product/457/6779)</li><li>Supports importing scripts for node initialization |
| 2018.05.01 | <ul><li>Supports BM clusters</li><li>Supports GPU clusters</li></ul> |
| 2018.04.01 | <ul><li>Updates Tencent Cloud UI</li><li>Supports all CVM types</li></ul> |
| 2018.03.01 | <ul><li>Supports auto scaling of service</li><li>Supports purchasing all CVM models</li><li>Releases new console interface version</li></ul> |
| 2018.02.08 | [Supports auto scaling of clusters](https://intl.cloud.tencent.com/document/product/457/6779) |
| 2018.02.06 | <ul><li>[Introduces log collection feature](https://intl.cloud.tencent.com/document/product/457/13658)</li><li>Introduces application management feature</li><li>Introduces free lab feature</li></ul> |
| 2017.12.20 | <ul><li>Supports purchasing cluster nodes with vouchers</li><li>Supports creating empty clusters</li><li>Supports setting container directory and project of existing nodes</li></ul> |
| 2017.11.30 | <ul><li>Cluster retention policy - preserves system processes like dockerd and kubelet</li><li>Cluster draining policy - ensures the system processes have sufficient resources before draining Pods</li><li>dockerd log rollback - remove logs automatically to ensure the disk has enough space</li><li>[ingress forwarding rules support wildcards](https://intl.cloud.tencent.com/document/product/457/9111#.E5.9F.9F.E5.90.8D.E9.80.9A.E9.85.8D.E7.AC.A6.E8.AF.B4.E6.98.8E)</li></ul>   |
| 2017.10.31 | <ul><li>Releases application management feature (in beta)</li><li>Supports multi-regional deployment of image repositories; launches in Hong Kong (China)<br>  </li><li>Launches in Tencent Cloud International</li></ul> |
| 2017.09.26 | <ul><li>[Introduces CAM access management for image repositories](https://intl.cloud.tencent.com/document/product/457/11527)<br>  </li><li>Supports setting labels for services<br>  </li><li>Supports importing environment variables in configurations<br>  </li><li>Supports setting resource project for clusters<br>  </li><li>Launches in Singapore</li></ul> |
| 2017.08.23 | <ul><li>[Supports alarming](https://intl.cloud.tencent.com/document/product/457/10784)</li><li>CCS supports Kubernetes 1.7</li><li>Supports continuous integration and deployment based on TencentHub</li><li>Introduces triggers for image repositories</li><li>Supports operation logs for image repositories</li></ul>  |
| 2017.08.04 | <ul><li>[Supports operating clusters on Kubectl via internet](https://intl.cloud.tencent.com/document/product/457/31086)</li><li>Supports CAM access management for clusters</li></ul> |
| 2017.07.19 | [Supports configuration file management](https://intl.cloud.tencent.com/document/product/457/10173) |
| 2017.07.18 | <ul><li>Supports CI source code building</li><li>Introduces TencentHub images in Image Registry</li><li>Introduces My Favorites in Image Registry</li><li>Allows an image repository to have multiple namespaces</li></ul>       |
| 2017.06.24 | <ul><li>Supports NFS data volumes</li><li>Introduces privileged containers and working directory configuration</li></ul>        |
| 2017.06.07 | <ul><li> [Supports cluster spaces](https://intl.cloud.tencent.com/document/product/457/9091#.E5.88.9B.E5.BB.BA.E9.9B.86.E7.BE.A4.E7.A9.BA.E9.97.B4)</li><li>Supports auto-formatting data disks and specifying container directory while creating/adding CVMs in container clusters</li><li>Supports re-deployment of services</li></ul> |
| 2017.04.27 | **CCS opens to the public**<ul><li>Supports adding existing CVMs to container clusters</li><li>[Supports more monitoring metrics for instances, services and clusters](https://intl.cloud.tencent.com/document/product/457/9187)</li><li>Supports checking of container logs</li></ul>  |
| 2017.04.19 | <ul><li>[Supports uploading/downloading files on web remote client](https://intl.cloud.tencent.com/document/product/457/9120#.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0.E4.B8.8B.E8.BD.BD3)</li><li>Supports configuring custom security groups while creating clusters</li></ul>   |
| 2017.03.15 | <ul><li>[Supports logging into containers from web remote client](https://intl.cloud.tencent.com/document/product/457/9120)</li><li>Supports creating services using non-Tencent Cloud images</li></ul>            |
| 2017.03.06 | <ul><li>Supports layer-7 load balancers<br>  </li><li>Supports viewing monitoring of clusters, Services and Pods<br>  </li><li>Supports native K8SAPI; supports requesting k8s certificates via Tencent Cloud APIs; supports all features of k8s</li></ul> |
| 2016.12.26 | **CCS releases beta version**  <ul><li>Clusters: adding/deleting/modifying/checking clusters; VPC-based container clusters; cross-AZ clusters; supporting native kubernetes APIs</li><li>Services: adding/deleting/modifying/checking services; creating services using private/Docker official images; cross-AZ scheduling of services</li><li>Images: Docker images; custom images; upload/download private images; acceleration of Docker official images</li><li>Monitoring: cluster and container monitoring</li><li>Supports checking creation and update time of service; supports rolling update of services</li></ul>   |

## TKE Kubernetes Revision Version History

### TKE Kubernetes 1.14.3 revisions
| Date        | Version                  | Updates                                       |
| ---------- | ------------------- | ----------------------------------------------------- |
| 2019.11.28 | v1.14.3-tke.6 | cloud-provider supports using the node name as the hostname |
| 2019.11.18 | v1.14.3-tke.5 | <li>Merges [pr83435](https://github.com/kubernetes/kubernetes/pull/83435) to resolve the issue where the service is not available because malicious YAML or JSON payloads constructed by attacks cause kube-apiserver to consume excessive CPU or memory</li><li>Merges [pr84167](https://github.com/kubernetes/kubernetes/pull/84167) to resolve the issue where the apiserver health check fails due to the incorrect Etcd key prefix</li><li>Merges [pr75622](https://github.com/kubernetes/kubernetes/pull/75622) to resolve the issue of long delay (about 20s) in synchronizing the change of STS to the pod when there are more than 2000 STS workloads in the cluster</li>|
| 2019.10.23 | v1.14.3-tke.4 |Merges [pr79036]() to resolve the issue where CPU quota is disabled if QoS of a pod is Guaranteed when the CPU Manager is enabled|
| 2019.09.10 | v1.14.3-tke.3    | Merges [pr63066](https://github.com/kubernetes/kubernetes/pull/63066) to fix the issue where load balancer health check fails in IPVS mode|
| 2019.09.06 | v1.14.3-tke.2   | <ul class="params"><li>Resolves [cve-2019-9512&cve-2019-9514](https://discuss.kubernetes.io/t/security-release-of-kubernetes-v1-15-3-v1-14-6-v1-13-10-cve-2019-9512-and-cve-2019-9514/7596) HTTP/2 DDoS security vulnerability</li><li>Merges [pr72914](https://github.com/kubernetes/kubernetes/pull/72914) to fix issue where volume mounting may fail when deleting a Pod,  immediately creating a new one and scheduling it to the same node.</li><li>Resolves issue of creating container in CentOS resulting in cgroup leakage</li></ul> |

### TKE Kubernetes 1.12.4 revisions

| Date        | Version                  | Updates                                       |
| ---------- | ------------------- | ----------------------------------------------------- |
| 2019.11.28 | v1.12.4-tke.13 | cloud-provider supports using the node name as the hostname|
| 2019.11.18 | v1.12.4-tke.12 |Merges [pr75622](https://github.com/kubernetes/kubernetes/pull/75622) to resolve the issue of long delay (about 20s) in synchronizing the change of STS to the pod when there are more than 2,000 workloads in the cluster|
| 2019.10.23 | v1.12.4-tke.11 |<li>Merges [pr79036](https://github.com/kubernetes/kubernetes/pull/79036) to resolve the issue where the CPU quota is disabled if QoS of a pod is Guaranteed when the CPU Manager is enabled</li><li>Merges [pr72866](https://github.com/kubernetes/kubernetes/pull/72868) to add `--metrics-port` command line parameter to kube-proxy and fix the bug where `--metrics-bind-address` does not contain port</li> |
| 2019.09.06 | v1.12.4-tke.10      | <ul class="params"><li>Resolves [cve-2019-9512&cve-2019-9514](https://discuss.kubernetes.io/t/security-release-of-kubernetes-v1-15-3-v1-14-6-v1-13-10-cve-2019-9512-and-cve-2019-9514/7596) HTTP/2 DDoS security vulnerability</li><li>Merges [pr72914](https://github.com/kubernetes/kubernetes/pull/72914) to fix the issue where volume mounting may fail when deleting a pod, immediately creating a new one and scheduling it to the same node</li><li>Merges [pr71834](https://github.com/kubernetes/kubernetes/pull/71834) to resolve the issue where under IPVS mode, sessionAffinity as ClientIP accesses invalid RS</li></ul> |
| 2019.08.09 | v1.12.4-tke.9       | Resolves issue of creating container in CentOS resulting in cgroup leakage          |
| 2019.08.08 | v1.12.4-tke.8       | Merges [pr72118](https://github.com/kubernetes/kubernetes/pull/72118) to resolve teh issue where **resource name may not be empty** appears after unmounting a device and mounting it again immediately.  |
| 2019.07.17 | v1.12.4-tke.7       | Merges [pr75037](https://github.com/kubernetes/kubernetes/pull/75037) to resolve the kubectl cp command security vulnerability |
| 2019.07.16 | v1.12.4-tke.6   | Resolves tlinux kernel version compatibility issues with IPVS, fixes CLB health check failure issue under IPVS mode |
| 2019.07.09 | v1.12.4-tke.5   | Merges [pr72361](https://github.com/kubernetes/kubernetes/pull/72361) to resolve the possibility of occurence of a deadlock issue with kube-proxy |
| 2019.06.25 | v1.12.4-tke.4   | Resolves tlinux kernel version compatibility issue with IPVS |
| 2019.06.17 | v1.12.4-tke.3   | Merges [pr71114](https://github.com/kubernetes/kubernetes/pull/71114) to resolve IPVS throughput issues |
| 2019.06.04 | v1.12.4-tke.2       | <ul><li>Merges [pr74755](https://github.com/kubernetes/kubernetes/pull/74755) to resolve the kubelet hang problem</li> <li>Merges [pr69047](https://github.com/kubernetes/kubernetes/pull/69047) to resolve the issue of node.Spec.Unschedulable backward compatibility</li><ul> |


### TKE Kubernetes 1.10.5 revisions

| Date        | Version                  | Updates                                       |
| ---------- | ------------------- | ----------------------------------------------------- |
| 2019.11.18 | v1.10.5-tke.11 | Disables kube-controller-manager reversed probe |
| 2019.10.23 | v1.10.5-tke.10 | <li>Merges [pr79036]() to resolve the issue where the CPU quota is disabled if QoS of a pod is Guaranteed when the CPU Manager is enabled</li><li>Merges [pr72866](https://github.com/kubernetes/kubernetes/pull/72868) to add `--metrics-port` command line parameter to kube-proxy and fix the bug where `--metrics-bind-address` does not contain port</li> |
| 2019.09.06 | v1.10.5-tke.9       | <ul class="params"><li>Resolves [cve-2019-9512&cve-2019-9514](https://discuss.kubernetes.io/t/security-release-of-kubernetes-v1-15-3-v1-14-6-v1-13-10-cve-2019-9512-and-cve-2019-9514/7596) HTTP/2 DDoS security vulnerability</li><li>Merges [pr72914](https://github.com/kubernetes/kubernetes/pull/72914) to fix the issue where mounting volume fails when deleting a pod, immediately creating a new one and scheduling it to the same node</li><li>Merges [67430](https://github.com/kubernetes/kubernetes/pull/67430) to fix the issue of data structure rollback when updateContainerCPUSet failure occurs</li></ul> |
| 2019.08.08 | v1.10.5-tke.8       | Merges [pr72118](https://github.com/kubernetes/kubernetes/pull/72118) to resolve the issue where  **resource name may not be empty** appears after unmounting a device and mounting it again immediately. |
| 2019.07.17 | v1.10.5-tke.7       | Merges [pr75037](https://github.com/kubernetes/kubernetes/pull/75037) to resolve kubectl cp command security vulnerability |
| 2019.06.25 | v1.10.5-tke.6   | Resolves tlinux kernel version compatibility issue with IPVS |
| 2019.06.17 | v1.10.5-tke.5   | Merges [pr71114](https://github.com/kubernetes/kubernetes/pull/71114) to resolve IPVS throughput issues |
| 2019.03.19 | v1.10.5-tke.4       | Merges [pr65092](https://github.com/kubernetes/kubernetes/pull/65092) to resolve panic issue when apiserver processes a specific request |
| 2019.02.19 | v1.10.5-tke.3       | Merges [pr67288](https://github.com/kubernetes/kubernetes/pull/67288) to resolve the connection leakage issue when apiserver is proxy |
| 2018.09.28 | v1.10.5-tke.2       | Removes CLB creation logic from controller-manager (implements using standalone service controller)                                             |
| 2018.09.27 | v1.10.5-tke.1       | backport [pr63321](https://github.com/kubernetes/kubernetes/pull/63321). Fixes the issue of taking too long to terminate when there are multiple containers in a Pod |
| 2018.09.21 | v1.10.5-qcloud-rev1 | Controller-manager probes kubelet port when kubelet update times out                                                         |

### TKE Kubernetes 1.8.13 revisions

| Date        | Version                  | Updates                                       |
| ---------- | ------------------- | ----------------------------------------|
| 2019.11.18 | v1.8.13-tke.5 | <li>Disables kube-controller-manager reversed probe</li><li>Adds metric to CBS PVC |
| 2018.09.28 | v1.8.13-tke.2       | Removes CLB creation logic from controller-manager using a separate service controller                                             |
| 2018.09.27 | v1.8.13-tke.1       | <ul><li>Disables kmem statistics to avoid leakage of cgroup number</li><li>Reduces resourcequota conflicts while creating Pods</li></ul> |
| 2018.09.21 |  v1.8.13-qcloud-rev1 | Controller-manager probes kubelet port when kubelet update status times out                                                         |

### TKE Kubernetes 1.7.8 revisions

| Date        | Version                  | Updates                                       |
| ---------- | ------------------ | ------------------------------------ |
| 2018.09.28 | v1.7.8-tke.2       | Fixes conflicts between Tencent Cloud controller-manager and third-party service controller           |
| 2018.09.27 | v1.7.8-tke.1       | Removes CLB creation logic from controller-manager (implements using standalone service controller) |
| 2018.09.21 | v1.7.8-qcloud-rev1 | Controller-manager probes kubelet port when kubelet update times out        |
