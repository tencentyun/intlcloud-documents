Elastic cluster is a service of Elastic Kubernetes Service (EKS). Before you use this service, please read the following information.

## Billing Method
EKS adopts the pay-as-you-go billing method. For more information about the bills, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054), [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055), and [Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).

## Pod Specification Configuration
Container runtime resources and bills depend on the pod specification configuration. Please note the pod specification configuration and specific methods supported by elastic clusters. For more information, please see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057) and [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).

## Pod Temporary Storage
Upon the creation of each pod, temporary image storage less than 20 GiB is allocated.

>!
>- Temporary image storage will be deleted when the pod lifecycle ends. Therefore, ensure that important data is not stored in it.
>- Due to image storage, the actual available storage is less than 20 GiB.
>- You are recommended to mount important data and large files to Volume for persistent storage.

## Kubernetes Version
Kubernetes versions earlier than 1.12 are not supported.

## Unsupported Features
Elastic clusters do not have nodes. Therefore, some dependent node components, such as Kubelet and Kube-proxy, are not supported.
### Node
Currently, adding or managing a physical node is not supported.

### Kernel
Only kernel parameters started with "net" can be defined.

### Workloads
You cannot deploy workloads of the DaemonSet type through EKS.

### Services
You cannot deploy services of the NodePort type through EKS.

### Volumes
You cannot use Linux filesystem events with inotify, which is a feature of emptyDir volumes.
