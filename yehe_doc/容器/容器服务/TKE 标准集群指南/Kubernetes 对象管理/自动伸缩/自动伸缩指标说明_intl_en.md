
Horizontal Pod Autoscaler (HPA) can automatically adjust the number of Pods for services according to the average CPU utilization of target Pods and other metrics. You can set auto scaling triggering metrics in the console, including CPU, memory, disk, network, and GPU metrics. You can also use these metrics when creating and editing HPAs through YAML files. This document describes how to configure a YAML file.

## Auto Scaling Metrics
The following tables list the details of the auto scaling metrics:
>?Each variable under `metricName` has its own unit that is listed in the default unit column. You can omit such units when compiling the YAML file.

### CPU metrics

<table>
<tr>
	<th width="17.8%">Metric Name in the Console</th><th width="14.1%">Unit in the Console</th><th width="17.1%">Remarks</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default Unit</th>
	</tr>
	<tr>
	<td>CPU Usage</td>
	<td>Core</td>
	<td>Number of CPU cores used by the Pod</td>
	<td>Pods</td>
	<td>k8s_pod_cpu_core_used</td>
	<td>Core</td>
	</tr>
	<tr>
	<td>CPU Utilization<br>(per node)</td>
	<td>%</td>
	<td>Percentage of total CPU of the node used by the Pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_node</td>
	<td>% </td>
	</tr>
	<tr>
	<td>CPU Utilization <br>(per Request)</td>
	<td>% </td>
	<td>Ratio of the total number of CPU cores used by the Pod and the value of Request specified by the container in the Pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>CPU Utilization<br>(per Limit)</td>
	<td>%</td>
	<td>Ratio of the total number of CPU cores used by the Pod and the sum of Limit specified by the container in the Pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_limit</td>
	<td>%</td>
	</tr>
</table>



### Disk metrics	

<table>
<tr>
	<th width="17.8%">Metric Name in the Console</th><th width="14.1%">Unit in the Console</th><th width="17.1%">Remarks</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default Unit</th>
	</tr>
	<tr>
	<td>Disk Write Traffic</td>
	<td>KB/s</td>
	<td>Pod's disk write rate</td>
	<td>Pods</td>
	<td>k8s_pod_fs_write_bytes</td>
	<td>B/s</td>
	</tr>
	<tr>
	<td>Disk Read Traffic</td>
	<td>KB/s</td>
	<td> Pod's disk read rate</td>
	<td>Pods</td>
	<td>k8s_pod_fs_read_bytes</td>
	<td>B/s</td>
	</tr>
	<tr>
	<td>Disk Read IOPS</td>
	<td>Times/s </td>
	<td>Number of I/O times Pod reads data from disk </td>
	<td>Pods</td>
	<td>k8s_pod_fs_read_times</td>
	<td>Times/s</td>
	</tr>
	<tr>
	<td>Disk Write IOPS</td>
	<td>Times/s</td>
	<td>Number of I/O times Pod writes data to disk</td>
	<td>Pods</td>
	<td>k8s_pod_fs_write_times</td>
	<td> Times/s </td>
	</tr>
</table>


### Network	

<table>
<tr>
	<th width="17.8%">Metric Name in the Console</th><th width="14.1%">Unit in the Console</th><th width="17.1%">Remarks</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default Unit</th>
	</tr>
	<td>Inbound Network Bandwidth</td>
	<td>Mbps</td>
	<td>Sum of inbound bandwidth of all containers per Pod</td>
	<td>Pods</td>
	<td>k8s_pod_network_receive_bytes_bw</td>
	<td>Bps</td>
	</tr>
	<tr>
	<td>Outbound Network Bandwidth</td>
	<td>Mbps</td>
	<td>Sum of outbound bandwidth of all containers per Pod</td>
	<td>Pods</td>
	<td>k8s_pod_network_transmit_bytes_bw</td>
	<td>Bps</td>
	</tr>
	<tr>
	<td>Inbound Network Traffic</td>
	<td>KB/s</td>
	<td>Sum of inbound traffic of all containers per Pod</td>
	<td>Pods</td>
	<td>k8s_pod_network_receive_bytes</td>
	<td>B/s</td>
	</tr>
	<tr>
	<td>Outbound Network Traffic</td>
	<td>KB/s</td>
	<td>Sum of outbound traffic of all containers per Pod</td>
	<td>Pods</td>
	<td>k8s_pod_network_transmit_bytes</td>
	<td>B/s</td>
	</tr>
	<tr>
	<td>Network Packets In</td>
	<td>Count/s</td>
	<td>Sum of inbound packets of all containers per Pod</td>
	<td>Pods</td>
	<td>k8s_pod_network_receive_packets</td>
	<td>Count/s</td>
	</tr>
	<tr>
	<td>Network Packets Out</td>
	<td>Count/s</td>
	<td>Sum of outbound packets of all containers per Pod</td>
	<td>Pods</td>
	<td>k8s_pod_network_transmit_packets</td>
	<td>Count/s	</td>
	</tr>
</table>



### Memory

<table>
<tr>
	<th width="17.8%">Metric Name in the Console</th><th width="14.1%">Unit in the Console</th><th width="17.1%">Remarks</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default Unit</th>
	</tr>
	<tr>
	<td>Memory usage</td>
	<td>MiB</td>
	<td>Amount of memory used by the pod</td>
	<td>Pods</td>
	<td>k8s_pod_mem_usage_bytes</td>
	<td>B</td>
	</tr>
	<tr>
	<td>Memory Usage<br>(excluding cache)	</td>
	<td>MiB</td>
	<td>Pod Memory Usage, excluding cache</td>
	<td>Pods</td>
	<td>k8s_pod_mem_no_cache_bytes</td>
	<td>B</td>
	</tr>
	<tr>
	<td> Memory Utilization<br>(per node)</td>
	<td>%</td>
	<td>Percentage of total memory of the node used by the Pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_node</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory Utilization<br>(per node, excluding cache)</td>
	<td>%</td>
	<td>Percentage of total memory of the node used by the Pod, excluding cache</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_no_cache_node</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory Utilization<br>(per Request)</td>
	<td>%</td>
	<td>Percentage of total memory of the Request used by the Pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory Utilization<br>(per Request, excluding cache)</td>
	<td>%</td>
	<td>Percentage of total memory of the Request used by the Pod, excluding cache</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_no_cache_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory Utilization<br>(per Limit)</td>
	<td>%</td>
	<td>Percentage of Pod memory usage to the Limit value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_limit</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory Utilization<br>(per Limit, excluding cache)</td>
	<td>%</td>
	<td>Percentage of Pod memory usage to the Limit value, excluding cache</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_no_cache_limit</td>
	<td>%</td>
	</tr>
</table>




### GPU
>? The following GPU-related triggering metrics can only be used in EKS clusters.  

<table>
<tr>
	<th width="17.8%">Metric Name in the Console</th><th width="14.1%">Unit in the Console</th><th width="17.1%">Remarks</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default Unit</th>
	</tr>
	<tr>
	<td>GPU Usage</td>
	<td>CUDA Core</td>
	<td>Pod GPU usage</td>
	<td>Pods</td>
	<td>k8s_pod_gpu_used</td>
	<td>CUDA Core</td>
	</tr>
	<tr>
	<td>GPU Applications</td>
	<td>CUDA Core</td>
	<td>Pod GPU applications</td>
	<td>Pods</td>
	<td>k8s_pod_gpu_request</td>
	<td>CUDA Core</td>
	</tr>
	<tr>
	<td> GPU Utilization<br>(per Request)</td>
	<td>%</td>
	<td>Percentage of GPU usage to the Request value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_gpu_used_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>GPU Utilization<br>(per node)</td>
	<td>%</td>
	<td>GPU usage percentage in the node</td>
	<td>Pods</td>
	<td>k8s_pod_rate_gpu_used_node</td>
	<td>%</td>
 </tr>
 <tr>
	<td>GPU Memory Usage</td>
	<td>Mib</td>
	<td>Pod GPU memory usage</td>
	<td>Pods</td>
	<td>k8s_pod_gpu_memory_used_bytes</td>
	<td>B</td>
 </tr>
 <tr>
	<td>GPU Memory Applications</td>
	<td>MiB</td>
	<td>Pod GPU memory applications</td>
	<td>Pods</td>
	<td>k8s_pod_gpu_memory_request_bytes</td>
	<td>B</td>
 </tr>
 <tr>
	<td>GPU Memory Utilization<br>(per Request)</td>
	<td>%</td>
	<td>Percentage of GPU memory usage to the Request value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_gpu_memory_used_request</td>
	<td>%</td>
 </tr>
 <tr>
	<td>GPU Memory Utilization<br>(per node)</td>
	<td>%</td>
	<td>GPU memory usage percentage in the node</td>
	<td>Pods</td>
	<td>k8s_pod_rate_gpu_memory_used_node</td>
	<td>%</td>
 </tr>
</table>


## Creating and Editing HPA Through YAML 
You can create and edit an HPA through a YAML file. Below is a sample configuration file that defines an HPA named `example`, which will be triggered when the CPU usage reaches `1`. The instance range is 1–2.

>! TKE is compatible with the native Resource types.

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
  - type: Pods	# Support using Resource
    pods:
      metricName: k8s_pod_cpu_core_used
      targetAverageValue: "1"
  scaleTargetRef:
    apiVersion: apps/v1beta2
    kind: Deployment
    name: nginx
```


