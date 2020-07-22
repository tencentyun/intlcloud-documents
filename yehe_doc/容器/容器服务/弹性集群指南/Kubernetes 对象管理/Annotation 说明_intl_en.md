## Workload Template Annotations
You can define `template annotation` in a YAML file to implement capabilities such as binding security groups and the allocation of resources for pods. For more information about the configuration method, see the following table.

>!
>- If no security group is specified, a pod is bound to the `default` security group in the same region by default. Ensure that the network policy of the `default` security group does not affect the normal operation of the pod.
>- To allocate GPU resources, specify `eks.tke.cloud.tencent.com/gpu-type`.
>- The annotations related to resource allocation in the following table, except `eks.tke.cloud.tencent.com/gpu-type`, are optional. Ensure that they are correct if you specify them.
>- To allocate CPU resources, specify both the `cpu` and `mem` annotations and ensure that their values meet the CPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057). In addition, you can allocate Intel or AMD CPU resources by specifying `cpu-type`. AMD CPU resources are more cost effective. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055). 
>- To allocate GPU resources, specify the `cpu`, `mem`, `gpu-type`, and `gpu-count` annotations and ensure that their values meet the GPU specifications in [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057).


<table>
<thead>
<tr>
<th width="20%">Annotation Key</th>
<th width="40%">Annotation Value and Description</th>
<th width="40%">Required?</th>
</tr>
</thead>
<tbody>
<tr>
<td>eks.tke.cloud.tencent.com/security-group-id</td>
<td>Default security group bound to a workload. Specify the <a href="https://console.cloud.tencent.com/cvm/securitygroup" target="_blank">security group ID</a>.
	<ul class="params">
	<li>You can specify multiple security group IDs and separate them with commas (<code>,</code>), such as <code>sg-id1,sg-id2</code>.</li>
	<li>Network policies take effect in the order of security groups.</li>
	</ul>
</td>
<td> No. If it is not specified, the workload is bound to the <code>default</code> security group in the same region by default. <br>If it is specified, ensure that the security group ID already exists in the region to which the workload belongs. </td></tr>
<tr>
<td>eks.tke.cloud.tencent.com/cpu</td>
<td>Number of CPU cores required by a pod. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. It is a number and no unit of measurement is required.</td>
<td>No. If it is specified, ensure that the specifications are supported and specify the <code>cpu</code> and <code>mem</code> parameters.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/mem</td>
<td>Memory required by a pod. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. The unit must be included in the value, for example, 512 MiB, 0.5 GiB, or 1 GiB.</td>
<td>No. If it is specified, ensure that the specifications are supported and specify the <code>cpu</code> and <code>mem</code> parameters.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/cpu-type</td>
<td>Model of the GPU resources required by a pod. Currently, supported models include:
<ul class="params">
<li>Intel</li>
<li>AMD</li>
</ul>
For more information about configurations supported by different models, see <a href="https://console.cloud.tencent.com/cvm/securitygroup" target="_blank">Resource Specifications</a>.</td>
<td>No. If it is not specified, the CPU type is not specified forcibly by default. The system will calculate the most suitable specifications based on the <a href="https://intl.cloud.tencent.com/document/product/457/36161" target="_blank">method for configuring resource specifications</a>. If the calculated specifications are supported by both Intel and AMD, Intel is preferred.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/gpu-type</td>
<td>Model of the GPU resources required by a pod. Currently, supported models include:
<ul class="params">
<li>1/4*V100</li>
<li>1/2*V100</li>
<li>V100</li>
<li>1/4*T4</li>
<li>1/2*T4</li>
<li>T4</li>
</ul>
For more information about configurations supported by different models, see <a href="https://console.cloud.tencent.com/cvm/securitygroup" target="_blank">Resource Specifications</a>.</td>
<td>If GPU resources are required, this parameter is required. Ensure that the specified GPU model is supported. Otherwise, an error will be reported.</td>
</tr>
<tr>
<td>eks.tke.cloud.tencent.com/gpu-count</td>
<td>Number of GPU cards required by a pod. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34057" target="_blank">Resource Specifications</a>. It is a number and no unit of measurement is required.</td>
<td>No. If it is specified, ensure that the specifications are supported.</td>
</tr>
</tr>
</tbody></table>

### Sample
The following sample shows the complete GPU specifications of the security group bound to a pod.
```
apiVersion: apps/v1
kind: Deployment
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


## EKS Annotations

Elastic Kubernetes Service (EKS) allows you to use existing CLBs to create services accessed through the public or private network. If you want to provide idle CLBs to services to be created or use the same CLB in a cluster, you can add annotations.

>!
>- Ensure that your EKS does not share the same CLB with the CVM.
>- When you use existing CLBs:
    >- Only CLBs created in the CLB console can be used. You cannot reuse CLBs automatically created by Tencent Kubernetes Engine (TKE).
    >- Ports of services that share the same existing CLB cannot be the same.
    >- Cross-cluster services cannot share the same CLB.


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
