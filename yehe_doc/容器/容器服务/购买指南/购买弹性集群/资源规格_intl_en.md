## Overview
Elastic Kubernetes Service (EKS) frees you from managing cluster nodes. However, to properly allocate resources and accurately calculate fees, you need to specify resource specifications for pods when deploying a workload. Tencent Cloud allocates computing resources to the workload and calculates the corresponding fees based on the specified specifications.

When you use the Kubernetes API or Kubectl to create a workload for EKS, you can use annotations to specify resource specifications. If annotations are not used, EKS will calculate the specifications based on the container parameters set for the workload, such as Request and Limit. For more information, see [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).

>!
> - The resource specifications indicate the maximum amount of resources available for containers in a pod.
> - The following tables list the supported CPU and GPU specifications. Ensure that allocated resources do not exceed the supported specifications.
> - The total amount of resources specified by Request for all the containers in a pod cannot exceed the maximum pod specification.
> - The amount of resources specified by Limit for any container in a pod cannot exceed the maximum pod specification.


## CPU Specifications

The following table lists CPU specifications that EKS provides for pods in all regions where CPU resources are supported. EKS also provides a set of CPU options. Different CPU sizes correspond to different memory ranges. Select the CPU specification as needed when creating a workload.

#### Intel
| CPU (Cores) | Memory Range (GiB) | Granularity of Memory Range (GiB) |
| -------|-------|------- |
| 0.25 | 0.5, 1, 2 | - |
| 0.5 | 1, 2, 3, 4 | - |
| 1 | 1 - 8 | 1 |
| 2 | 4 - 16 | 1 |
| 4 | 8 - 32 | 1 |
| 8 | 16 - 32 | 1 |
| 12 | 24 - 48 | 1 |
| 16 | 32 - 64 | 1 |

#### Star Lake AMD
The AMD processor provides high performance with high reliability, security, and stability based on the Star Lake servers developed by Tencent Cloud. For more information, see [CVM Standard SA2 Introduction](https://intl.cloud.tencent.com/document/product/213/11518).

| CPU (Cores) | Memory Range (GiB) | Granularity of Memory Range (GiB) |
| -------|-------|------- |
| 1 | 1 - 4 | 1 |
| 2 | 2 - 8 | 1 |
| 4 | 4 - 16 | 1 |
| 8 | 8 - 32 | 1 |
| 16 | 16 - 32 | 1 |
| 32 | 32 - 64 | 1 |

## GPU Specifications

The following table lists the GPU specifications that EKS provides for pods. Different GPU card models and sizes map to different CPU and memory options. Select the GPU specification as needed when creating a workload.
>!If you create, manage, and use GPU workloads using a YAML file, see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).

| GPU Model | GPU (Cards) | CPU (Cores) | Memory (GiB) |
| ------- | ------- | ------- | ------- |
| 1/4 Tesla V100-NVLINK-32G | 1 | 2 | 10 |
| 1/2 Tesla V100-NVLINK-32G | 1 | 4 | 20 |
| Tesla V100-NVLINK-32G | 1 | 8 | 40 |
| Tesla V100-NVLINK-32G | 2 | 18 | 80 |
| Tesla V100-NVLINK-32G | 4 | 36 | 160 |
| Tesla V100-NVLINK-32G | 8 | 72 | 320 |
| 1/4 NVIDIA T4 | 1 | 4 | 20 |
| 1/2 NVIDIA T4 | 1 | 10 | 40 |
| NVIDIA T4 | 1 | 20 | 80 |
| NVIDIA T4 | 2 | 40 | 160 |
| NVIDIA T4 | 4 | 80 | 320 |



## Supported Regions
The following table describes the regions, availability zones, and resource types that are currently supported by EKS.


### China
<table class="table-striped">
<tbody>
	<tr>
		<th>Region</th>
		<th>AZ</th>
	</tr>
	<tr>
		<td rowspan="3">South China (Guangzhou)<br> ap-guangzhou</td>
		<td>Guangzhou Zone 3<br> ap-guangzhou-3</td>	
	</tr>
	<tr>
		<td>Guangzhou Zone 4<br>ap-guangzhou-4</td>
	</tr>	
		<tr>
		<td>Guangzhou Zone 6<br>ap-guangzhou-6</td>
	</tr>	
	<tr>
		<td rowspan="4">East China (Shanghai)<br>ap-shanghai</td>
		<td>Shanghai Zone 2</br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>Shanghai Zone 3</br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>Shanghai Zone 4</br>ap-shanghai-4</td>
	</tr>
	<tr>
		<td>Shanghai Zone 5 <br>ap-shanghai-5</td>
	</tr>
	<tr>
		<td rowspan="3">East China (Nanjing)<br> ap-nanjing</td>
		<td>Nanjing Zone 1<br>ap-nanjing-1</td></tr>
			<tr><td>Nanjing Zone 2<br> ap-nanjing-2</td></tr>
	<tr><td>Nanjing Zone 3<br> ap-nanjing-3</td></tr>
	<tr>
			<td rowspan="5">North China (Beijing)<br>ap-beijing</td>
			<td>Beijing Zone 3</br>ap-beijing-3</td>
	</tr>
	<tr>
		<td>Beijing Zone 4</br>ap-beijing-4</td>
	</tr>
	<tr>
		<td>Beijing Zone 5 <br>ap-beijing-5</td>
	</tr>
	<tr>
		<td>Beijing Zone 6<br>ap-beijing-6</td>
	</tr>
	<tr>
		<td>Beijing Zone 7<br>ap-beijing-7</td>
	</tr>
		<tr>
		<td rowspan="2">Southwest China (Chengdu)<br>ap-chengdu</td>
		<td>Chengdu Zone 1<br>ap-chengdu-1</td>
	</tr>
	<tr>
		<td>Chengdu Zone 2</br>ap-chengdu-2</td>
	</tr>	   
			<tr>
		<td rowspan="1">Hong Kong, Macao and Taiwan, China (Hong Kong)
<br> ap-hongkong</td>
		<td>Hong Kong Zone 2 (Hong Kong nodes can cover services in the China regions of Hong Kong, Macao, and Taiwan)
<br> ap-hongkong-2</td>
	</tr>
	
</tbody>
</table>

### Other countries and regions	
<table class="table-striped">
	<tbody>
	<tr>
			<th>Region</th>
			<th>Availability Zone</th>
		</tr>
		<tr>
			<td>Southeast Asia (Jakarta)<br>ap-jakarta</td>
			<td>Jakarta Zone 1 (Jakarta nodes can cover services in Southeast Asia)<br>ap-jakarta-1</td>
		</tr>
       <tr>
			<td  rowspan="2">South Asia Pacific (Mumbai)<br>ap-mumbai</td>
			<td>Mumbai Zone 1 (Mumbai nodes can cover services in South Asia)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>Mumbai Zone 2 (Mumbai nodes can cover services in South Asia) <br>ap-mumbai-2</td>
		</tr>
		<tr>
			<td rowspan="2">Western US (Silicon Valley)<br>na-siliconvalley</td>
			<td>Silicon Valley Zone 1 (Silicon Valley nodes can cover services in Western US)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>Silicon Valley Zone 2 (Silicon Valley nodes can cover services in Western US)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td>Europe (Frankfurt) <br>eu-frankfurt</td>
			<td>Frankfurt Zone 1 (Frankfurt nodes can cover services in Europe)<br>eu-frankfurt-1</td>
		</tr>
		<td >Europe (Moscow)<br>eu-moscow</td>
		<td>Moscow Zone 1 (Moscow nodes can cover services in Europe)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>
