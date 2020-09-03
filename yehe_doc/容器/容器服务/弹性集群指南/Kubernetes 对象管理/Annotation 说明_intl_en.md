## Workload Template Annotation Description
You can define `template annotation` in a YAML file to implement capabilities such as binding security groups and allocating resources for pods. For more information on the configuration method, see the following table.

>!
>- If no security group is specified, a pod is bound to the `default` security group in the same region by default. Ensure that the network policy of the `default` security group does not affect the pod.
>- To allocate GPU resources, you must specify `eks.tke.cloud.tencent.com/gpu-type`.
>- Except `eks.tke.cloud.tencent.com/gpu-type`, the other four annotations related to resource allocation in the following table are optional. If you specify them, ensure that they are correct.
>- To allocate CPU resources, you must specify both `cpu` and `mem` and make sure that their values meet the CPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). In addition, you can select Intel or AMD CPUs to allocate by specifying `cpu-type`. AMD CPUs are more cost-effective. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/457/34055). 
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
<td>Default security group bound to a workload. Specify the <a href="https://console.cloud.tencent.com/cvm/securitygroup" target="_blank">security group ID</a>.
	<ul class="params">
	<li>Multiple security group IDs can be specified and separated by a comma (<code>,</code>), such as <code>sg-id1,sg-id2</code>.</li>
	<li>Network policies take effect based on the sequence of security groups.</li>
	</ul>
</td>
<td> No. If you do not specify it, the <code>default</code> security group in the same region bound to the workload is associated by default. <br>If you specify it, ensure that the security group ID already exists in the region where the workload resides.</td></tr>
<tr>
<td>eks.tke.cloud.tencent.com/cpu</td>
<td>Number of CPU cores required by a pod. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The unit is core by default.</td>
<td>No. If you specify it, ensure that the specifications are supported and specify the <code>cpu</code> and <code>mem</code> parameters.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/mem</td>
<td>Memory required by a pod. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The unit must be included in the value, for example, 512 MiB, 0.5 GiB, or 1 GiB.</td>
<td>No. If you specify it, ensure that the specifications are supported and specify the <code>cpu</code> and <code>mem</code> parameters.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/cpu-type</td>
<td>Model of the CPU resources required by a pod. Currently, supported models include:
<ul  class="params">
<li>intel</li>
<li>amd</li>
</ul>
For more information on configurations supported by different models, see <a href="https://console.cloud.tencent.com/cvm/securitygroup" target="_blank">Resource Specifications</a>.</td>
<td>No. If you do not specify it, the CPU type is not specified forcibly by default. The system will calculate the most suitable specifications according to <a href="https://intl.cloud.tencent.com/document/product/457/36161" target="_blank">Methods for Specifying Resource Specifications</a>. If the calculated specifications are supported by both Intel and AMD, Intel CPUs are preferred.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/gpu-type</td>
<td>Model of the GPU resources required by a pod. Currently, supported models include:
<ul  class="params">
<li>1/4*V100</li>
<li>1/2*V100</li>
<li>V100</li>
<li>1/4*T4</li>
<li>1/2*T4</li>
<li>T4</li>
</ul>
For more information on configurations supported by different models, see <a href="https://console.cloud.tencent.com/cvm/securitygroup" target="_blank">Resource Specifications</a>.</td>
<td>If GPU resources are required, this option is required. When specifying it, ensure that the GPU model is supported. Otherwise, an error will be reported.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/gpu-count</td>
<td>Number of GPUs required by a pod. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The unit is card by default.</td>
<td>No. If you specify it, ensure that the specifications are supported.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/static-ip</td>
<td>Fixed IP address for a pod. You can enable this feature by setting the value to <code>true</code>. If this feature is enabled, the IP address of a StatefulSet or Bare pod will not change when the pod is updated or restarted.</td>
<td>No. This annotation is valid only for StatefulSet and Pod workloads.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/role-name</td>
<td>CAM role associated to a pod. The value is a <a href="https://console.cloud.tencent.com/cam/role" target="_blank">CAM role name</a>. A pod can obtain the permission policy of the associated CAM role to facilitate cloud resource operations such as purchasing resources and reading from or writing to storage.
<td>No. If you specify it, ensure that the CAM role exists.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/monitor_port</td>
<td>Sets an open port for monitoring data for a pod, to facilitate collection by Prometheus and other components.</td>
<td>No. If you do not specify it, the default value is 9100.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/custom_metrics_url</td>
<td>Sets the custom monitoring metric pull address for a pod. The monitoring data opened at this address will be automatically read and reported by the monitoring component.</td>
<td>No. If you specify it, please ensure that the opened data protocol can be recognized by the monitoring system, such as the Prometheus protocol and cloud monitoring data protocol.</td>
</tr>
</tr>
</tbody></table>

### Sample
The following example shows the complete GPU specifications of the security group bound to a pod.
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
        eks.tke.cloud.tencent.com/static-ip: "true"
        eks.tke.cloud.tencent.com/role-name: "cam-role-name"
        eks.tke.cloud.tencent.com/monitor_port: "9123"
        eks.tke.cloud.tencent.com/custom_metrics_url: "http://localhost:8080/metrics"
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


## EKS Annotation Description

Elastic Kubernetes Service (EKS) allows you to use existing CLBs to create services accessed through the public or private network. If you want to provide idle CLBs to created services or use the same CLB in a cluster, you can add annotations.

>!
>- Ensure that your EKS does not share the same CLB with the CVM.
>- When existing CLBs are used:
>  - Only CLBs created through the CLB console can be used. You cannot reuse CLBs automatically created by Tencent Kubernetes Engine (TKE).
>  - Ports of services that share the same existing CLB cannot be the same.
>  - Cross-cluster services cannot share the same CLB.


### Sample
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    service.kubernetes.io/tke-existed-lbid: lb-pxxxxxxq
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
