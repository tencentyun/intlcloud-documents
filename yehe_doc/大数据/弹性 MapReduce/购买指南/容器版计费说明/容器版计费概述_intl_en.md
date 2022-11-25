## Billing Overview
Container-based EMR clusters are deployed in EKS and free you from managing cluster nodes. However, to reasonably allocate resources and accurately calculate fees, you need to specify resource specifications for Pods when configuring a job. Tencent Cloud allocates computing resources to the workload and calculates the fees based on the specifications.
Currently, container-based EMR is pay-as-you-go by the amount of EKS CPU and memory resources required to run services.
>! 
>1. The following prices are only for the configurations of CPU and memory, which don’t include cloud data disk and bandwidth fees.
>2. For cloud disk prices, see [Billing Overview](https://www.tencentcloud.com/document/product/362/32415).

## Billable Items
<table>
<tr>
<th>Resource Type</th>
<th>EKS Resource (Intel)</th>
<th>	EKS Resource (AMD)</th>
</tr><tr>
<td rowspan=2,colspan=2>Billable items</td>
<td>CPU	</td>
<td>CPU	</td>
</tr><tr>
<td>Memory	</td>
<td>Memory	</td>
</tr></table>
Container-based EMR provides Intel resources by default. If you need AMD resources, configure the job accordingly.
The service calculates applicable fees based on the container resource type you select.

Billing formula: Fees = billable item configuration * resource unit price * execution time

For more information on configurations currently supported for billable items, see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057).
For more information on how to select configurations for billable items, see [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).

## Pricing
### Pay-as-you-go (Intel)

| Billable Item | 	Price (Per Second)	 | Price (Per Hour) |
|---------|---------|---------|
| CPU	| 0.0003438 USD/core	| 0.020628 USD/core/hour |
| Memory	|0.0001434 USD/GB| 0.008604 USD/GB/hour |

### Pay-as-you-go (AMD)

| Billable Item | 	Price (Per Second)	 | Price (Per Hour) |
|---------|---------|---------|
| CPU	| 0.0001518 USD/core	| 0.009108 USD/core/hour |
| Memory	| 0.0000882 USD/GB	|0.005292 USD/GB/hour |


## Overdue Payment Policy
For more information, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/1026/34537).