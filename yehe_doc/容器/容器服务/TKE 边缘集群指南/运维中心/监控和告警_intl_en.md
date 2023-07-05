## Overview
Elastic Kubernetes Service (EKS) collects and displays metrics for clusters, workloads, pods, and containers.

## Prerequisites
An elastic cluster has been created and is in the Running state. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).

## Procedure
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar.
2. On the **Elastic Cluster** page that appears, click the ID of the cluster that you want to manage.
3. On the cluster resource management page, view the metrics and configure alarms for them. For more information, see the following documents:
 - [Viewing Metrics](https://intl.cloud.tencent.com/document/product/457/30689)
 - [Setting Alarms](https://intl.cloud.tencent.com/document/product/457/30690)

## Monitoring and Alarm Metrics
### Monitoring metrics
TKE currently provides monitoring metrics in the following dimensions. All metrics are **average values** of the statistics collected within the statistical period.
>
>- For monitoring metrics for persistent volumes (PVs) used by a workload, see [Block Storage](https://console.cloud.tencent.com/monitor/product/bs) and [Cloud File Storage](https://console.cloud.tencent.com/monitor/product/cfs).
>- For network monitoring metrics for a CLB associated with a Service, see the [Cloud Load Balancer](https://console.cloud.tencent.com/monitor/clb).
- For more information on how to create an alarm policy, see [Creating an Alarm Policy](https://intl.cloud.tencent.com/document/product/248/6215).


### Monitoring metrics for a cluster

| Metric | Unit | Description |
| --------| ---- | -------------- |
| CPU Usage | Core | Total number of CPU cores used by the running pods in the cluster |
| MEM Usage | B | Total amount of memory used by the running pods in the cluster |

### Monitoring metrics for a workload

| Metric | Unit | Description |
| ---------------------------   | ---- | ------------------ |
| Restart of Pods | Times | Total number of times the pods in the workload are restarted |
| CPU Usage | Core | Total number of CPU cores used by the pods in the workload |
| CPU Utilization (% of Pod Specification) | % | Percentage of the CPU cores allocated to the pods in the workload that is used by the pods |
| MEM Usage | B | Total amount of memory used by the running pods in the workload |
| MEM Utilization (% of Pod Specification) | % | Percentage of the memory capacity allocated to the pods in the workload that is used by the pods |

### Monitoring metrics for a pod

| Metric | Unit | Description |
| ---------------------------   | ---- | ------------------ |
| Exception | - | Status of the pod, which can be normal or abnormal |
| CPU Usage | Core | Number of CPU cores used by the pod |
| CPU Utilization (% of Request) | % | Percentage of the total number of CPU cores specified by Request that is used by the pod |
| CPU Utilization (% of Limit) | % | Percentage of the total number of CPU cores specified by Limit that is used by the pod |
| CPU Utilization (% of Pod Specification) | % | Percentage of the CPU cores allocated to the pod that is used by the pod |
| MEM Usage | B | Amount of memory used by the pod, including the cache usage for the pod |
| MEM Utilization (% of Request) | % | Percentage of the total amount of memory specified by Request that is used by the pod |
| MEM Utilization (% of Limit) | % | Percentage of the total amount of memory specified by Limit that is used by the pod |
| MEM Utilization (% of Pod Specification) | % | Percentage of the memory capacity allocated to the pod that is used by the pod |

### Monitoring metrics for a container

| Metric | Unit | Description |
| ---------------------------   | ---- | ------------------ |
| CPU Usage | Core | Number of CPU cores used by the container |
| CPU Utilization (% of Request) | % | Percentage of the total number of CPU cores specified by Request that is used by the container |
| CPU Utilization (% of Limit) | % | Percentage of the total number of CPU cores specified by Limit that is used by the container |
| MEM Usage | B | Amount of memory used by the container, including the cache usage for the container |
| MEM Utilization (% of Request) | % | Percentage of the total amount of memory specified by Request that is used by the container |
| MEM Utilization (% of Limit) | % | Percentage of the total amount of memory specified by Limit that is used by the container |

## Alarm Metrics

TKE currently provides alarm metrics in the following dimensions. All metrics are **average values** of the statistics collected within the statistical period.

### Alarm metrics for a pod

| Metric | Unit | Description |
| ---------------------------   | ---- | ------------------ |
| CPU Utilization (% of Pod Specification) | % | Percentage of the CPU cores allocated to the pod that is used by the pod |
| MEM Utilization (% of Pod Specification) | % | Percentage of the memory capacity allocated to the pod that is used by the pod |
| CPU Utilization (% of Request) | % | Percentage of the total number of CPU cores specified by Request that is used by the pod |
| MEM Utilization (% of Request) | % | Percentage of the total amount of memory specified by Request that is used by the pod |
| CPU Utilization (% of Limit) | % | Percentage of the total number of CPU cores specified by Limit that is used by the pod |
| MEM Utilization (% of Limit) | % | Percentage of the total amount of memory specified by Limit that is used by the pod |
| Restart of Pods | Times | Number of times the pod is restarted. |
| Pod Ready | - | Status of the pod. By default, an alarm is generated when the value is False. |
| CPU Usage | Core | Number of CPU cores used by the pod |
| MEM Usage | MB | Amount of memory used by the pod, including the cache usage for the pod |
