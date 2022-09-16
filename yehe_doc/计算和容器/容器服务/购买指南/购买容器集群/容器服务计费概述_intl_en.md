
### Billable Items
The service fees for TKE consists of two parts, **cluster management fees** and **Tencent Cloud service resources fees**.
- **Cluster management fees**
>! Tencent Cloud starts charging for managed clusters from 10:00, March 21, 2022 (UTC +8). See [Starting Charging for Managed Clusters](https://intl.cloud.tencent.com/zh/document/product/457/45156).
>
**Managed clusters** incur the cluster management fees based on their cluster models. For more information, see [Cluster Management Fees].(#cluster).

- **Tencent Cloud service resources fees**
Other Tencent Cloud services resources (such as CVM, CBS and CLB) created during the usage of TKE will be charged based on the billing mode for each resource. For more information, see [Tencent Cloud Services Resources Fees](#cloudproducts).

## Cluster Management Fees[](id:cluster)

### Billing Mode
The billing mode of pay-as-you-go is usually adopted for TKE.

| Billing Item    | Billing Mode | Payment Method                                                     | Billing Unit |
| --------- | -------- | ------------------------------------------------------------ | -------- |
| Number of clusters | Pay-as-you-go | [Freeze the fees](https://intl.cloud.tencent.com/document/product/555/12039) at the time of purchase, and the service is billed at an hourly basis | USD/hour |

### Recommendations for small clusters
- If your cluster has only a small number of nodes (less than 20), we highly recommend you use [TKE Serverless Cluster](https://intl.cloud.tencent.com/document/product/457/34040) . With TKE Serverless cluster, you can deploy workloads and pay for actual container usage, with no need to purchase nodes and pay cluster management fees.
- You can choose to migrate your existing TKE general clusters as needed in the following ways:
	- Conduct smooth business migration through [super nodes](https://intl.cloud.tencent.com/document/product/457/39759) to reduce the number of nodes in the TKE general cluster and thereby lower the cluster management fees (such fees are not charged for super nodes; for more information, see [Pricing](#price) below).
	- Completely migrate the TKE general cluster to the TKE serverless cluster through the migration tool as instructed in [Guide on Migrating Resources in a TKE Managed Cluster to an TKE Serverless Cluster](https://intl.cloud.tencent.com/document/product/457/47002). If you encounter any problems, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.


### Pricing[](id:price)
>! 
>- The unit prices are varied depending on the region. Please refer to the prices displayed in the console. 
- Read the [Purchase Instructions](https://intl.cloud.tencent.com/document/product/457/45158) carefully before you select the specification.
>- The billing cycle of a cluster starts when the cluster is created. You can view the cluster creation time by going to the **TKE console** > **Basic Information**.




| Cluster Specification | Price (USD/hour) |
| ---------------- | -------------- |
| L5                | 0.02040816           |
| L20               | 0.06279435           |
| L50               | 0.11459969           |
| L100              | 0.19152276           |
| L200              | 0.40031397           |
| L500              | 0.8021978            |
| L1000             | 1.47252747           |
| L3000             | 2.44897959           |
| L5000             | 4.40188383           |

## Tencent Cloud Service Resources Fees[](id:cloudproducts)
Other Tencent Cloud service resources (such as CVM, CBS and CLB) created during the usage of TKE will be charged based on each billing mode. For more information, see billing description for each resource.

| Tencent Cloud Service | Documentation | 
|---------|---------|
| CVM | [CVM Billing Mode](https://intl.cloud.tencent.com/document/product/213/2180)| 
| CBS | [CBS Billing Overview](https://intl.cloud.tencent.com/document/product/213/2255)| 
| CLB | [CLB Billing Description](https://intl.cloud.tencent.com/document/product/214/36999)| 

>! TKE is a declarative service based on Kubernetes. When you do not need CLB, CBS or other IaaS service resources created by TKE, you must delete them in TKE console, otherwise, TKE will re-create them and continue to charge fees. For example, if you delete a CLB instance in CLB console instead of in TKE console, TKE will re-create a CLB instance based on declarative APIs.
