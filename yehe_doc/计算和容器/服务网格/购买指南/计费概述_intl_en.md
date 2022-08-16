

The billing mode of Tencent Cloud Mesh is pay-as-you-go (postpaid). Tencent Cloud Mesh is billed at a service fee based on two dimensions, that is, the number of clusters and the number of sidecars in a mesh.
>! Tencent Cloud Mesh is officially billed from 10:00 on April 20, 2022. For details, see [Tencent Cloud Mesh Billing Notifications](https://intl.cloud.tencent.com/document/product/1152/47429).

### Billable Items
| Billable Item | Billing Mode | Payment Mode | Billing Unit |
|--|--|--|--|
| Number of clusters | Pay-as-you-go | [Freeze the fees](https://intl.cloud.tencent.com/document/product/555/12039) at the time of purchase, and the clusters are billed at an hourly basis | USD/hour |
| Number of sidecars | Pay-as-you-go | [Freeze the fees](https://intl.cloud.tencent.com/document/product/555/12039) at the time of purchase, and the sidecars are billed at an hourly basis | USD/hour |


#### Number of Clusters
Each cluster in the mesh is billed at a management fee of $0.2474 USD/hour. The number of clusters is based on the number of valid clusters every hour on the hour. Clusters that have been deleted but not disassociated are invalid and will not be counted as valid clusters.

#### Number of Sidecars
Each mesh provides 100 free sidecars. After 100 sidecars are exceeded, each sidecar is billed at a service fee of $0.0008 USD/hour.
The number of sidecars used for billing is the total online hours of all sidecars. Therefore, the number of billed sidecars is less than or equal to the actual number of online sidecars. The online duration of the sidecars is calculated based on the pod life cycle duration. For example, in the current hour, there are 204 sidecars running in the mesh, among which 200 sidecars run for 30 minutes, and the other four sidecars each run for 20 minutes, and therefore the actual use duration is: (200 × 30 + 4 × 20)/60 = 101.33 hours. In this case, the number of sidecars used for billing is 101.33. As a user has 100 free quotas, 1.33 sidecars will actually incur fees.

## Billing Example
>? To simplify the calculation, it is assumed that the sidecars in the following cases have been used for a full month.

#### Case 1:
**Scenario**: A user creates a Tencent Cloud Mesh instance and adds a TKE cluster to the mesh. The cluster contains 500 service pods, only a specific namespace foo has enabled automatic sidecar injection, and 90 pods have been injected with sidecars.

**Fee**: Calculation is made based on that the mesh runs for one month (estimated based on 30 days). The mesh contains one cluster, and the cluster fee is: 0.2474 × 24 × 30 = $178.128. As the total number of sidecars in the mesh does not exceed 100, there is no additional fee for the sidecars. The total monthly fee of the mesh is $178.128.


#### Case 2:

**Scenario**: A user creates a Tencent Cloud Mesh instance and adds two TKE clusters to the mesh. Cluster 1 contains 1,000 service pods, only a specific namespace foo has enabled automatic sidecar injection, and 100 pods have been injected with sidecars. Cluster 2 contains 2,000 service pods, only a specific namespace foo has enabled automatic sidecar injection, and 100 pods have been injected with sidecars.

**Fee**: Calculation is made based on that the mesh runs for one month (estimated based on 30 days). The mesh contains two clusters, and the cluster fee is: 0.2474 × 24 × 30 x 2 = $356.256. As the total number of sidecars in the mesh is 200 and exceeds a free quota 100, the sidecar fee is: 100 × 0.0008 × 24 × 30 = $57.6. The total monthly fee of the mesh is: 356.256 + 57.6 = $413.856.

## Other Fees
The fees billed for Tencent Cloud Mesh include only the management and service fees of Tencent Cloud Mesh. If you use other cloud resources and services in the business process, such as Cloud Load Balancer (CLB), Cloud Log Service (CLS), Application Performance Management (APM), you also need to pay fees according to the billing rules of the corresponding products. For specific billing details, see the billing overview of each product.

| Cloud Product | Billing Description |
| :----------- | :----------------------------------------------------------- |
| TKE/EKS | [TKE Billing Overview](https://intl.cloud.tencent.com/document/product/457/6770) |
| CLB | [CLB Billing Overview](https://intl.cloud.tencent.com/document/product/214/36999) |
| CLS | [CLS Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509) |

