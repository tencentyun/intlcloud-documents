When you create a Kubernetes cluster by using TKE, you must select models from various configuration options. This document describes and compares available feature models and gives suggestions to help you select models that are most applicable to your services.
- [Kubernetes Versions](#Kubernetes)
- [Container Network Plugins: GlobalRouter and VPC-CNI](#network)
- [Runtime Components: Docker and Containerd (Under Beta Testing)](#runtime)
- [Service Forwarding Modes: iptables and IPVS](#service)
- [Cluster Types: Managed Cluster and Self-Deployed Cluster](#cluster)
- [Node Operating Systems](#os)
- [Node Pool](#nodepool)
- [Launch Script](#shell)

<span id ="Kubernetes"></span>
## Kubernetes Versions
Kubernetes versions are iterated quickly. New versions usually include many bug fixes and new features. Meanwhile, earlier versions will be phased out. We recommend that you select the latest version that is supported by the current TKE when creating a cluster. Subsequently, you can upgrade existing master components and nodes to the latest versions generated during iteration.

<span id ="network"></span>

## Container Network Plugins: GlobalRouter and VPC-CNI

### Network modes
TKE supports the following two network modes. For more information, see [How to Choose TKE Network Mode](https://intl.cloud.tencent.com/document/product/457/38966).
- **GlobalRouter mode**:
	- In this mode, container network capabilities are implemented based on container networking interfaces (CNIs) and network bridges, whereas container routing is implemented based on the underlying VPC layer.
	- Containers are located on the same network plane as nodes. IP ranges of containers cover abundant IP addresses and do not overlap those of VPC instances.

- **VPC-CNI mode**:
	- In this mode, container network capabilities are implemented based on CNIs and VPC ENIs, whereas container routing is implemented based on ENIs. The performance of this mode is approximately 10% higher than that of the GlobalRouter mode.
	- Containers are located on the same network plane as nodes. The IP ranges of containers fall within those of VPC instances.
	- Pods can use static IP addresses.


### How to use
TKE allows you to specify network modes in the following ways:
 - Specify the GlobalRouter mode when creating a cluster.
 - Specify the VPC-CNI mode when creating a cluster. Subsequently, all pods must be created in VPC-CNI mode.
 - Specify the GlobalRouter mode when creating a cluster. You can enable the VPC-CNI mode for the cluster when needed. In this case, the two modes are mixed.


### Recommendations
- In general cases, we recommend that you select the GlobalRouter mode, because IP ranges of containers cover abundant IP addresses, allow high scalability, and support large-scale services.
- If a subsequent service needs to run in VPC-CNI mode, you can enable the VPC-CNI mode for the GlobalRouter cluster. In this case, the GlobalRouter mode is mixed with the VPC-CNI mode, but only some services run in VPC-CNI mode.
- If you fully understand and accept the use limits of the VPC-CNI mode and all pods in the cluster need to run in VPC-CNI mode, we recommend that you select the VPC-CNI mode when creating the cluster.

<span id="runtime"></span>


## Runtime Components: Docker and Containerd (Under Beta Testing)

### Runtime components
TKE supports two types of runtime components: Docker and containerd. For more information, see [How to Choose Between containerd and Docker](https://intl.cloud.tencent.com/document/product/457/31088).
- **Using Docker as a container runtime**:
  ![](https://main.qcloudimg.com/raw/3bfe6956a3c4c1f28db41cf4cb14b3ec.png)

  - The call chain is as follows:
   1. The dockershim module in kubelet adapts the container runtime interface (CRI) for the Docker runtime.
   2. The kubelet component calls dockershim by using a socket file.
   3. The dockershim module calls the API of the dockerd component, that is, the Docker HTTP API.
   4. The dockerd component calls the docker-containerd gRPC API to create or terminate the container.
  - Reasons for a long call chain:
  Kubernetes initially supported Docker only. Later, the CRI was introduced and runtime was abstracted so that multiple types of runtimes were supported. Docker and Kubernetes are competitors, and therefore Docker did not implement the CRI in dockerd, and Kubernetes had to implement the CRI in dockerd itself. Internal components of Docker were modularized to adapt to the CRI.

- **Using containerd (under beta testing) as a container runtime**:
![](https://main.qcloudimg.com/raw/3b868d11263d6120512bec5b1cc52a20.png)
	
	- Containerd has supported the CRI plugin since containerd 1.1. That is, containerd can adapt to the CRI.
	- The call chain of the containerd runtime does not include dockershim and dockerd, which exist in the call chain of the Docker runtime.

### Comparison between the two runtimes
- The call chain of the containerd runtime bypasses dockerd and therefore is shorter. Accordingly, the containerd solution requires fewer components, occupies fewer node resources, and bypasses dockerd bugs. However, containerd has some bugs that need to be fixed. Currently, containerd is under beta testing and has fixed some bugs.
- Having been used for a long time, the Docker solution is more mature, supports the Docker API, and provides abundant features. This solution is friendly to most users.

### Recommendations
- The Docker solution is more mature than the containerd solution. If you require high stability, we recommend that you select the Docker solution.
- In the following scenarios, you can select the Docker solution only:
 - You need to run a Docker host inside of another Docker host (Docker-in-Docker). This requirement usually occurs during continuous integration (CI).
 - You need to use Docker commands on a node.
 - You need to call the Docker API.

In other scenarios, we recommend that you select the containerd solution.

<span id="service)"></span>


## Service Forwarding Modes: iptables and IPVS
The following figure shows how a Service is forwarded.
![](https://main.qcloudimg.com/raw/c05b7266ff029047e11e23d1cf14504e.png)
1. The kube-proxy component on the node watches API Server to obtain the Service and the Endpoint. Then, the kube-proxy component converts the Service to an iptables or IPVS rule based on the forwarding mode and writes the rule to the node.
2. The client in the cluster gains access to the Service through the cluster IP address. Then, according to the iptable or IPVS rule, the client is load-balanced to the backend pod corresponding to the Service.

### Comparison between the two forwarding modes
- The IPVS mode provides higher performance but has some outstanding bugs.
- The iptables mode is more mature and stable.

### Recommendations
If you require extremely high stability with less than 2,000 Services running in the cluster, we recommend that you select iptables. In other scenarios, we recommend that you preferably select IPVS.

<span id ="cluster"></span>

## Cluster Types: Managed Cluster and Self-Deployed Cluster
TKE supports the following types of clusters:
- **Managed clusters**:
 - Master components are invisible to you but are managed by Tencent Cloud.
 - Clusters with most new features are preferably managed.
 - Computing resources of master components are automatically scaled up based on the cluster scale.
 - You do not need to pay for master components.

- **Self-deployed clusters**:
	- Master components are fully under your control.
	- You need to purchase master components.
	
### Recommendations
In regular cases, we recommend that you select managed clusters. If you need to fully control master components, such as specifying custom features to implement advanced features, you can select self-deployed clusters.

<span id="os"></span>


## Node Operating System

TKE supports three distributions of operating systems, Tencent Linux, Ubuntu and CentOS. The Tencent Linux operating system uses [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel) that is a customized kernel maintained by Tencent Cloud team. Other operating systems use the open-source kernel provided by the official Linux community. The following shows the supported operating systems. 
![](https://main.qcloudimg.com/raw/732966719f531c12d517366c2eed7071.png)



>? TKE-Optimized series images is once used for improving the stability of the image and providing more features, but it is not available for the clusters in TKE console after the Tencent Linux public image is launched. For more information, see [TKE-Optimized Series Images](https://intl.cloud.tencent.com/document/product/457/34715).




### Recommendations

We recommend that you use the Tencent Linux operating system. It is a public image of Tencent Cloud that contains the [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel). TKE now supports this image and uses it as the default image.

<span id="nodepool)"></span>

## Node Pool
The node pool is mainly used to batch manage nodes with the following items:
- Label and Taint properties of nodes
- Startup parameters of node components
- Custom launch script for nodes
For more information, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).

### Application scenarios
- Manage heterogeneous nodes by group to reduce management costs.
- Use the Label and Taint properties to enable a cluster to support complex scheduling rules.
- Frequently scale out and in nodes to reduce operation costs.
- Routinely maintain nodes, such as upgrade node versions.

### Examples
Some I/O-intensive services require models with high I/O throughput. You can create a node pool for a service of these kinds, configure a model, centrally specify Label and Taint properties for the nodes, and configure affinity with I/O-intensive services. You can select Labels to schedule the service to a node with a high I/O model. To avoid other service pods from being scheduled to the node, you can select specific Taints.

When the service traffic increases, the I/O-intensive service needs more computing resources. During peak hours, the HPA feature automatically scales out pods for the service, and the computing resources of the node become insufficient. In this case, the auto scaling feature of the node pool automatically scales out nodes to withstand the traffic spike.

<span id="shell"></span>


## Launch Script
### Custom parameters for components
>?To use this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.
>
- When creating a cluster, you can customize some startup parameters of master components in **Advanced Settings** under **Cluster Information**.
![](https://main.qcloudimg.com/raw/2470700f16e0c274828d775c57884b24.png)
- In **Select Model** step, you can customize some startup parameters of kubelet in **Advanced Settings** under **Worker Configurations**.
![](https://main.qcloudimg.com/raw/caf2c8185044be4648cfe26d2ac9e362.png)


### Node launch configuration
- When creating a cluster, in **Advanced Settings** under **CVM Configuration**, you can specify custom data to configure the node launch script. In the script, you can modify component startup parameters and kernel parameters, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a8a02291383025e3ec5ad54a6ddf69db.png)
- When adding a node, in **Advanced Settings** under **CVM Configuration**, you can specify custom data to configure the node launch script. In the script, you can modify component startup parameters and kernel parameters, as shown in the following figure:
![](https://main.qcloudimg.com/raw/18f8150375278f5ab5400330236be470.png)


