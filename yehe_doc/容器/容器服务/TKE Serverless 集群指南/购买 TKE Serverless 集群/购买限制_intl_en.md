## Use Restrictions

Before using a TKE serverless cluster, you need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).



## Supported Regions
For more information on regions where TKE serverless clusters are supported, see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/457/41125). For more information on resource specifications, see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057).

## Resource Quotas

#### Cluster and Pod limits
| Resource | Limit | Description |
| --------- | --------- | --------- |
| Clusters in one region | 5 | Includes clusters that are being created and running. |
| Pods in one cluster | 100 | Includes all namespaces, workloads, and stateless and stateful pods. |
| Pod replicas for one workload | 100 | Includes all stateless and stateful pods in the workload. |
| The largest container instance size for the same region | 500 | Includes all stateless and stateful container instances. |

#### Other limits
All Pods in a TKE serverless cluster are independent computing and network instances in the cloud, which can be regarded as CVM instances and are therefore subject to the following limits:
1. When a workload is created, each Pod will be associated with a [security group](https://intl.cloud.tencent.com/document/product/215/38750) by default, and all Pod replicas in the same workload will be associated with the same security group. Each Pod is a CVM instance for the security group and is subject to the quota on the [number of CVM instances that can be associated with a security group](https://intl.cloud.tencent.com/document/product/215/38959).
2. When CLB Services are used, each Pod bound to the CLB instance is a CVM instance for the CLB instance and is subject to the quota on the [number of servers that can be bound to a forwarding rule in a CLB instance](https://intl.cloud.tencent.com/document/product/214/6187).

#### Applying for a higher quota
If the number of required resources exceeds the quota limit shown in the preceding table, you can submit a ticket to apply for a higher quota. Tencent Cloud will assess your actual needs and increase your quota as appropriate.
1. [Submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=2028&source=0&data_title=%E5%BC%B9%E6%80%A7%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1%20EKS&step=1). Select **Others** > **Create Now** to enter the ticket creation page.
2. In the **Problem description** field, enter a description such as "I want to apply for a higher quota for the TKE serverless cluster." Specify the target region, object, and quota. Enter your mobile number and other information as instructed.
3. Click **Submit Ticket**.
