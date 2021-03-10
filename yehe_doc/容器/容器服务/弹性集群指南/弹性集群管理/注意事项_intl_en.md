>! Elastic cluster is a service of Elastic Kubernetes Service (EKS). Before you use this service, please read the following information.

## Billing Mode
EKS adopts the pay-as-you-go billing method. For more information about EKS billing, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054), [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055), and Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).

## Pod Specification Configuration
Container runtime resources and bills depend on the pod specification configuration. Please note the pod specification configuration and specific methods supported by elastic clusters. For more information, please see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057) and [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).


## Pod Temporary Storage
Each pod will be allocate less than 20 GiB temporary image storage when it be created.

>!
>- Temporary image storage will be deleted when the pod lifecycle ends. Therefore, ensure that important data is not stored in it.
>- Due to image storage, the actual available storage is less than 20 GiB.
>- You are recommended to mount important data and large files to Volume for persistent storage.

## Kubernetes Version
Kubernetes v1.12 and lower versions are not supported.

## Unsupported Features
Elastic clusters do not have nodes. Therefore, some dependent node components, such as Kubelet and Kube-proxy, are not supported.
#### Node
- Currently, adding or managing a physical node is not supported.
- EKS nodes will be replaced by "virtual nodes", and each virtual node corresponds to a specified VPC subnet in the container network.
- The virtual nodes also support the scheduling operations such as node affinity, taint, and cordoning.
- The number of Pods that can be scheduled on a virtual node is only limited by the number of IPs in the corresponding VPC subnet.

#### Container network
- The container network of an elastic cluster uses a VPC which is at the same level as the Tencent Cloud services such as CVM and TencentDB. Each Pod in the cluster will occupy a VPC subnet IP.
- Pod and Pod, Pod and other Tencent Cloud services in the same VPC can communicate directly through the VPC, without performance loss.

#### Pod isolation
The Pod in the elastic cluster has the same security isolation as the CVM. Pods are scheduled and created on the underlying physical server of Tencent Cloud, and the resource isolation between Pods is guaranteed by virtualization technology during the creation.

#### Kernel
Only kernel parameters started with "net" can be defined.

### Workloads
You cannot deploy workloads of the DaemonSet type through EKS.

#### Services
You cannot deploy services of the NodePort type through EKS.

In addition, for the ordinary Kubernetes cluster, the Service of ClusterIP type relies on nodes to forward traffic. For the elastic cluster, in order to be compatible with the Service of ClusterIP type, the user needs to specify a separate VPC subnet as the cluster's Service CIDR. Each ClusterIP Service will create a private network CLB (for free) in this subnet, which will occupy one IP in the subnet, to forward traffic. Please ensure that the subnet has sufficient available IPs.

#### Volumes
Volumes of hostpath type are not supported.
