## Object Management Instructions

You can manipulate native Kubernetes objects directly in the console, such as Deployment, DaemonSet, and more.
A Kubernetes object is a persistent entity in a cluster that is used to carry the business running in the cluster. Different Kubernetes objects can express different meanings:
- Running applications
- Resources available to applications
- Application-associated policies

You can use Kubernetes objects directly in the TKE console or through the Kubernetes APIs such as kubectl.

## Types of Objects

Common Kubernetes objects are mainly divided into the following types:
- Workloads
    + Deployment: Used to manage a Pod for which a scheduling rule has been specified.
    + StatefulSet: Used to manage the workload API objects of a stateful application.
    + DaemonSet: Used to ensure that Pods are running on all or some of the nodes, such as log collection.
    + Job: A Job creates one or more Pods until the end of run.
    + CronJob: A Job that runs as scheduled.
- Services
    + Service: A Kubernetes object that provides Pod access. Different types can be defined based on business needs.
    + Ingress: A Kubernetes object that manages external access to Services in a cluster.
- Configuration
    + ConfigMap: Used to store configuration information.
    + Secret: Used to store sensitive information such as passwords and tokens.
- Storage
    + Volume: Used to store container access-related data.
    + PersistentVolume (PV): A piece of storage configured in a Kubernetes cluster.
    + PersistentVolumesClaim (PVC): Claim for a storage request. If a PV is seen as a Pod, then a PVC is equivalent to a workload.
    + StorageClass: Used to describe the type of storage. When a PVC is created, the storage of the specified type (i.e. stored template) is created through the StorageClass.

There are dozens of other Kubernetes objects such as Namespace, HPA, and ResourceQuota. You can use different objects based on your business needs. The objects available vary by Kubernetes version. For more information, visit [Kubernetes' official website](https://kubernetes.io/docs/concepts/).

## Object Management Operations

- Workloads
    + [Deployment Management](https://cloud.tencent.com/document/product/457/31705)
    + [StatefulSet Management](https://cloud.tencent.com/document/product/457/31707)
    + [DaemonSet Management](https://cloud.tencent.com/document/product/457/31706)
    + [Job Management](https://cloud.tencent.com/document/product/457/31708)
    + [CronJob Management](https://cloud.tencent.com/document/product/457/31709)
- Services
    + [Service Management](https://cloud.tencent.com/document/product/457/31710)
    + [Ingress Management](https://cloud.tencent.com/document/product/457/31711)
- Configuration
    + [ConfigMap Management](https://cloud.tencent.com/document/product/457/31717)
    + [Secret Management](https://cloud.tencent.com/document/product/457/31718)
- Storage
    + [Volume Management](https://cloud.tencent.com/document/product/457/31713)
    + [PersistentVolume Management](https://cloud.tencent.com/document/product/457/31712)
    + [PersistentVolumesClaim Management](https://cloud.tencent.com/document/product/457/31712)
    + [StorageClass Management](https://cloud.tencent.com/document/product/457/31714)
