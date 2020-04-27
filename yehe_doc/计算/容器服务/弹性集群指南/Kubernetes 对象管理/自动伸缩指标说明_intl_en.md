Horizontal Pod Autoscaler (HPA) can automatically scale the number of Pods for services according to the average CPU utilization of target Pods and other metrics. You can set auto-scaling triggering metrics in the console. Such metrics include CPU, memory, disk, network, and GPU metrics. You can also use these metrics when creating and editing HPAs with YAML files. This document provides an example of configuring a YAML file.

## Autoscaling Metrics
The following tables provide details about some autoscaling metrics:
>Each variable in the `metricName` column has its own unit listed in the Unit column. You can omit such units when compiling the YAML file.

### CPU metrics

<table>
<tr>
	<th width="17.8%">Metric Name in the Console</th><th width="14.1%">Unit in the Console</th><th width="17.1%">Description</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default Unit</th>
	</tr>
	<tr>
	<td>CPU Usage</td>
	<td>Core</td>
	<td>Number of CPU cores used by the pod</td>
	<td>Pods</td>
	<td>k8s_pod_cpu_core_used</td>
	<td>Core</td>
	</tr>
	<tr>
	<td>CPU Usage <br>(% of Pod)</td>
	<td>%</td>
	<td>Percentage of the CPU cores allocated to the pod that is used by the pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_resource</td>
	<td>%</td>
	</tr>
	<tr>
	<td>CPU Utilization <br>(% of Request)</td>
	<td>%</td>
	<td>Percentage of the total number of CPU cores specified by Request that is used by the pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>CPU Utilization <br>(% of Limit)</td>
	<td>%</td>
	<td>Percentage of the total number of CPU cores specified by Limit that is used by the pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_cpu_core_used_limit</td>
	<td>%</td>
	</tr>
</table>

### Memory metrics

<table>
<tr>
	<th width="17.8%">Metric Name in the Console</th><th width="14.1%">Unit in the Console</th><th width="17.1%">Description</th>
	<th width="6.6%">type</th><th width="33%">metricName</th><th width="11.4%">Default Unit</th>
	</tr>
	<tr>
	<td>MEM Usage</td>
	<td>Mib</td>
	<td>Amount of memory used by the pod</td>
	<td>Pods</td>
	<td>k8s_pod_mem_usage_bytes</td>
	<td>B</td>
	</tr>
	<tr>
	<td>MEM Utilization <br>(% of Pod Specification)</td>
	<td>%</td>
	<td>Percentage of the memory capacity allocated to the pod that is used by the pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_bytes_resource</td>
	<td>%</td>
	</tr>
	<tr>
	<td>MEM Utilization <br>(% of Request)</td>
	<td>%</td>
	<td>Percentage of the total amount of memory specified by Request that is used by the pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_request</td>
	<td>%</td>
	</tr>
	<tr>
	<td>MEM Utilization <br>(% of Limit)</td>
	<td>%</td>
	<td>Percentage of the total amount of memory specified by Limit that is used by the pod</td>
	<td>Pods</td>
	<td>k8s_pod_rate_mem_usage_limit</td>
	<td>%</td>
	</tr>
</table>







## Creating and Editing an HPA by Using a YAML File 
You can create and edit an HPA by using a YAML file. The following example shows a configuration file that defines an HPA named "test". The HPA enables the system to trigger HPA for 1 or 2 pods when the CPU usage reaches 1.
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
