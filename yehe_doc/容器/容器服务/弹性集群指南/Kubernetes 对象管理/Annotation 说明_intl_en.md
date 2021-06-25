## Workload Template Annotation Description
You can define `template annotation` in a YAML file to implement capabilities such as binding security groups and allocating resources for Pods. For more information about the configuration method, please see the following table.

>!
>- If no security group is specified, a Pod is bound with the `default` security group in the same region by default. Ensure that the network policy of the `default` security group does not affect the Pod.
>- To allocate GPU resources, you must specify `eks.tke.cloud.tencent.com/gpu-type`.
>- Except `eks.tke.cloud.tencent.com/gpu-type`, the other four annotations related to resource allocation in the following table are optional. If you specify them, ensure that they are correct.
> - To allocate CPU resources, you must specify both `cpu` and `mem` annotations and make sure that their values meet the CPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). In addition, you can select Intel or AMD CPUs to allocate by specifying `cpu-type`. AMD CPUs are more cost-effective. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055). 
>- To allocate GPU resources, you must specify the `cpu`, `mem`, `gpu-type`, and `gpu-count` annotations and ensure that their values meet the GPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057).


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
	<ul class="params">
	<li>Multiple security group IDs can be specified and separated by a comma (<code>,</code>), such as <code>sg-id1,sg-id2</code>.</li>
	<li>Network policies take effect based on the sequence of security groups.</li>
	<li>Please note that a single security group can be associated with only 2,000 computing instances, such as CVM instances and Elastic Kubernetes Service (EKS) Pods. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/15379" target="_blank">Security Group Limits</a>.</li>
	</ul>
</td>
<td> No. If you do not specify it, the <code>default</code> security group in the same region bound to the workload is associated by default.<br>If you specify it, ensure that the security group ID already exists in the region where the workload resides.</td></tr>
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
<td>Model of the CPU resources required by a Pod. Currently, the supported models include:
<ul  class="params">
<li>intel</li>
<li>amd</li>
<li>You can specify the model by priority. For example, `amd,intel` indicates AMD resource Pods will be created first. If the AMD resources in the selected region are insufficient, Intel resource Pods will be created.</li>
</ul>
For specific configurations supported by each model, please see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>.</td>
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
<td>eks.tke.cloud.tencent.com/gpu-count</td>
<td>Number of GPUs required by a Pod. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The unit is card by default.</td>
<td>No. If you specify it, ensure that the specification is supported.</td>
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
<tr>
<td>eks.tke.cloud.tencent.com/role-name</td>
<td>Associates a Pod with a CAM role. Please specify <a href="https://console.cloud.tencent.com/cam/role" target="_blank">CAM role name</a> as the value. In this way, the Pod can obtain the permission policies of the associated CAM role to facilitate cloud resource operations such as purchasing resources and reading from or writing to storage.</td>
<td>No. If you specify it, please make sure the specified CAM role exists.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/monitor-port</td>
<td>Opens a port for monitoring data for a Pod, so as to facilitate collection by PROM instance and other components.</td>
<td>No. If you do not specify it, the port will default to 9100.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/custom-metrics-url</td>
<td>Sets a custom monitoring metric pull address for a Pod. The monitoring data opened at this address will be automatically read and reported by the monitoring component.</td>
<td>No. If you specify it, please ensure that the opened data protocol can be recognized by the monitoring system, such as the Prometheus protocol and cloud monitoring data protocol.</td>
</tr>
</tr>
</tbody></table>

### Sample
The following example shows the complete GPU specifications of the security group bound to a Pod.
```
apiVersion: apps/v1
kind: StatefulSet
metadata:
   generation: 1
   labels:
     k8s-app: nginx
     qcloud-app: nginx
   name: nginx
   namespace: default
spec:
   progressDeadlineSeconds: 600
   replicas: 1
   revisionHistoryLimit: 10
   selector:
     matchLabels:
       k8s-app: nginx
       qcloud-app: nginx
   strategy:
     rollingUpdate:
       maxSurge: 1
       maxUnavailable: 0
     type: RollingUpdate
   template:
     metadata:
       annotations:
         eks.tke.cloud.tencent.com/cpu: "2"
         eks.tke.cloud.tencent.com/gpu-count: "1"
         eks.tke.cloud.tencent.com/gpu-type: 1/4*V100
         eks.tke.cloud.tencent.com/mem: 10Gi
         eks.tke.cloud.tencent.com/security-group-id: "sg-dxxxxxx5,sg-zxxxxxxu"
         eks.tke.cloud.tencent.com/role-name: "cam-role-name"
         eks.tke.cloud.tencent.com/monitor-port: "9123"
         eks.tke.cloud.tencent.com/custom-metrics-url: "http://localhost:8080/metrics"
       creationTimestamp: null
       labels:
         k8s-app: nginx
         qcloud-app: nginx
     spec:
       containers:
       - image: nginx:latest
         imagePullPolicy: Always
         name: nginx
         resources:
           limits:
             cpu: "1"
             memory: 2Gi
             nvidia.com/gpu: "1"
           requests:
             cpu: "1"
             memory: 2Gi
             nvidia.com/gpu: "1"
         terminationMessagePath: /dev/termination-log
         terminationMessagePolicy: File
       dnsPolicy: ClusterFirst
       imagePullSecrets:
       - name: qcloudregistrykey
       restartPolicy: Always
       schedulerName: default-scheduler
       securityContext: {}
       terminationGracePeriodSeconds: 30
```



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

### Sample
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



## Service Annotation Description

EKS allows you to use existing CLBs to create services accessed through the public or private network. If you want to provide idle CLBs to created services or use the same CLB in a cluster, you can add annotations.

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
<td>service.kubernetes.io/tke-existed-lbid</td>
<td>The Service is created with the existing <a href="https://intl.cloud.tencent.com/document/product/214/524" target="_blank">CLB</a>. Specify the ID of the CLB instance you want to use as the value.</td>
<td>No. If you specify it, ensure that the specified CLB instance ID exists.</td>
</tr>
<tr>
<td>service.kubernetes.io/qcloud-share-existed-lb</td>
<td>By default, multiple Services cannot share the same CLB instance. If you hope that a Service uses the CLB occupied by other Services, please add this annotation and specify the value as <code>"true"</code>.</td>
<td>No. If you do not specify it, a CLB instance cannot be reused by default.</td>
</tr>
</tr>
</tbody></table>

The elastic cluster also supports the same expansion protocol as the TKE cluster. For more information, see [Service Extension Protocol](https://intl.cloud.tencent.com/document/product/457/39141).

>!
>- Ensure that your EKS does not share the same CLB with the CVM.
>- When the existing CLBs are used:
>   - Only CLBs created through the CLB console can be used. You cannot reuse CLBs automatically created by TKE.
>   - Ports of Services that share the same existing CLB cannot be the same.
>   - Cross-cluster Services cannot share the same CLB.


### Sample
```
apiVersion: v1
kind: Service
metadata:
   annotations:
     service.kubernetes.io/tke-existed-lbid: lb-pxxxxxxq
     service.kubernetes.io/qcloud-share-existed-lb: true
   name: servicename
   namespace: default
spec:
   externalTrafficPolicy: Cluster
   ports:
   - name: tcp-80-80
     nodePort: 31728
     port: 80
     protocol: TCP
     targetPort: 80
   sessionAffinity: None
   type: LoadBalancer
```

<style>
	.params{margin:0px !important}
</style>
