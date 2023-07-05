
TKE Serverless Cluster specifies the maximum resources allocated to a pod using [annotation specification](#Annotation) or [automatic Request and Limit calculation](#RequestLimit). You can select either method.




## Specifying by Annotation[](id:Annotation)
TKE Serverless Cluster can add `template annotation` in the YAML file of a workload to explicitly specify the pod resource specifications. For more information, see [Annotation Description](https://intl.cloud.tencent.com/document/product/457/36162).

## Automatically Calculating by Request and Limit[](id:RequestLimit)
TKE Serverless Cluster can calculate the Request and Limit parameters set for a workload to determine the resources required for running pods. The calculation method varies depending on the pod resource type. For more information on how to automatically calculate specified resource specifications based on the Request and Limit parameters, see [CPU specification calculation methods for pods](#CPUpod) and [GPU specification calculation methods for pods](#GPUpod).



>!
>- If `template annotation` is specified for a workload, the annotation configuration prevails and the Request and Limit parameters are not calculated.
>- For more information about Request and Limit resource allocation, see the supported CPU and GPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). If the set value varies greatly from the supported specifications, the allocation of a resource may exceed expectations, resulting in resource waste.
>- Regardless of how Request and Limit are set, the final calculation result will match with that in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057), and resources allocated to a pod will not exceed the allowed specifications.
>- If Request and Limit are not set for a container in a pod, the Request and Limit values of the container are regarded as 0.
>- If Request and Limit are not set for all containers in a pod, the default pod specifications are 1 core and 2 GiB.
>- Initcontainer and Container are calculated based on the following methods, and the larger value is used.

[](id:CPUpod)
### CPU specifications calculation methods for pods
#### Step 1. Calculate the total CPU and memory value of a pod.
 The total values are the **total Request value of all containers in a pod** and the **maximum Limit value of containers in a pod**, respectively.

#### Step 2. Match pod resource specifications based on the following table.
<table>
<tr>
<th>Total CPU and Memory Values</th> <th>Pod Resource Selection Rules</th>
</tr>
<tr>
<td>The total CPU and memory values are both 0.</td>
<td>The pod specifications are 1 core and 2 GiB.</td>
</tr>
<tr>
<td>Either the total CPU value or total memory value is 0.</td>
<td>Match the minimum value based on the non-0 total value.<br>For example, if the total CPU value is 0 cores, and the total memory value is 8 GiB, match the minimum CPU value in allowed specifications with 8 GiB memory. The selected pod specifications are 1 core and 8 GiB.</td>
</tr>
<tr>
<td>Neither the total CPU value nor total memory value is 0.</td>
<td>
Match resource specifications in <a href="https://intl.cloud.tencent.com/document/product/457/34057">Resource Specifications</a>. First, select a higher specification (specification A) with a CPU value the same as or similar to the total CPU value. Then, select a higher specification with a memory value similar to the total memory value.
	<ul  class="params">
	<li>If the total memory value is less than the minimum memory value in the memory range of specification A, select the minimum memory value in the memory range of specification A.</li>
	<li>If the total memory value is greater than the maximum memory value in the memory range of specification A, select a higher specification (specification B) with a memory value similar to the total memory value and change the total CPU value to that of specification B.</li>
	<li>If the total memory value is within the memory range of specification A, select the nearest larger dual-value.</li>
	</ul>
</td>
</tr>
<tr>
<td>Either the total CPU value or memory value exceeds the maximum specification.</td>
<td>An error occurs, and resource matching fails.</td>
</tr>
</table>

#### Sample
You can better understand the CPU specification calculation methods for pods based on the following examples.
<dx-tabs>
::: Example 1 
```yaml
resources:
    limits:
      cpu: "1"
      memory: 2Gi
    requests:
      cpu: "1"
      memory: 2Gi
```
**Result**: The selected pod specification is 1 core and 2 GiB.
:::
::: Example 2 
```yaml
## container1
resources:
    limits:
      cpu: "4"
      memory: 4Gi
    requests:
      cpu: "2"
      memory: 4Gi
## container2
resources:
    limits:
      cpu: "1"
      memory: 2Gi
    requests:
      cpu: "1"
      memory: 2Gi
```

**Note:**
Total CPU value: max((2+1),max(4,1)) = 4 cores
Total memory value: max((4+2),max(4,2)) = 6 GiB

**Result**: TKE Serverless Cluster does not support pod specifications of 4 cores and 6 GiB, and 6 GiB is less than the minimum memory value in the specifications with 4 CPU cores. Therefore, adjust the minimum memory value in the specifications with 4 CPU cores. The selected pod specifications are 4 cores and 8 GiB.
:::
</dx-tabs>

 
[](id:GPUpod)
### GPU specification calculation methods for pods
>?
>- Typically, GPUs have the same `nvidia.com/gpu` parameter value as vGPUs, and the value must be an integer.
>- vGPU can be regarded as an independent GPU type. For example, 1/4\*V100 indicates that 1/4 the computing power of a V100 GPU card is virtualized to a complete card. During resource allocation, one GPU card is applied for, that is, nvidia.com/GPU is 1.
>


#### Step 1. Calculate the total GPU value of a pod.
The total GPU value is the **total Request value of all containers in a pod**.

#### Step 2. Match pod resource specifications based on the following table.
<table>
<tr>
<th width="22%">Total CPU, Memory, and GPU Values</th>
<th>Pod Resource Matching Rules</th>
</tr>
<tr>
<td>The total values must comply with specification requirements, for example, 1, 2, 4, and 8.</td>
<td>First select a higher specification (specification A) with a GPU value the same as or similar to the total GPU value. Then, calculate the CPU and memory values based on the <a href="#CPUpod">CPU specification calculation methods for pods</a> to obtain the CPU specification (specification B).
<ul class="params">
<li>If the CPU and memory values of specification A are greater than or equal to those of specification B, select the GPU value of specification A. </li>
<li>If the CPU and memory values of specification A are less than those of specification B, select a higher GPU specification (specification C) with CPU and memory values similar to those of specification B. In this method, the allocated number of GPU cards are more than that needed, which should be avoided. <b>To prevent waste</b>, lower the CPU and memory request values. </li>
</ul>
</td>
</tr>
<tr>
<td>Any total value exceeds the maximum specifications.</td>
<td>An error occurs, and resource matching fails.</td>
</tr>
</table>

#### Sample
You can better understand the GPU specification calculation methods for pods based on the following examples.
<dx-tabs>
::: Example 1
```yaml
## eks.tke.cloud.tencent.com/gpu-type: V100
resources:
    limits:
      cpu: "8"
      memory: 32Gi
      nvidia.com/gpu: "1"
    requests:
      cpu: "4"
      memory: 16Gi
      nvidia.com/gpu: "1"
```

**Note**:
Total GPU value: 1
Total CPU value: max(4,8) = 8 cores
Total memory value: max(16,32) = 32 GiB

**Result**: 8 cores and 32 GiB are less than the CPU and memory values (8 cores and 40 GiB) of the V100 GPU specification (one card) in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). The ultimately selected pod specification is 8 cores, 40 GiB, and 1x V100.
:::
::: Example 2
```yaml
## eks.tke.cloud.tencent.com/gpu-type: V100
## container1
resources:
    limits:
      cpu: "8"
      memory: 32Gi
      nvidia.com/gpu: "1"
    requests:
      cpu: "4"
      memory: 16Gi
      nvidia.com/gpu: "1"
## container2
resources:
    limits:
      cpu: "32"
      memory: 128Gi
      nvidia.com/gpu: "1"
    requests:
      cpu: "16"
      memory: 64Gi
      nvidia.com/gpu: "1"
```

**Note**:
Total GPU value: 1+1 = 2
Total CPU value: max((4+16),max(8,32)) = 32 cores
Total memory value: max((16+64),max(32,128)) = 128 GiB

**Result**: 32 cores and 128 GiB are greater than the CPU and memory values (18 cores and 80 GiB) of the V100 GPU specification (two cards) but less than the CPU and memory values (36 cores and 160 GiB) of the V100 GPU specification (four cards).
	The ultimately selected pod specification is 36 cores, 160 GiB, and 4x V100, resulting in the waste of two GPU cards. Such a waste should be avoided.

:::
</dx-tabs>
 
<style>
	.params{margin:0px !important}
</style>

