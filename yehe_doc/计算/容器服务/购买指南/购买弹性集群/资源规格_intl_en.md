## Overview
With Elastic Kubernetes Service (EKS), you can ignore cluster nodes. However, to properly allocate resources and accurately calculate fees, you need to specify resource specifications for a pod when deploying a workload. Based on the specified specifications, Tencent Cloud allocates resources to the workload and calculates the fees of the workload.

When creating a workload for EKS through the Kubernetes API or kubectl, you also need to specify the resource specifications. For more information, see [Workload Management](https://intl.cloud.tencent.com/document/product/457/34043).

>
> - The resource specification indicates the maximum amount of resources available for the containers in a pod.
> - The total amount of resources specified by Request for all the containers in a pod cannot exceed the corresponding resource specification of the pod.
> - The amount of resources specified by Limit for any container in a pod cannot exceed the corresponding resource specification of the pod.
> - You must specify the resource specifications for a pod when creating a workload for the pod. Otherwise, the creation fails.



## Supported Regions
The following table describes the regions, availability zones, and resource types that are currently supported by EKS. In the future, EKS will be supported in other regions.

<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>Availability Zone</th>
		<th>Supported Resource Type</th>
	</tr>
	<tr>
		<td rowspan="1">South China (Guangzhou)<br> ap-guangzhou</td>
		<td>Guangzhou Zone 3<br>ap-guangzhou-3</td>
		<td>CPU</td>
	</tr>	
	<tr>
		<td rowspan="2">East China (Shanghai)<br>ap-shanghai</td>
		<td>Shanghai Zone 2<br>ap-shanghai-2</td>
		<td>CPU</td>
	</tr>
	<tr>
		<td>Shanghai Zone 3<br>ap-shanghai-3</td>
		<td>CPU</td>
	</tr>
	<tr>
			<td rowspan="1">North China (Beijing)<br>ap-beijing</td>
			<td>Beijing Zone 3<br>ap-beijing-3</td>
			<td>CPU</td>
	</tr>
</tbody>
</table>

## CPU Specifications

EKS provides the following CPU specifications for pods in all regions where CPU resources are supported. EKS also provides a set of CPU options, and different CPU sizes correspond to different memory ranges. When creating a work, you must specify the CPU specification based on your actual need.

| CPU/Core | Memory Range/GiB | Granularity of Memory Range/GiB |
| -------|-------|------- |
| 0.25 | 0.5, 1, 2 | - |
| 0.5 | 1, 2, 3, 4 | - |
| 1 | 2 - 8 | 1 |
| 2 | 4 - 16 | 1 |
| 4 | 8 - 32 | 1 |
| 8 | 16 - 32 | 1 |
| 12 | 24 - 48 | 1 |
| 16 | 32 - 64 | 1 |

