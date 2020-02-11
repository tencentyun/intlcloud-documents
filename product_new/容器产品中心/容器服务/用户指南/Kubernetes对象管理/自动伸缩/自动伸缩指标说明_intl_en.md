
Horizontal Pod Autoscaler (HPA) can automatically scale the number of Pods for services according to the average CPU utilization of target Pods and other metrics. You can set auto-scaling triggering metrics in the console. Such metrics include CPU, memory, disk, network, and GPU metrics. You can also use these metrics when creating and editing HPAs with YAML files. This document provides an example of configuring a YAML file.

## Autoscaling Metrics
The following table provides details about autoscaling metrics:
> Each variable under `metricName` has its own unit which is listed in the default unit column. You can omit such units when compiling the YAML file.

### CPU Metrics

<table>
<tr>
	<th width="17.8%">Metric name (Console)</th><th width="14.1%">Unit (Console)</th><th width="17.1%">Description</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default unit</th>
	</tr>
	<tr>
	<td>CPU usage</td>
	<td>Core(s)</td>
	<td>Pod’s CPU usage</td>
	<td>Pods</td>
	<td>k8s_pod_cpu_core_used</td>
	<td> Core(s) </td>
	</tr>
	<tr>
	<td>CPU utilization<br>(% of node)</td>
	<td>%</td>
	<td>Percentage of total CPU of the node used by the Pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_node</td>
	<td>% </td>
	</tr>
	<tr>
	<td>CPU utilization<br>(% of request)</td>
	<td>% </td>
	<td>Percentage of Pod’s CPU usage to the pre-set request value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>CPU utilization<br>(% of limit)</td>
	<td>%</td>
	<td>Percentage of Pod’s CPU usage to the pre-set limit value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_limit</td>
	<td>%</td>
	</tr>
</table>



### Disk Metrics	

<table>
<tr>
	<th width="17.8%">Metric name (Console)</th><th width="14.1%">Unit (Console)</th><th width="17.1%">Description</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default unit</th>
	</tr>
	<tr>
	<td>Disk write traffic</td>
	<td>KB/s</td>
	<td> Pod’s disk write speed</td>
	<td>Pods</td>
	<td>k8s_pod_fs_write_bytes</td>
	<td>B/s</td>
	</tr>
	<tr>
	<td>Disk read traffic</td>
	<td>KB/s</td>
	<td> Pod’s disk read speed</td>
	<td>Pods</td>
	<td>k8s_pod_fs_read_bytes</td>
	<td>B/s</td>
	</tr>
	<tr>
	<td>Disk read IOPS</td>
	<td>Times/s </td>
	<td>Number of I/O times Pod reads data from disk </td>
	<td>Pods</td>
	<td>k8s_pod_fs_read_times</td>
	<td>Times/s</td>
	</tr>
	<tr>
	<td>Disk write IOPS</td>
	<td>Times/s</td>
	<td>Number of I/O times Pod writes data to disk</td>
	<td>Pods</td>
	<td>k8s_pod_fs_write_times</td>
	<td> Times/s </td>
	</tr>
</table>


### Network Metrics	

<table>
<tr>
	<th width="17.8%">Metric name (Console)</th><th width="14.1%">Unit (Console)</th><th width="17.1%">Description</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default unit</th>
	</tr>
	<td>Network ingress bandwidth</td>
	<td>Mbps</td>
	<td>Sum of Pod’s ingress bandwidth</td>
	<td>Pods</td>
	<td>k8s_pod_network_receive_bytes_bw</td>
	<td>Bps</td>
	</tr>
	<tr>
	<td>Network egress bandwidth</td>
	<td>Mbps</td>
	<td>Sum of Pod’s egress bandwidth</td>
	<td>Pods</td>
	<td>k8s_pod_network_transmit_bytes_bw</td>
	<td>Bps</td>
	</tr>
	<tr>
	<td>Network ingress traffic</td>
	<td>KB/s</td>
	<td>Sum of Pod’s ingress traffic</td>
	<td>Pods</td>
	<td>k8s_pod_network_receive_bytes</td>
	<td>B/s</td>
	</tr>
	<tr>
	<td>Network egress traffic</td>
	<td>KB/s</td>
	<td>Sum of Pod’s egress traffic</td>
	<td>Pods</td>
	<td>k8s_pod_network_transmit_bytes</td>
	<td>B/s</td>
	</tr>
	<tr>
	<td>Network inbound packets</td>
	<td>Packets/s</td>
	<td> Sum of Pod’s inbound packets</td>
	<td>Pods</td>
	<td>k8s_pod_network_receive_packets</td>
	<td>Packets/s</td>
	</tr>
	<tr>
	<td>Network outbound packets</td>
	<td>Packets/s</td>
	<td> Sum of Pod’s outbound packets</td>
	<td>Pods</td>
	<td>k8s_pod_network_transmit_packets</td>
	<td>Packets/s</td>
	</tr>
</table>



### Memory Metrics

<table>
<tr>
	<th width="17.8%">Metric name (Console)</th><th width="14.1%">Unit (Console)</th><th width="17.1%">Description</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default unit</th>
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
	<td>Memory usage<br>(excluding cache)</td>
	<td>Mib</td>
	<td>Pod memory usage, excluding cache</td>
	<td>Pods</td>
	<td>k8s_pod_mem_no_cache_bytes</td>
	<td>B</td>
	</tr>
	<tr>
	<td> Memory utilization<br>(% of node)</td>
	<td>%</td>
	<td>Percentage of total memory of the node used by the Pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_node</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory utilization<br>(% of node, excluding cache)</td>
	<td>%</td>
	<td>Percentage of total memory of the node used by the Pod, excluding cache</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_no_cache_node</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory utilization<br>(% of request)</td>
	<td>%</td>
	<td>Percentage of Pod memory usage to the request  value </td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory utilization<br>(% of request, excluding cache)</td>
	<td>%</td>
	<td>Percentage of Pod memory usage to the request  value, excluding cache</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_no_cache_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory utilization<br>(% of limit)</td>
	<td>%</td>
	<td>Percentage of Pod memory usage to the limit value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_limit</td>
	<td>%</td>
	</tr>
	<tr>
	<td>Memory utilization<br>(% of limit, excluding cache)</td>
	<td>%</td>
	<td>Percentage of Pod memory usage to the limit value, excluding cache</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_no_cache_limit</td>
	<td>%</td>
	</tr>
</table>




### GPU Metrics

<table>
<tr>
	<th width="17.8%">Metric name (Console)</th><th width="14.1%">Unit (Console)</th><th width="17.1%">Description</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default unit</th>
	</tr>
	<tr>
	<td>GPU usage</td>
	<td>CUDA Core</td>
	<td>Pod GPU usage</td>
	<td>Pods</td>
	<td>k8s_pod_gpu_used</td>
	<td>CUDA Core</td>
	</tr>
	<tr>
	<td>GPU applications</td>
	<td>CUDA Core</td>
	<td>Pod GPU applications</td>
	<td>Pods</td>
	<td>k8s_pod_gpu_request</td>
	<td>CUDA Core</td>
	</tr>
	<tr>
	<td> GPU utilization<br>(% of request)</td>
	<td>%</td>
	<td>Percentage of GPU usage to the request value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_gpu_used_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>GPU utilization<br>(% of node)</td>
	<td>%</td>
	<td>Percentage of node taken up by GPU usage</td>
	<td>Pods</td>
	<td>k8s_pod_rate_gpu_used_node</td>
	<td>%</td>
 </tr>
 <tr>
	<td>GPU memory usage</td>
	<td>Mib</td>
	<td>Pod GPU memory usage</td>
	<td>Pods</td>
	<td>k8s_pod_gpu_memory_used_bytes</td>
	<td>B</td>
 </tr>
 <tr>
	<td>GPU memory applications</td>
	<td>Mib</td>
	<td>Pod GPU memory applications</td>
	<td>Pods</td>
	<td>k8s_pod_gpu_memory_request_bytes</td>
	<td>B</td>
 </tr>
 <tr>
	<td>GPU memory utilization<br>(% of request)</td>
	<td>%</td>
	<td>Percentage of GPU memory usage to the request value</td>
	<td>Pods</td>
	<td>k8s_pod_rate_gpu_memory_used_request</td>
	<td>%</td>
 </tr>
 <tr>
	<td>GPU memory utilization<br>(% of node)</td>
	<td>%</td>
	<td>Percentage of node taken up by GPU memory usage</td>
	<td>Pods</td>
	<td>k8s_pod_rate_gpu_memory_used_node</td>
	<td>%</td>
 </tr>
</table>


## Creating and Editing HPAs with YAML Files  
You can create and edit HPAs with YAML files. The following example shows how to configure the file. This file defines an HPA named “test” which will be triggered when the CPU usage reaches 1 with the number of Pods ranging from 1 to 2.  
```
{
    "kind":"HorizontalPodAutoscaler",
    "apiVersion":"autoscaling/v2beta1",
    "metadata":{
        "name":"ccc",
        "namespace":"kube-system",
        "labels":{
            "qcloud-app":"ccc"
        }
    },
    "spec":{
        "minReplicas":1,
        "maxReplicas":2,
        "metrics":[
            {
                "type":"Pods",
                "pods":{
                    "metricName":"k8s_pod_cpu_core_used",
                    "targetAverageValue":"1"
                }
            }
        ],
        "scaleTargetRef":{
            "apiVersion":"apps/v1beta2",
            "kind":"Deployment",
            "name":"cbs-provisioner"
        }
    }
}
```
