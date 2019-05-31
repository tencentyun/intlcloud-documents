## TKE Release Notes
|Date| Updates  |
| ------| ------- |
| 2019.05.20 | Fixes the fault tolerance issue when drain fails during autoscaling |
| 2019.05.17 | <ul><li>Supports registering TKE network to CCN</li><li> Supports GPU virtualization</li></ul> |
| 2019.04.24 | <ul><li>Kubelet applies CNI mode by default</li></ul>|
| 2019.04.22 | <ul><li>Beta release of Docker 18.06</li><li>Releases new alarming system in all regions</li></ul> |
| 2019.03.28 | <ul><li>Supports BM 2.0 nodes</li><li>Supports using purchased CVMs to create clusters</li></ul>|
| 2019.03.16 | Supports setting a scaling-in threshold for cluster scaling  |
| 2019.03.12 | Cluster AS group supports scaling out using GPU instances    |
| 2019.02.18 | Releases new monitoring system  |
| 2019.02.15 | Standalone cluster supports Kubernetes version 1.12  |
| 2019.02.13 | Fixes runc vulnerability CVE-2019-5736   |
| 2019.01.24 | <ul><li>Supports using existing LB to create services</li><li>[Supports using custom images to create clusters (please submit a ticket to do so)](https://console.qcloud.com/workorder)</li><li>Supports setting affinity scheduling while creating workload</li></ul>|
| 2019.01.10 | Supports multiple services using the same existing LB |

|Date|Updates|
|:--|:---|
|2018.12.04|<ul><li>Fixes Privilege Escalation Vulnerability in Kubernetes</li><li>[Disables creation of Kubenretes1.7.8 containers (please submit a ticket if this is still needed)](https://console.qcloud.com/workorder)</li></ul>|
|2018.10.31|<ul><li>Starts internal trials of TKE new console</li><li>Supports the binding of specified partial nodes to the LB of the service</li></ul>|
|2018.09.10|<ul><li>Upgrades default kubernretes version to 1.10</li><li>BM clusters support Kubernetes1.10</li><li>BM clusters support Ubuntu16.04|
|2018.07.30|<ul><li>TKE launches in Russia</li><li>TKE launches in India</li><li>Supports visiting Master from private network</li><li>Releases the open source component tencentcloud-cloud-controller-manager<br></li><li>Releases the open source component  kubernetes-csi-tencentcloud</li><li>Releases the BM cluster ingress plug-in</li></ul>|
|2018.06.22|<ul><li>CCS is renamed to TKE</li><li>Supports custom configuration of cluster auto scaling</li><li>Supports importing scripts for node initialization|
|2018.05.01|<ul><li>Supports BM clusters</li><li>Supports GPU clusters</li></ul>|
|2018.04.01|<ul><li>Console UI update</li><li>Supports all CVM types</li></ul>|
|2018.03.01|<ul><li>Supports auto scaling of service</li><li>Supports purchasing all CVM models</li><li>Releases new version of console</li></ul>|
|2018.02.08|Supports auto scaling of clusters|
|2018.02.06|<ul><li>Introduces log collection feature</li><li>Introduces application management feature</li><li>[Introduces FREE lab features](https://console.cloud.tencent.com/ccs/lab)</li></ul>|
|2017.12.20|<ul><li>Supports purchasing cluster nodes with vouchers</li><li>Supports creating empty clusters</li><li>Supports setting container directory and project of existing nodes</li></ul>|
|2017.11.30|<ul><li>Cluster retaining policy - preserves system processes like dockerd, kubelet</li><li>Cluster draining policy - ensures the system processes have sufficient sources and drain the pods</li><li>dockerd  log rollback - remove logs automatically to ensure the disk has enough space</li><li>[Supports wildcards in ingress forwarding rules](https://cloud.tencent.com/document/product/457/9111#.E5.9F.9F.E5.90.8D.E9.80.9A.E9.85.8D.E7.AC.A6.E8.AF.B4.E6.98.8E)</li></ul>|
|2017.10.31|<ul><li>[Starts internal trial of application management](https://cloud.tencent.com/act/apply/ccs_application)</li><li>Supports multi-regional deployment of image repositories; launches in Hong Kong<br></li><li>Launches in Tencent Cloud International</li></ul>|
|2017-09-26|<ul><li>Introduces CAM access management for image repositories<br></li><li>Supports setting labels for services<br></li><li>Supports importing environment variables in configurations<br></li><li>Supports setting resource project for clusters<br></li><li>Launches in Singapore</li></ul>|
|2017-08-23|<ul><li>Supports alarming</li><li>Supports  Kubernetes1.7</li><li>Supports continuous integration and deployment based on TencentHub</li><li>Introduces triggers for image repositories</li><li>Supports operation logs of image repositories</li></ul>|
|2017-08-04|<ul><li>Supports operating clusters on Kubectl via internet</li><li>Supports CAM access management for clusters</li></ul>|
|2017-07-19|Supports config file management|
|2017-07-18|<ul><li>Supports CI source code building</li><li>Introduces TencentHub images in Image Registry</li><li>Introduces "My Favorites” in Image Registry</li><li>Allows an image repository to have multiple namespaces</li></ul>|
|2017-06-24|<ul><li>Supports NFS data volume</li><li>Introduces privileged containers and working directory configuration</li></ul>|
|2017-06-07|<ul><li>Supports cluster spaces<br></li><li>Supports auto-formatting data disks and specifying container directory while creating/adding CVMs in container clusters<br></li><li>Supports re-deployment of services</li></ul>|
|2017-04-27|**CCS opens to the public**<ul><li>Supports adding existing CVMs to container clusters</li><li>Supports more monitoring metrics for instances, services and clusters</li><li>Supports checking of container logs</li></ul>|
|2017-04-19|<ul><li>Supports uploading/downloading files on web remote client</li><li>Supports creating monthly-subscribed CVMs in clusters</li><li>Supports configuring custom security groups while creating clusters</li></ul>|
|2017-03-15|<ul><li>[Supports logging into containers from web remote client</li><li>Supports creating services using non-Tencent Cloud images</li></ul>|
|2017-03-06|<ul><li>Supports layer-7 load balancers<br></li><li>Supports monitoring of clusters, services and pods<br></li><li>Supports native K8SAPI; supports requiring k8s certificates via Tencent Cloud APIs; supports all features of k8s</li></ul>|
|2016-12-26|**CCS internal trial starts**<br><ul><li>Clusters: adding/deleting/modifying/checking clusters; VPC-based container clusters; cross-AZ clusters; supporting native kubernetes APIs</li><li>Services: adding/deleting/modifying/checking services; creating services using private/Docker official images; cross-AZ scheduling of services</li><li>Images: Docker images; custom images; upload/download private images; acceleration of Docker official images</li><li>Monitoring: cluster and container monitoring</li><li>Supports checking creation and update time of service; supports rolling update of services</li></ul>|


## TKE kubernetes revisions
### TKE kubernetes 1.10.5 revisions
|Date|Revisions|Updates|
|:--|:---|:--|
|2018.09.28|v1.10.5-tke.2|Removes the logic of creating CLB from controller-manager (implements it by standalone service controller)|
|2018.09.27|v1.10.5-tke.1|backport [pr63321](https://github.com/kubernetes/kubernetes/pull/63321). Fixes the issue that it takes too long to terminate while there’re multiple containers in a pod|
|2018.09.21|v1.10.5-qcloud-rev1|Controller-manager probes kubelet port when kubelet update times out|


### TKE kubernetes 1.8.13 revisions
|Date|Revisions|Updates|
|:--|:---|:--|
|2018.09.28|v1.8.13-tke.2|Removes the logic of creating CLB from controller-manager (implements it by standalone service controller)|
|2018.09.27|v1.8.13-tke.1|<ul><li>Closes kmem statistics to avoid leakage of cgroup number</li><li>Reduces resourcequota conflicts while creating pods</li></ul>|
|2018.09.21|v1.8.13-qcloud-rev1|Controller-manager probes kubelet port when kubelet update times out|

### TKE kubernetes 1.7.8 revisions
|Date|Revisions|Updates|
|:--|:---|:--|
|2018.09.28|v1.7.8-tke.2|Fixes the conflicts between Tencent Cloud controller-manager and third-party service controller|
|2018.09.27|v1.7.8-tke.1|Removes the logic of creating CLB from controller-manager (implements it by standalone service controller)|
|2018.09.21|v1.7.8-qcloud-rev1|Controller-manager probes kubelet port when kubelet update times out |
