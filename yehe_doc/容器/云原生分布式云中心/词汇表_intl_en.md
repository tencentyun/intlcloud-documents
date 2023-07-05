
### Security group

A security group is a virtual firewall that features stateful data packet filtering. It is used to configure the network access control of CVMs. You can add CVM instances with the same network security isolation requirements in the same region to the same security group to filter the inbound and outbound traffic of the CVM through the network policies of the security group.

### Edge cluster

It supports managing nodes located in multiple data centers in the same cluster, and delivering applications to all edge nodes with one click. Also, it has edge autonomy and distributed health check capabilities.

### Elastic cluster

You can deploy serverless Kubernetes clusters for workloads without the need to purchase any node. Same as TKE managed clusters, you will not be charged for management resources such as managed master components and etcd components.

### Self-deployed cluster

TKE provides an independent master node deployment mode, in which you have full control over your cluster. In this mode, the master nodes and etcd nodes of the Kubernetes cluster are deployed on the CVM you purchased, and you have all management and operation permissions for the Kubernetes cluster.

### Ingress

This is a collection of rules for routing external HTTP(S) traffic to a service.


### Node

<br/>In TKE, a node indicates a CVM that is registered in a cluster.
<br/>It indicates a blockchain component with specific features, and a unit that can operate independently. In blockchain TBaaS, it indicates a network node that maintains the ledger. In Fabric blockchain network, it indicates an endorser node by default.

### Node pool

A node pool provides features such as unified model, unified tag, Taint and dynamic scaling. You can quickly create, manage and terminate nodes as well as realize dynamic scaling of nodes with these features.

### Image

A pre-configured template for instances, containing a pre-configured environment (an operating system and other installed software programs) for the server.

### Image repository

An image repository is used to store Docker images. A single image repository corresponds to a single Docker application and hosts different versions of the application to deploy TKE.

### Cluster

In TKE, a cluster is a collection of cloud resources required for running a container. It includes several CVMs, CLBs and other resources. You can run your applications in your cluster.

### Namespace

<br/>In TSF, a namespace is an abstract collection of resources and objects. It isolates resources in the same cluster, so you can use the same account to create different environments.
A cluster can have multiple namespaces, but a resource in the cluster can belong to only one namespace. With namespaces, you can divide a cluster into the development environment, test environment, etc. If there are active network connections, services in the same namespace can discover and call each other.
<br/>In TCR, a namespace is a directory hierarchy in an instance like an organization in Docker Hub or a project in Harbor, which can be used to isolate image repositories of different projects, teams, or other organizations. A namespace falls between an instance and a repository, and its access level attribute directly determines the public or private attribute of image repositories in it. Image repositories and Helm chart repositories can share a namespace.
<br/>In TDMQ, a namespace manages associated topics as a group. It is the basic unit of topic management. Each tenant can have multiple namespaces which correspond to different Tencent Cloud environments.

### ConfigMap

A ConfigMap is a collection of multiple configurations that help you manage different environments and applications.

### Managed cluster

TKE provides Kubernetes cluster management service where all master components and etcd components are hosted. In this mode, the master components and etcd components of a Kubernetes cluster are managed and maintained by Tencent Cloud technical team. You only need to purchase worker nodes required by cluster running, without the need to take care of cluster management.