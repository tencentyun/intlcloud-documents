## Monitoring

TKE currently provides monitoring metrics of the following dimensions. All metrics are **average values** within the granularity.

### Monitoring Metrics for Clusters

|Monitoring Metric|Unit|Description|
| --------| ---- | -------------- |
|CPU Utilization|%|CPU utilization rate of entire cluster|
|MEM Utilization|%|Memory utilization rate of entire cluster|

### Monitoring Metrics for Master & Etcd and Ordinary Nodes

|Monitoring Metric|Unit|Description|
| ---------------------------   | ---- | ------------------ |
| Re-startup of Pods|restarts|Sum of the number of restarts of all pods on the node|
| Exception  |  -  | Node status: normal or exceptional      |
| CPU Utilization     | %  | CPU usage of all pods on the node to the total CPU of the node   |
| MEM Utilization     | %  | Memory usage of all pods on the node to the total memory of the node    |
| Private bandwidth in     | bps  | Total private network inbound bandwidth of all pods on the node    |
| Private bandwidth out     | bps  | Total for private network outbound bandwidth of all pods on the node   |
| Public bandwidth in     | bps  | Total public network inbound bandwidth of all pods on the node    |
| Public bandwidth out     | bps  | Total public network outbound bandwidth of all pods on the node    |
| TCP Connections Count     | connections  | Number of TCP connections maintained on the node   |

For more information on monitoring metrics for cluster nodes, please see [Get Monitoring Statistics](http://intl.cloud.tencent.com/document/product/213/5178).

For more information on monitoring metrics for cluster node data disks, please see [Monitoring Cloud Disks](http://intl.cloud.tencent.com/document/product/362/6742).


### Monitoring Metrics for Workloads

|Monitoring Metric                |Unit   |Description                 |
| ---------------------------   | ---- | ------------------ |
| Re-startup of Pods    | restarts    | Total for the number of restarts of all pods in the workload   |
| CPU Usage  | cores   | CPU usage of all pods in the workload      |
| CPU Utilization (% cluster) | %  |  CPU usage of all pods in the workload to the total CPU of the cluster |
| MEM Usage  | B   | Memory usage of all pods in the workload      |
| MEM Utilization (% cluster) | %  | Memory usage of all pods in the workload to the total memory of the cluster  |
| Network Inbound Bandwidth     | bps  | Total inbound bandwidth of all pods in the workload    |
| Network Outbound Bandwidth     | bps  | Total for outbound bandwidth of all pods in the workload    |
| Network Inbound Traffic    | B  | Total inbound traffic of all pods in the workload  |
| Network Traffic Out     | B  |Total outbound traffic of all pods in the workload     |
| Network Inbound Traffic     | packets/sec  | Total inbound packets of all pods in the workload    |
| Network Outbound Traffic     | packets/sec  | Total outbound packets of all pods in the workload    |

If the workload provides services outside the cluster, please see [Obtaining Monitoring Data](http://intl.cloud.tencent.com/document/product/214/8885) for more information on network monitoring metrics for bound services.


### Monitoring Metrics for Pods

|Monitoring Metric                |Unit   |Description                 |
| ---------------------------   | ---- | ------------------ |
| Exception  |  -  | Pod status: normal or exceptional       |
| CPU Usage  | cores   | CPU usage of the pod      |
| CPU Utilization (% node) | %  | CPU usage of the pod to the total CPU of the node|
| CPU Utilization (% Request) | %  | CPU usage of the pod to the Request valude|
| CPU Utilization (% of Limit) | %  | CPU usage of the pod to the Limit value |
| MEM Usage  | B   | Memory usage of the pod, including cache  |
| MEM Usage (exclude cache)  | B   | Actual memory usage (not including cache) of all containers in the pod |
| MEM Utilization (% node) | %  | Memory usage of the pod to the total memory of the node  |
| MEM Utilization (% node, exclude cache) | %  | Actual memory usage (not including cache) of all containers in the pod to the total memory of the node|
| MEM Utilization (% Request) | %  | Memory usage of the pod to the Request value|
| MEM Utilization (% Request, exclude cache) | %  | Actual memory usage (not including cache) of all containers in the pod to the Request value|
| MEM Utilization (% of Limit) | %  | Memory usage of the pod to the Limit value|
| MEM Utilization (% limit, exclude cache) | %  | Actual memory usage (not including cache) of all containers in the pod to the Limit value|
| Network Inbound Bandwidth | bps | Total inbound bandwidth of the pod|
| Network Outbound Bandwidth | bps | Total outbound bandwidth of the pod |
| Network Inbound Traffic | B | Total inbound traffic of the pod |
| Network Traffic Out | B | Total outbound traffic of the pod |
| Network Inbound Traffic | packets/sec | Total inbound packets of the pod |
| Network Outbound Traffic | packets/sec | Total outbound packets of the pod |

### Monitoring Metrics for Containers

|Monitoring Metric                |Unit   |Description                 |
| ---------------------------   | ---- | ------------------ |
| CPU Usage  | cores   | CPU usage of container      |
| CPU Utilization (% node) | %  | CPU usage of the container to the total CPU of the node  |
| CPU Utilization (% Request) | %  | CPU usage of the container to the Request value  |
| CPU Utilization (% Limit) | %  | CPU usage of the container to the Limit value|
| MEM Usage  | B   | Memory usage of the container, including cache   |
| MEM Usage (exclude cache)  | B   | Actual memory usage of the container (not including cache)    |
| MEM Utilization (% node) | %  | Memory usage of the container to the total memory of the node |
| MEM Utilization (% node, exclude cache) | %  | Actual memory usage (not including cache) of the container to the total memory of the node|
| MEM Utilization (% request) | %  | Memory usage of the container to the Request value  |
| MEM Utilization (% Request, excl. cache) | %  | Actual memory usage (not including cache) of the container to the Request value|
| MEM Utilization (% of Limit)  | %  | Memory usage of the container to the Limit value  |
| MEM Utilization (% limit, exclude cache) | %  | Actual memory usage (not including cache) of the container to the Limit value  |
| Block device read bandwidth    | B/sec  | Throughput of the container to read data from disk   |
| Block device write bandwidth     | B/sec  | Throughput of the container to write data to disk     |
| Read IOPS of Block Device     | operations/sec  | Number of times the container read from disk  |
| Write IOPS of Block Device    | operations/sec  | Number of times the container wrote to disk    |

## Alarms

TKE currently provides alarm metrics of the following dimensions. All metrics are **average values** within the statistical period.

### Alarm Metrics for Clusters

|Monitoring Metric  |Unit   |Description  |
| --------| ---- | -------------- |
| CPU Utilization | %    | CPU utilization rate of entire cluster |
| MEM Utilization | %    | Memory utilization rate of entire cluster  |
| CPU Allocation | %    | Ratio of the sum of the set CPU Requests from all containers in the cluster to the cluster’s total allocable CPU resources |
| MEM Allocation | %    | Ratio of the sum of the set Requests from all containers in the cluster to the cluster’s total allocable memory resources |
| Apiserver Normal | - | Apiserver status. By default, alarms when status value is `False`. Only self-deployed clusters support this metric. |
| Etcd Normal | - | Etcd status. By default, alarms when status value is `False`. Only self-deployed clusters support this metric.  |
| Scheduler Normal | - | Scheduler status. By default, alarms when status value is `False`. Only self-deployed clusters support this metric.  |
| Control Manager Normal | - | Control Manager status. By default, alarms when status value is `False`. Only self-deployed clusters support this metric. |

### Alarm Metrics for Nodes

|Monitoring Metric  |Unit   |Description  |
| --------| ---- | -------------- |
| CPU Utilization     | %  | CPU usage of all pods on the node to the total CPU of the node    |
| MEM Utilization     | %  | Memory usage of all pods on the node to the total memory of the node    |
| Re-startup of Pods on This Node     | Times  | Total number of restarts of all pods on the node  |
| Node Ready     | -  | Node status. By default, alarms when status value is `False`.   |

For more information on alarm metrics for cluster nodes, please see [Get Monitoring Statistics](http://intl.cloud.tencent.com/document/product/213/5178) and [Create Alarm](https://intl.cloud.tencent.com/document/product/248/38908).

For more information on alarm metrics for cluster node data disks, please see [Monitoring Cloud Disks](http://intl.cloud.tencent.com/document/product/362/6742) and [Create Alarm](https://intl.cloud.tencent.com/document/product/248/38908).


### Alarm Metrics for Pods

|Monitoring Metric                |Unit   |Description                 |
| ---------------------------   | ---- | ------------------ |
| CPU Utilization (% node) | %  | CPU usage of the pod to the total CPU of the node l  |
| MEM Utilization (% node) | %  | Memory usage of the pod to the total memory of the node  |
| Actual MEM Utilization (% node, exclude cache) | %  | Actual memory usage (exclude cache) of all containers in the pod to the total memory of the node|
| CPU Utilization (% limit)  | %  | CPU usage of the pod to the Limit value |
| MEM Utilization (% of Limit) | %  | Memory usage of the pod to the Limit value|
| Actual MEM Utilization (% of Limit, exclude cache) | %  | Actual memory usage of the pod (exclude cache) to the Limit value  |
| Re-startup of Pods    | restarts    | Number of pod restarts  |
| Pod Ready  | -   | Pod status. By default, alarms when status value is `False`.   |
| CPU Usage  | cores   | CPU usage of the pod      |
| MEM Usage  | MB   | Memory usage of the pod, including cache    |
| Actual MEM Usage (exclude cache)  | MB   | Actual memory usage of all containers in the pod, excluding cache    |
