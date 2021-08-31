## Basic Concepts 

#### Cluster
A cluster is a collection of cloud resources required to run a container, including several CVMs and CLBs. You can run your applications in a cluster.

#### Managed cluster
TKE provides the Kubernetes cluster management service for managing Master and Etcd nodes. In this mode, the Tencent Cloud technical team centrally manages and maintains the Master and Etcd nodes of a Kubernetes cluster. You only need to purchase worker nodes for the cluster in order to run workloads and do not need to care about cluster management.

#### Independently deployed cluster

TKE provides an independent Master deployment mode in which you have full control over your cluster. In this mode, the Master and Etcd nodes of the Kubernetes cluster are deployed in your CVM instances, and you have full management and operation permissions for the Kubernetes cluster.

#### Elastic cluster
An elastic cluster is a serverless Kubernetes cluster that allows you to deploy workloads without purchasing nodes. Managed control-plane resources, such as the Master and Etcd nodes, are not billed in an elastic cluster, just as in a TKE managed cluster.

#### Edge cluster
In an edge cluster, you can manage nodes deployed in multiple data centers (DCs), deliver an application to all edge nodes with one-click, and enjoy edge autonomy and distributed health check capabilities.

#### Node
A node is a basic element of a container cluster. It can be either a virtual machine or a physical machine, depending on the service. Each node contains the basic components required to run a pod, including Kubelet and Kube-proxy.

#### Container
Docker containers allow you to run applications independently in an independent environment. Multiple containers can run in a node.

#### Image
Docker images are used to deploy TKE. Each image has a unique ID (image repository address + image name + image tag). Currently, Docker Hub official images and users' private images are supported.


## Advanced Concepts

#### Node pool
Nodes in a node pool have the same model, label, and taint attributes and can be dynamically scaled in or out. With these features, you can conveniently and quickly create, manage, and terminate nodes and dynamically scale nodes in and out.

#### Application
Kubernetes applications can run in a cluster. TKE allows you to create applications from the application market, third-party applications, and private applications.


#### Image repository
An image repository is used to store Docker images, which are used to deploy TKE.


#### Application market
The TKE application market provides Kubernetes community applications suitable for various scenarios. You can use application packages from the application market to create and run applications in clusters.

#### Security group
A security group is a virtual firewall that can filter stateful data packets. It is used to configure network access control for one or more CVMs. It is an important network security isolation method provided by Tencent Cloud. For more information, see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).

#### Add-on
Add-ons include event persistence components, log collection components, GPU management components, and COS and file storage components. You can install these components to extend related features for clusters.

#### Namespace

You can set multiple namespaces in a Kubernetes cluster. Each namespace is an independent virtual space. Resources in different namespaces are isolated. A cluster can use namespaces to manage resources by partition.

#### Workloads

<table>
<tr>
<th>Type</th> <th>Description</th>
</tr>
<tr>
<td>Deployment</td>
<td>A Deployment workload declares a pod template and a policy for controlling how the pod runs. It is used to deploy stateless applications. You can declare the number of replicas, scheduling policy, and update policy for a pod that runs in the Deployment workload as required.</td>
</tr>
<tr>
<td>StatefulSet</td>
<td>A StatefulSet workload is used to manage stateful applications. It creates a persistent identifier for each pod based on the specifications. The identifier will be retained after the pod is migrated, terminated, or restarted. When using persistent storage, you can map storage volumes to identifiers. If your application does not require a persistent identifier, we recommend that you use a Deployment workload to deploy the application.</td>
</tr>
<tr>
<td>StatefulSet with fixed pod IP addresses</td>
<td>TKE provides StatefulSet workloads with fixed pod IP addresses. Pods created by StatefulSet workloads of this type will be assigned private network IP addresses through the ENI. The TKE VPC-CNI plugin is responsible for IP address assignment. When a pod is restarted or migrated, its IP address can remain unchanged.</td>
</tr>
<tr>
<td>DaemonSet</td>
<td>A DaemonSet workload is used to deploy resident backend programs in a cluster., such as node log collection. DaemonSet ensures that specified pods are running on all or certain nodes. When you add new nodes to a cluster, pods are deployed automatically. When nodes are removed from the cluster, pods are retrieved automatically.</td>
</tr>
<tr>
<td>Job</td>
<td>A Job creates one or multiple pods and ensure that these pods run according to the rules until they are terminated.</td>
</tr>
<tr>
<td>CronJob</td>
<td>A CronJob workload periodically runs a Job workload based on a preset plan.</td>
</tr>
</table>

#### Service

You can deploy various containers in a Kubernetes cluster. Some containers use HTTP or HTTPS to provide external Layer-7 network services, and the others use TCP or UDP to provide Layer-4 network services. Service resources defined by Kubernetes are used to manage Layer-4 network service access in a cluster. Based on the Layer-4 network, a service exposes TKE in a cluster.

#### Ingress

An ingress exposes HTTP and HTTPS services in a Layer-7 network and provides common Layer-7 network capabilities. An ingress is a collection of rules that allow access to services of a cluster. You can configure different forwarding rules to allow different URLs to access different services.

#### ConfigMap
- **ConfigMap**: a key-value pair. ConfigMap allows you to decouple the configuration from the runtime image to make the application more portable.
- **Secret**: a key-value pair. A secret stores sensitive information, such as passwords, tokens, and keys to reduce the risk of information leakage.


#### Volume

A volume is a directory that may contain some data. Containers in a pod can access the directory. The volume lifecycle is the same as that of a pod and longer than that of containers running in the pod. Typically, it saves data when a container is restarted.

#### PersistentVolume (PV)
PVs are used to store resources in a cluster, such as nodes. A PV is independent of the lifecycle of the pod, and different types of PVs can be created based on different StorageClass types.

#### PersistentVolumeClaim (PVC)

PersistentVolumeClaim (PVC) is a storage request in a cluster. Pods consume node resources, and the PVC consumes PV resources. If PV resources are insufficient, the PVC can dynamically create PVs.

#### StorageClass
StorageClass describes the storage type. A cluster admin can define different storage types for a cluster.

## References

- [Official Docker documentation](https://docs.docker.com/glossary/)
- [Official Kubernetes documentation](https://kubernetes.io/docs/concepts/)
