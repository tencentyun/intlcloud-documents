Horizontal Pod Autoscaler (HPA) uses various metrics, such as target instance CPU usage, to adjust the number of Pods to automatically scale in or out. You can use the console to configure these metrics, including CPU, memory, disk, network, and GPU metrics. You can also use YAML files to create or modify HPAs. This article also contains a sample YAML file.

## Metrics
The following table is a list of metrics used the HPA:
> Each variable in the `metricName` column has a Default unit. You can omit such units when editing the YAML file.

### CPU metrics

<table>
<tr>
	<th width="17.8%">Metric name (Console)</th><th width="14.1%">Unit (Console)</th><th width="17.1%">Description</th>
	<th width="6.6%">Type</th><th width="33%">metricName</th><th width="11.4%">Default unit</th>
	</tr>
	<tr>
	<td>CPU utilization</td>
	<td>Cores</td>
	<td>CPU utilization of the Pod</td>
	<td>Pods</td>
	<td>k8s_pod_cpu_core_used</td>
	<td> Cores </td>
	</tr>
	<tr>
	<td>CPU utilization <br>(% of total resources)</td>
	<td>%</td>
	<td>The percentage of the CPU utilization out of all cores allocated to the Pod.</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_resource</td>
	<td>%</td>
	</tr>
	<tr>
	<td>CPU utilization<br>(% of request)</td>
	<td>%</td>
	<td>The percentage of CPU utilization to the request value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>CPU utilization<br>(% of limit)</td>
	<td>%</td>
	<td>The percentage of CPU utilization to the limit value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_limit</td>
	<td>%</td>
	</tr>
</table>

### Memory metrics

<table>
<tr>
	<th width="17.8%">Metric name (Console)</th><th width="14.1%">Unit (Console)</th><th width="17.1%">Description</th>
	<th width="6.6%">Type</th><th width="33%">metricName</th><th width="11.4%">Default unit</th>
	</tr>
	<tr>
	<td>Memory usage</td>
	<td>Mib</td>
	<td>Pod memory usage</td>
	<td>Pods</td>
	<td>k8s_pod_mem_usage_bytes</td>
	<td>B</td>
	</tr>
	<tr>
	<td>Memory utilization <br>(% of allocated resources)</td>
	<td>%</td>
	<td>The percentage of used memory out of all memory allocated to the Pod.</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_bytes_resource</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory utilization<br>(% of request)</td>
	<td>%</td>
	<td>The percentage of memory usage to the request value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory utilization<br>(% of limit)</td>
	<td>%</td>
	<td>The percentage of memory usage to the limit value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_limit</td>
	<td>%</td>
	</tr>
</table>







## Using YAML files to Create and Modify HPAs 
You can use YAML files to create and edit HPAs. The following is a sample YAML file. It creates an HPA called example which is triggered when CPU utilization reaches 1 and the number of Pods ranges from 1 to 2.  
```
apiVersion: autoscaling/v2beta1
kind: HorizontalPodAutoscaler
metadata:
  name: example
  namespace: default
  labels:
    qcloud-app: example
spec:
  minReplicas: 1
  maxReplicas: 2
  metrics:
  - type: Pods
    pods:
      metricName: k8s_pod_cpu_core_used
      targetAverageValue: "1"
  scaleTargetRef:
    apiVersion: apps/v1beta2
    kind: Deployment
    name: nginx
```
