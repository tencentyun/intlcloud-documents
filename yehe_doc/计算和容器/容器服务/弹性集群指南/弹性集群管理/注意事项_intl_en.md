## Billing Mode
TKE Serverless cluster adopts the pay-as-you-go billing method. For more information about TKE Serverless cluster billing, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054), [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055), and [Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).

## Pod Specification Configuration
Container runtime resources and bills depend on the Pod specification configuration. Please note the Pod specification configuration and specific methods supported by TKE Serverless clusters. For more information, please see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057) and [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).


## Pod Temporary Storage
When created, each Pod is allocated less than 20 GiB of temporary image storage.

>!
>- Temporary image storage will be deleted when the Pod lifecycle ends. Therefore, please do not store important data in it.
>- Due to image storage, the actual available storage capacity is less than 20 GiB.
>- It is recommended to mount important data and large files to Volume for persistent storage.

## Kubernetes Version
Kubernetes v1.14 and earlier versions are not supported.

## Notes
TKE Serverless clusters do not have nodes. Therefore, some features, which depend on node components such as Kubelet and Kube-proxy, are not supported.
#### Node
- Currently, adding or managing a physical node is not supported.
- TKE Serverless clusters nodes will be replaced by "supernodes", and each supernode corresponds to a specified VPC subnet in the container network.
- The supernodes also support scheduling operations such as node affinity, taint, and cordoning.
- The number of Pods that can be scheduled on a supernode is only subject to the number of IPs in the corresponding VPC subnet.

#### Container network
- The container network of an TKE Serverless cluster is a VPC which is at the same level as Tencent Cloud services such as CVM and TencentDB. Each Pod in the cluster occupies a VPC subnet IP.
- Pods can directly communicate through the VPC with Pods or other Tencent Cloud services in the same VPC, without performance loss.

#### Pod isolation
Pods in the TKE Serverless cluster and the CVM have the same security isolation. Pods are scheduled and created on the underlying physical server of Tencent Cloud, and resource isolation between Pods is guaranteed by the virtualization technology during the creation.

#### Kernel
Only the kernel parameters starting with "net" can be defined.

#### Workload
You cannot deploy workloads of the DaemonSet type through TKE Serverless cluster.

#### Service
You cannot deploy services of the NodePort type through TKE Serverless cluster.

In addition, for the ordinary Kubernetes cluster, the Service of ClusterIP type relies on nodes to forward traffic. To make the TKE Serverless cluster compatible with the Service of ClusterIP type, you need to specify another VPC subnet as the cluster's Service CIDR block. Each ClusterIP Service will create a private network CLB in this subnet, which will occupy one IP in the subnet, to forward traffic. Please ensure that the subnet has sufficient available IPs.

#### Volume

TKE Serverless cluster supports the volume of the Hostpath type. For more information, see [Instructions for Other Storage Volumes](https://intl.cloud.tencent.com/document/product/457/30678).
TKE Serverless clusters may not necessarily meet your expectations because they don’t have nodes, although TKE Serverless cluster is still compatible with Host-related parameters (such as `Hostpath`, `Hostnetwork: true`, and `DnsPolicy: ClusterFirstWithHostNet`, etc.) in the Pod. For example, you want to use Hostpath to share data, but the two Pods scheduled to the same supernode may be the Hostpath of different hosts. Therefore, we recommend that the tasks you run on the TKE Serverless cluster do not strongly depend on Host-related parameters.

## Port Limits
Port 9100  are not available.
