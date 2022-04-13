
## Billing Mode

For pods scheduled to the virtual nodes, there are two billing mode options, pay-as-you-go and spot billing. See [Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054), [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055), and [Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).


## Kubernetes Version

It supports clusters of v1.16 and above.

## Default Quota

By default, up to **100 Pods** can be scheduled to a virtual node for each cluster. If the number of required Pods exceeds the quota limit, you can submit a ticket to apply for a higher quota. Tencent Cloud will assess your actual needs and increase your quota as appropriate.

### Applying for a higher quota
1. [Submit a ticket](https://console.cloud.tencent.com/workorder/category). On the **Submit a ticket** page, select the product name and issue type (Others), and then complete the ticket information.
2. In the **Problem description** field, enter a description such as "I want to apply for a higher quota for the Pod of cluster virtual node." Then, enter the region where your cluster is located and your desired quota. Finally, enter your mobile number and other information as instructed.
3. Click to contact customer service.

## Pod Configurations

### Pod specification configuration

Pod specification configuration is the basis for billing the available resources and services when the container is running. For the resource specification configuration of virtual node Pod and how to specify the resource specification, please see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057) and [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).

### Pod temporary storage

When each Pod scheduled to the virtual node is created, a temporary image storage of no more than 20 GiB will be allocated.

>!
>- Temporary image storage will be deleted when the Pod lifecycle ends. Therefore, please do not store important data in it.
>- The actual available storage will be less than 20 GiB due to the stored images.
>- It is recommended to mount important data and large files to Volume for persistent storage.

### Pod network

The Pods scheduled to virtual node are on the same VPC network plane as the Tencent Cloud services such as CVM and TencentDB. Each Pod takes an IP address in the VPC subnet.

A Pod can connect to other Pods or Tencent Cloud services in the same VPC without any performance losses.

### Pod isolation

The Pod scheduled to the virtual node has the same security isolation as the CVM. Pods are scheduled and created on the underlying physical server of Tencent Cloud, and the resource isolation between Pods is guaranteed by virtualization technology during the creation.

### Other special configurations

You can define `template annotation` in a YAML file to implement capabilities such as binding security groups, allocating resources and allocating EIP for Pods scheduled to the virtual node. For more information about the configuration method, please see the following table:

>!
>- If no security group is specified, the Pod will be bound to the specified security group of the node pool by default. Please ensure that the network policy of the security group does not affect the normal operation of the Pod. For example, you need to open port 80 if the Pods provide service via port 80.
>- To allocate CPU resources, you must specify both `cpu` and `mem` annotations and make sure that their values meet the CPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). In addition, you can select Intel or AMD CPUs to allocate by specifying `cpu-type`. AMD CPUs are more cost-effective. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055). 
>- To allocate GPU resources through the method specified in the annotation, you must specify the `gpu-type` and `gpu-count` annotations and ensure that their values meet the GPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057).

<table>
<thead>
<tr>
<th width="20%">Annotation Key</th>
<th width="40%">Annotation Value and Description</th>
<th width="40%">Required</th>
</tr>
</thead>
<tbody>
<tr>
<td>eks.tke.cloud.tencent.com/security-group-id</td>
<td>Default security group bound with a workload. Specify the <a href="https://console.cloud.tencent.com/cvm/securitygroup" target="_blank">security group ID</a>.
	<li>You can specify multiple security group IDs and separate each of them by commas (<code>,</code>). For example, <code>sg-id1,sg-id2</code>.</li>
	<li>Network policies take effect based on the sequence of security groups.</li>
</td>
<td>Not required. Make sure that the security group ID exists in the region of the workload.<br>If it’s not specified, the workload is bound to the security group specified in the node pool by default.</td></tr>
<tr>
<td>eks.tke.cloud.tencent.com/cpu</td>
<td>Number of CPU cores required by a Pod. See <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>.</td>
<td>Not required. Make sure the entered specification is supported and both the <code>cpu</code> and <code>mem</code> are specified.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/mem</td>
<td>Memory required by a Pod. See <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The unit must be included in the value, for example, `512Mi`, `0.5Gi` and `1Gi`.</td>
<td>Not required. Make sure the entered specification is supported and both the <code>cpu</code> and <code>mem</code> are specified.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/cpu-type</td>
<td>Model of the CPU resources required by a Pod. The supported models include:
<li>intel</li>
<li>amd</li>
<li>Specific model, such as `S4`, `S3`</li>
See <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>.</td>
<td>Not required. If it’s not specified, the system automatically choose the best-suit specification. See <a href="https://intl.cloud.tencent.com/document/product/457/36161" target="_blank">Specifying Resource Specifications</a>. If the matched specifications are supported by both Intel and AMD, Intel CPUs are preferred.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/gpu-type</td>
<td>Model of the GPU resources required by a Pod. The supported models include:
<ul  class="params">
<li>V100</li>
<li>1/4*T4</li>
<li>1/2*T4</li>
<li>T4</li>
<li>You can specify the model by priority. For example, “T4,V100” indicates T4 resource Pods will be created first. If the T4 resources in the selected region are insufficient, V100 resource Pods will be created.</li>
</ul>
For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>.</td>
<td>If GPUs are required, this option is required. When specifying it, ensure that the GPU model is supported. Otherwise, an error will be reported.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/gpu-count</td>
<td>Number of GPU cards required by a Pod. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. </td>
<td>Not required. Make sure that the entered specification is supported.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/retain-ip</td>
<td>Whether to retain the IP when the Pod is deleted. <code>"true"</code>: Retain the IP after the deletion of a Pod (for 24 hours by default. If the Pod is rebuilt the retention period, this IP can be retrieve.<b>It’s only valid for `statefulset` and `rawpod`.</b></td>
<td>Not required</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/retain-ip-hours</td>
<td>The retention period of the IP of a Pod in hours. It can be up to 8760 hours (one year).<b>It’s only valid for `statefulset` and `rawpod`.</b></td>
<td>Not required</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/eip-attributes</td>
<td>Attributes of the EIP associated with Pods of the Workload. When the value is `""`, it indicates that the default EIP configuration is used. You can enter the API parameter json of the EIP in within "" to realize custom configuration. For example, if the value of annotation is '{"InternetMaxBandwidthOut":2}', it means the bandwidth is 2M. Note that it is only applicable to bill-by-IP accounts.</td>
<td>Not required</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/eip-claim-delete-policy</td>
<td>Whether to release the EIP once the Pod is deleted. `Never`: Do not release. This parameter takes effect only when eks.tke.cloud.tencent.com/eip-attributes is specified. Note that it is only applicable to bill-by-IP accounts.</td>
<td>Not required</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/eip-id-list</td>
<td>For a StatefulSet workload, you can specify multiple existing EIPs (such as "eip-xx1, eip-xx2"). Note that the number of StatefulSet pods can not exceed the number of EIPs specified in the annotation. Otherwise, the pods without EIPs go pending. It is only applicable to bill-by-IP accounts.</td>
<td>Not required</td>
</tr>
</tbody></table>


For samples, see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).

## Pod Limits

### Workload limits

The Pods for DaemonSet workloads are not scheduled to the virtual node.

### Service limits

For cluster services using [GlobalRouter Mode](https://intl.cloud.tencent.com/document/product/457/38968), if externaltrafficpolicy = local, the traffic is not forwarded to Pods scheduled to the virtual node.

### Volume limits

Pods that mount with hostpath volumes are not scheduled to the virtual node.


### Other limits

- The virtual node feature is not available for the cluster without any server nodes.
- Pods that have enabled the [Static IP Address](https://intl.cloud.tencent.com/document/product/457/38974) cannot be scheduled to the virtual node.
- Pods with hostPort specified are not scheduled to the virtual node.
- Pods that with hostIP specified use the Pod IP as the hostIP by default.
- If Anti-affinity is enabled, only one pod is created on the virtual node for the same workload.
- If the container logs are stored in the specified node file, and log collection is performed through the node file, the Pod logs on the virtual node cannot be collected.
