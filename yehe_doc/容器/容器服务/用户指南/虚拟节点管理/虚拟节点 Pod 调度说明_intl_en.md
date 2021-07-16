## Billing Mode

Pods scheduled to the virtual node adopt the pay-as-you-go billing mode. For details, please see [Elastic Clusters Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054), [Elastic Clusters Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055), and [Elastic Clusters Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).

## Pod Specification Configuration

Pod specification configuration is the basis for billing the available resources and services when the container is running. For the specification configuration of virtual node Pod and how to specify the resource specification, please see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057) and [Specifying Resource Specifications](https://intl.cloud.tencent.com/document/product/457/36161).

## Kubernetes Version

Only the Kubernetes clusters of v1.16 and later versions are supported.

## Default Quota

By default, up to **100 Pods** can be scheduled to the virtual node for each cluster. If the number of required Pods exceeds the quota limit, you can submit a ticket to apply for a higher quota. Tencent Cloud will assess your actual needs and increase your quota as appropriate.

#### Applying for a higher quota

1. Please [Submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1). On the **Submit a ticket** page, select the product name and issue type (Others), and then complete the ticket information.
2. In the **Problem description** field, enter a description such as "I want to apply for a higher quota for the Pod of cluster virtual node." Then, enter the region where your cluster is located and your desired quota. Finally, enter your mobile number and other information as instructed.
3. After providing all the necessary information, click **Submit Ticket** to submit the ticket.

## Pod Description

#### Pod temporary storage

When each Pod scheduled to the virtual node is created, a temporary image storage of no more than 20 GiB will be allocated.

>!
>- Temporary image storage will be deleted when the Pod lifecycle ends. Therefore, please do not store important data in it.
>- The actual available storage will be less than 20 GiB due to the stored images.
>- It is recommended to mount important data and large files to Volume for persistent storage.

#### Pod network

The Pods scheduled to virtual node are on the same VPC network plane as the Tencent Cloud services such as CVM and TencentDB. Each Pod will use an IP address of the VPC subnet.

Pod and Pod, Pod and other Tencent Cloud services in the same VPC can communicate directly without any performance losses.

#### Pod isolation

The Pod scheduled to the virtual node has the same security isolation as the CVM. Pods are scheduled and created on the underlying physical server of Tencent Cloud, and the resource isolation between Pods is guaranteed by virtualization technology during the creation.




## Virtual Node Annotation Description
EKS supports the virtual nodes. You can specify annotations in a YAML file to implement capabilities such as custom DNS, as shown below:

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
<td>eks.tke.cloud.tencent.com/resolv-conf</td>
<td>Queries the list of IP addresses for the DNS server while resolving the domain name, for example <code>nameserver 8.8.8.8</code>.
<br>You can use <code>kubectl edit node eklet-subnet-xxxx</code> to add this annotation.
<br>After the modification, the Pods scheduled to this virtual node will adopt this DNS configuration by default.</td>
<td>No</td>
</tr>
</tr>
</tbody></table>

#### Example
The example of a custom DNS configuration for a virtual node is as follows:

```
apiVersion: v1
kind: Node
metadata:
    annotations:
      eks.tke.cloud.tencent.com/resolv-conf:|
	   	nameserver 4.4.4.4
        nameserver 8.8.8.8
    
	
```




## Notes on Scheduling

#### Special configuration

You can define `template annotation` in a YAML file to implement capabilities such as binding security groups and allocating resources for Pods scheduled to the virtual node. For more information about the configuration method, please see the following table.

>!
>- If no security group is specified, the Pod will be bound to the specified security group of the node pool by default. Please ensure that the network policy of the security group does not affect the normal operation of the Pod. For example, you need to open port 80 if the Pods provide service via port 80.
>- To allocate CPU resources, you must specify both `cpu` and `mem` annotations and make sure that their values meet the CPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). In addition, you can select Intel or AMD CPUs to allocate by specifying `cpu-type`. AMD CPUs are more cost-effective. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055). 


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
	<li>You can specify multiple security group IDs and separate them by commas (<code>,</code>). For example, <code>sg-id1,sg-id2</code>.</li>
	<li>Network policies take effect based on the sequence of security groups.</li>
</td>
<td>No. If you do not specify it, the workload is bound to the specified security group of the node pool by default.<br>If you specify it, ensure that the security group ID already exists in the region to which the workload belongs.</td></tr>
<tr>
<td>eks.tke.cloud.tencent.com/cpu</td>
<td>Number of CPU cores required by a Pod. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The unit is core by default.</td>
<td>No. If you specify it, ensure that the specifications are supported and specify the <code>cpu</code> and <code>mem</code> parameters.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/mem</td>
<td>Memory required by a Pod. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The unit must be included in the value, for example, 512 MiB, 0.5 GiB, or 1 GiB.</td>
<td>No. If you specify it, ensure that the specifications are supported and specify the <code>cpu</code> and <code>mem</code> parameters.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/cpu-type</td>
<td>Model of the GPU resources required by a Pod. Currently, supported models include:
<li>intel</li>
<li>amd</li>
For more information about configurations supported by different models, see <a href="https://console.cloud.tencent.com/cvm/securitygroup" target="_blank">Resource specifications</a>.</td>
<td>No. If you do not specify it, the CPU type is not forcibly specified by default. The system will match the most suitable specifications according to <a href="https://intl.cloud.tencent.com/document/product/457/36161" target="_blank">Specifying Resource Specifications</a>. If the matched specifications are supported by both Intel and AMD, Intel CPUs are preferred.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/gpu-type</td>
<td>Model of the GPU resources required by a Pod. Currently, the supported models include:
<ul  class="params">
<li>V100</li>
<li>1/4*T4</li>
<li>1/2*T4</li>
<li>T4</li>
<li>You can specify the model by priority. For example, “T4,V100” indicates T4 resource Pods will be created first. If the T4 resources in the selected region are insufficient, V100 resource Pods will be created.</li>
</ul>
For specific configurations supported by each model, please see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>.</td>
<td>If GPUs are required, this option is required. When specifying it, ensure that the GPU model is supported. Otherwise, an error will be reported.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/retain-ip</td>
<td>The static IP of a Pod. Enter the value <code>"true"</code> to enable this feature. If a Pod with the static IP enabled is terminated, its IP will be retained 24 hours by default. If the Pod is rebuilt within 24 hours after termination, its IP can still be used. Otherwise, its IP may be occupied by other Pod.</td>
<td>No</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/retain-ip-hours</td>
<td>Modifies the default retention duration of the Pod’s static IP. Enter a number. Unit: hour. Default value: 24 hours. The IP can be retained up to one year.</td>
<td>No</td>
</tr>
</tbody></table>



For samples, please see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).


#### Workload limits

The Pods for workloads of the DaemonSet type will not be scheduled to the virtual node.

#### Service limits

If the cluster service using [GlobalRouter Mode](https://intl.cloud.tencent.com/document/product/457/38968) has enabled externaltrafficpolicy = local, the traffic will not be forwarded to the Pod scheduled to the virtual node.

#### Volume limits

The Pods that mount volumes of hostpath type will not be scheduled to the virtual node.


#### Notes

- The virtual node feature is not available for the cluster without any server nodes.
- The Pods that occupy the CPU resource cannot be scheduled to the virtual node.
- The Pods that have enabled the [Static IP Address](https://intl.cloud.tencent.com/document/product/457/38974) cannot be scheduled to the virtual node.
- The Pods that have specified the hostPort will not be scheduled to the virtual node.
- The Pods that have specified the hostIP will use the Pod IP as the value of hostIP by default.
- If the anti-affinity feature is enabled, only one of the Pods with the same workload will be created on the virtual node.
- If the container logs are stored in the specified node file, and log collection is performed through the node file, the Pod logs on the virtual node cannot be collected.






## The Relationship Between Virtual Node and Cluster Auto Scaling

If [Cluster Scaling](https://intl.cloud.tencent.com/document/product/457/30638) and virtual node are enabled for the cluster at the same time, Pods will be scheduled to the virtual node, and the scaling out will not be triggered. If the Pod cannot be scheduled to the virtual node due to the above scheduling limits, the node scaling out will be triggered normally.



