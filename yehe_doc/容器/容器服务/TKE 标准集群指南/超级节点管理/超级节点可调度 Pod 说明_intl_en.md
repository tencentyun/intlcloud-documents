

## Billing Mode

Pods scheduled to super nodes are billed on a pay-as-you-go or spot basis.

## Kubernetes Versions

- Pay-as-you-go super nodes are supported by clusters on v1.16 or later.

## Specifications of Pods Schedulable to Super Nodes

Make sure that you understand the specifications and configurations of Pods supported by super nodes, as they are the basis for billing available resources and services during container running.

### Pay-as-you-go mode

- 0.25C–16C Pods are supported (for nonstandard Pods, their specifications are automatically upgraded).
- Pods with a CPU to memory ratio of more than 1:8 are supported.

List of specifications supported by nodes:
>! For nonstandard Pods, their specifications are automatically upgraded.
>

| CPU (Cores) | Memory Range (GiB) | Granularity of Memory Range (GiB) |
| :----- | :----------- | :--------------- |
| 0.25   | 0.5, 1, 2    | -                |
| 0.5    | 1, 2, 3, 4   | -                |
| 1      | 1 - 8        | 1                |
| 2      | 4 - 16       | 1                |
| 4      | 8 - 32       | 1                |
| 8      | 16 - 32      | 1                |
| 12     | 24 - 48      | 1                |
| 16     | 32 - 64      | 1                |

 

## Super Node Configuration

### Pod temporary storage

When each Pod scheduled to a super node is created, a temporary image storage of 20 GiB will be allocated.

>!
>- Temporary image storage will be deleted when the Pod lifecycle ends. Therefore, do not store important data in it.
>- The actual available storage will be less than 20 GiB due to the stored images.
>- Annotations can be used to scale out system disk resources.
>- We recommend you mount important data and large files to Volume for persistent storage.

### Pod network

Pods scheduled to super nodes are in the same VPC as Tencent Cloud services such as CVM and TencentDB. Each Pod occupies a VPC subnet IP.
A Pod can connect to other Pods or Tencent Cloud services in the same VPC without any performance losses.

### Pod isolation

Pods scheduled to super nodes have the same security isolation as CVM instances. Pods are scheduled and created on the underlying physical server of Tencent Cloud, and the resource isolation between Pods is guaranteed by virtualization technology during the creation.

### Other special Pod configurations

You can define `template annotation` in a YAML file to implement capabilities such as binding security groups, allocating resources, and allocating EIPs for Pods scheduled to super nodes. For configuration details, see the following table:

>!
>- If no security group is specified, a Pod will be bound to the specified security group of the node pool by default. Make sure that the network policy of the security group doesn't affect the normal operation of the Pod. For example, you need to open port 80 if the Pod provides services via port 80.
>- To allocate CPU resources, you must specify the `cpu` and `mem` annotations in line with the CPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057).
>- To allocate GPU resources through the method specified in the annotation, you must specify the `gpu-type` and `gpu-count` annotations and ensure that their values meet the GPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057).

| Annotation Key                                      | Annotation Value and Description                                      | Required                      |
| :------------------------------------------------ | :----------------------------------------------------------- | :----------------------------------------------------------- |
| eks.tke.cloud.tencent.com/security-group-id       | Default security group bound to a workload. [Security group ID](https://console.cloud.tencent.com/cvm/securitygroup): You can enter multiple IDs and separate them by comma, for example, `sg-id1,sg-id2`. Network policies take effect based on the sequence of security groups. | No. If you don't specify it, the security group specified by the node pool is bound by default. If you specify it, make sure that the security group ID already exists in the same region. |
| eks.tke.cloud.tencent.com/cpu                     | Number of CPU cores required by a Pod. For more information, see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). The unit is cores by default and doesn't need to be specified. | No. If you specify it, make sure that the specification is supported, and you need to enter the `cpu` and `mem` parameters. |
| eks.tke.cloud.tencent.com/mem                     | Amount of memory required by a Pod. For more information, see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). You need to specify the unit, for example, 512 MiB, 0.5 GiB, or 1 GiB. | No. If you specify it, make sure that the specification is supported, and you need to enter the `cpu` and `mem` parameters. |
| eks.tke.cloud.tencent.com/cpu-type                | CPU model required by a Pod. Currently, Intel and AMD are supported. For more information on configurations supported by S4, S3, and other models, see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). | No. If you don't specify it, the system will match the most suitable specification according to [Specifying resource specifications](https://intl.cloud.tencent.com/document/product/457/36161). If the matched specification is supported by both Intel and AMD, the Intel specification is preferred. |
| eks.tke.cloud.tencent.com/gpu-type                | GPU model required by a Pod. Currently, V1001/4*T41/2*T4T4 are supported. You can specify the model by priority, for example, "T4,V100" indicates T4 Pods will be created first. If the T4 resources in the selected region are insufficient, V100 Pods will be created. For more information on configurations, see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). | It is required if you need a GPU. When specifying it, make sure that the GPU model is supported; otherwise, an error will be reported. |
| eks.tke.cloud.tencent.com/gpu-count               | Number of GPUs required by a Pod. For more information, see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). The unit is cards by default and doesn't need to be specified. | No. If you specify it, make sure that the specification is supported.                             |
| eks.tke.cloud.tencent.com/retain-ip               | Static IP of a Pod. Enter the value of `"true"` to enable this feature. If a Pod with the static IP enabled is terminated, its IP will be retained for 24 hours by default. If the Pod is rebuilt within 24 hours, its IP can still be used; otherwise, its IP may be occupied by other Pods. **It is valid only for StatefulSet and raw Pods.** | No                                                           |
| eks.tke.cloud.tencent.com/retain-ip-hours         | Modifies the default retention period of a Pod's static IP. Enter a number. The unit is hours, and the default value is 24 hours. An IP can be retained for up to one year. **It is valid only for StatefulSet and raw Pods.** | No                                                           |
| eks.tke.cloud.tencent.com/eip-attributes          | Indicates that the Pod of the workload needs to be associated with an EIP. When the value is "", the default EIP configuration is used. You can enter the cloud API parameter `json` of the EIP in "" to customize the configuration. For example, if the value of `annotation` is '{"InternetMaxBandwidthOut":2}', the bandwidth is 2 Mbps. Note that this cannot be used for non-bill-by-IP accounts. | No                                                           |
| eks.tke.cloud.tencent.com/eip-claim-delete-policy | Indicates whether to repossess the EIP after the Pod is deleted. `Never` indicates not to repossess. The default value is to repossess. This parameter takes effect only when `eks.tke.cloud.tencent.com/eip-attributes` is specified. Note that this cannot be used for non-bill-by-IP accounts. | No                                                           |
| eks.tke.cloud.tencent.com/eip-id-list             | If the workload is a StatefulSet, you can also specify one or multiple existing EIPs, such as "eip-xx1,eip-xx2". Note that the number of StatefulSet Pods must be less than or equal to the number of EIP IDs specified in this annotation; otherwise, Pods that cannot be allocated with EIPs will be in the "Pending" status. Note that this cannot be used for non-bill-by-IP accounts. | No                                                           |

For samples, see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).

## Default Quota

By default, up to 500 Pods can be scheduled to a pay-as-you-go super node in each cluster. If the desired number of Pods exceeds the quota limit, you can submit a ticket to apply for a higher quota. Tencent Cloud will assess your actual needs and increase your quota as appropriate.

### Applying for a higher quota

1. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to enter the ticket page.
2. In the **Problem description** field, enter a description such as "I want to apply for a higher quota for the Pods of cluster super node." Specify the target region and quota. Enter your mobile number and other information as instructed.
3. After providing all the necessary information, click **Submit Ticket**.

## Pod Limits

### Workload limits

The Pods for DaemonSet workloads won't be scheduled to super nodes.

### Service limits

For cluster services in [GlobalRouter mode](https://intl.cloud.tencent.com/document/product/457/38968), if externaltrafficpolicy = local, the traffic won't be forwarded to Pods scheduled to super nodes.

### Volume limits

The emptyDir, PVC, Secret, NFS, ConfigMap, DownloadAPI, and hostPath volumes are supported.
For PVC volumes:
- PV type: Only NFS, CephFS, hostPath, static CBS types are supported (CSI not supported).
- StorageClass type: Only user-defined and `cloud.tencent.com/qcloud-cbs` types are supported (CFS not supported).

### GPU limits

You must specify the `gpu-type` field in the annotation; otherwise, scheduling to super nodes is not supported. Different GPU Pod types come with different CPU and memory specifications, which don't need to be specified. If you need to specify them, make sure that they are identical to those supported by the GPU; otherwise, scheduling will fail.

### Other limits

- The super node feature is not available for clusters without any server nodes.
- Pods with the [static IP](https://intl.cloud.tencent.com/document/product/457/38974) enabled cannot be scheduled to super nodes.
- Pods that with hostIP specified use the Pod IP as the hostIP by default.
- Pods scheduled to super nodes are strictly isolated. If hard anti-affinity is enabled, scheduling to super nodes won't take effect, and it happens that multiple Pods of the same workload are scheduled to the same super node.
- Pods in the `tke-eni-ip-webhook` namespace cannot be scheduled to super nodes.

