

## Billing Items
The service fee for TKE consists of two parts, cluster management fee and Tencent Cloud service resources fee.
#### Cluster management fee
>! Tencent Cloud starts charging for managed clusters from 10:00, March 21, 2022 (UTC +8). See [Starting Charging for Managed Clusters](https://intl.cloud.tencent.com/document/product/457/45156).
>
**Managed clusters** incur the cluster management fee based on their cluster models. For more information, see [Cluster Management Fees].(#cluster).



#### Tencent Cloud services resources fees
Other Tencent Cloud services resources (such as CVM, CBS and CLB) created during the usage of TKE will be charged based on the billing mode for each resource. For more information, see [Tencent Cloud Services Resources Fees](#cloudproducts).


## Cluster Management Fees[](id:cluster)

### Billing mode
The billing mode of pay-as-you-go is usually adopted for TKE.

| Billing Item    | Billing Mode | Payment Method                                                     | Billing Unit |
| --------- | -------- | ------------------------------------------------------------ | -------- |
| Number of clusters | Pay-as-you-go | [Freeze the fees](https://intl.cloud.tencent.com/document/product/555/12039) at the time of purchase, and the service is billed at an hourly basis | USD/hour |

### Pricing
>? 
>- The nodes indicate Kubnernetss nodes, including CVM nodes, BM nodes, external nodes and virtual nodes.
>- Cluster management fees are not charged on clusters that are in idle status.
>
| Maximum Number of Nodes | Price (USD/hour) |
| ---------------- | -------------- |
| 5                | 0.02040816           |
| 20               | 0.06279435           |
| 50               | 0.11459969           |
| 100              | 0.19152276           |
| 200              | 0.40031397           |
| 500              | 0.8021978           |
| 1000             | 1.47252747           |
| 3000             | 2.44897959          |
| 5000             | 4.40188383          |


## Tencent Cloud Services Resources Fees[](id:cloudproducts)
Other Tencent Cloud services resources (such as CVM, CBS and CLB) created during the usage of TKE will be charged based on each billing mode. For more information, see billing description for each resource.

| Tencent Cloud Service | Documentation | 
|---------|---------|
| CVM | [CVM Billing Mode](https://intl.cloud.tencent.com/document/product/213/2180)| 
| CBS | [CBS Billing Overview](https://intl.cloud.tencent.com/document/product/213/2255)| 
| CLB | [CLB Billing Description](https://intl.cloud.tencent.com/document/product/214/36999)| 

>! TKE is a declarative service based on Kubernetes. When you do not need CLB, CBS or other IaaS service resources created by TKE, you must delete them in TKE console, otherwise, TKE will re-create them and continue to charge fees. For example, if you delete a CLB instance in CLB console instead of in TKE console, TKE will re-create a CLB instance based on declarative APIs.



