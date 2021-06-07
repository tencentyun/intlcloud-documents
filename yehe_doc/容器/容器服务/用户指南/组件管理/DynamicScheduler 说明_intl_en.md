
## Overview
### Add-on description

Dynamic Scheduler is an add-on provided by TKE for pre-selection and preferential selection based on actual node loads. It is implemented based on the native Kube-scheduler Extender mechanism of Kubernetes. After you install it in a TKE cluster, this add-on will work with Kube-scheduler to effectively prevent node load imbalances caused by the native scheduler through the request and limit scheduling mechanisms.
This add-on relies on the Prometheus monitoring component and configuration of relevant rules. Before installing this add-on, we recommend you carefully read [Dependency Deployment](#Dynamic) to prevent problems with the add-on.



### Kubernetes objects deployed in a cluster


| Kubernetes Object Name | Type | Requested Resources | Namespace |
| :----------------------- | :----------------- | :------------------------------------------| ------------- |
| node-annotator | Deployment | Each instance: CPU: 100m,  Memory: 100Mi, a total of 1 instance | kube-system |
| dynamic-scheduler | Deployment | Each instance: CPU: 400m, Memory: 200Mi, a total of 3 instances | kube-system |
| dynamic-scheduler        | Service            |                      -                       | kube-system   |
| node-annotator           | ClusterRole        |                      -                       | kube-system   |
| node-annotator           | ClusterRoleBinding |                      -                       | kube-system   |
| node-annotator           | ServiceAccount     |                      -                       | kube-system   |
| dynamic-scheduler-policy | ConfigMap          |                      -                       | kube-system   |
| restart-kube-scheduler   | ConfigMap          |                      -                       | kube-system   |
| probe-prometheus         | ConfigMap          |                      -                       | kube-system   |



## Use Cases

### Cluster load imbalance

In most cases, the Kubernetes native scheduler performs scheduling based on the pod request resources, without considering the actual load of nodes at the current time and over a previous period. Consequently, the following problem may occur:
In some nodes of the cluster, the amount of remaining schedulable resources (calculated based on the request and limit of the pods running on nodes) may be large but the actual load is high. In contrast, in other nodes, the amount of remaining schedulable resources may be low but the actual load is low. In some cases like this, Kube-scheduler preferentially schedules pods to nodes with more remaining resources (according to the LeastRequestedPriority policy).

As shown in the figure below, Kube-Scheduler will schedule pods to Node2, when it is clear that scheduling pods to Node1 (with a lower load level) is a better choice.
<img src="https://main.qcloudimg.com/raw/518239f56c2f4c805dc5678e79443466.png" data-nonescope="true">

### Scheduling hotspot-prevention policy

To prevent large numbers of pods from being continuously scheduled to low-load nodes, Dynamic Scheduler sets the scheduling hotspot-prevention policy, which calculates the number of pods scheduled to each node within the past few minutes and deducts points from the preferential selection scores of nodes accordingly.
The current policy is as follows:
- If more than 2 pods have been scheduled to a node in the last minute, 1 point is deducted from the preferential selection score of the node.
- If more than 5 pods have been scheduled to a node in the last 5 minutes, 1 point is deducted from the preferential selection score of the node.


## Risk Control

- This add-on is interconnected with the TKE monitoring alarm system.
- We recommend that you enable event persistence for your cluster to better monitor add-on exceptions and locate faults.
- After the addon is uninstalled, only the scheduling logic of the dynamic scheduler will be deleted. The scheduling feature of the native Kube-Scheduler will not be impacted.

## Limits

- It is recommended to use a TKE version of v1.10.x or later.
- If you need to upgrade the Kubernetes master version:
	- For managed clusters, you do not need to set Dynamic Scheduler again.
	- For self-deployed clusters, you need to remove Dynamic Scheduler and then reinstall it because the master version upgrade will reset all component configurations on the master, affecting the configuration of Dynamic Scheduler as Scheduler Extender.




## How It Works

Based on the scheduler extender mechanism, Dynamic Scheduler obtains node load data from the Prometheus monitoring data, develops scheduling policies based on the actual load of nodes, and intervenes during pre-selection and preferential selection to preferentially schedule pods to low-load nodes. This add-on consists of node-annotator and dynamic-scheduler.

### node-annotator

node-annotator regularly pulls node load metrics from monitoring data and synchronizes them to the node annotation, as shown in the figure below:
>! After the addon is deleted, the annotation generated by the node-annotator will not be automatically deleted. You can manually delete it as needed.

![](https://main.qcloudimg.com/raw/1a5ede9cc77fbb797e68f645e908bb33.png)

### Dynamic-scheduler

Dynamic-scheduler is a scheduler-extender that performs filtering and score calculation based on the load data in the node annotation during pre-selection and preferential selection of nodes.

#### Pre-selection policy

To prevent pods from being scheduled to high-load nodes, you need to filter out some high-load nodes through pre-selection (the filtering policy and proportion can be dynamically configured; for more information, see [Add-on Parameter Description](#parameter)).
As shown in the figure below, the load of Node2 in the past 5 minutes and the load of Node3 in the past hour both exceed the corresponding thresholds, so both nodes will be excluded from subsequent preferential selection.
![](https://main.qcloudimg.com/raw/170eca75a5d9b241a8cb501fb3c23071.png)

#### Preferential selection policy

At the same time, to balance the loads among nodes, Dynamic-Scheduler scores each node based on its load data. The lower the load, the higher the score.
As shown in the figure below, the score of Node1 is the highest, so pods will be preferentially scheduled to Node1 (the scoring policy and weights can be dynamically configured; for more information, see [Add-on Parameter Description](#parameter)).
![](https://main.qcloudimg.com/raw/a080287111f91ff1cf18ce85bb08cd13.png)

## Add-on Parameter Description

### Prometheus data query address


>!
>- To ensure that the add-on can pull the required monitoring data and the scheduling policy can take effect, please configure the rules for collecting monitoring data in accordance with **[Dependency Deployment](#Dynamic)** -> **[Prometheus rule configuration](#Prometheus1)**.
>- We have set the pre-selection parameters and preferential selection parameters to the default values. You do not have to modify them unless you have additional requirements.


- If you use a self-built PROM instance, directly enter the data query URL (http/https).
- If you use a managed PROM instance, select the managed instance ID, and we will automatically resolve it into the corresponding data query URL.



### Pre-selection parameters

| Default Value | Description |
| ----------------------------- | ------------------------------------------------------------ |
| Threshold for average **CPU** utilization in the past 5 minutes | If the **average** CPU utilization of a node in the past 5 minutes exceeds the specified threshold, pods will not be scheduled to this node. |
| Threshold for max **CPU** utilization in the past hour | If the **max** CPU utilization of a node in the past hour exceeds the specified threshold, pods will not be scheduled to this node. |
| Threshold for average **memory** utilization in the past 5 minutes | If the **average** memory utilization of a node in the past 5 minutes exceeds the specified threshold, pods will not be scheduled to this node. |
| Threshold for max **memory** utilization in the past hour | If the **max** memory utilization of a node for in past hour exceeds the specified threshold, pods will not be scheduled to this node. |


### Preferential selection parameters

| Default Value | Description |
| --------------------------- | ------------------------------------------------------------ |
| Weight of average **CPU** utilization in the past 5 minutes | The greater the weight, the greater influence the **average** CPU utilization of the node in the past 5 minutes will have on the node score. |
| Weight of max **CPU** utilization in the past hour | The greater the weight, the greater influence the **max** CPU utilization of the node in the past hour will have on the node score. |
| Weight of max **CPU** utilization in the past day | The greater the weight, the greater influence the **max** CPU utilization of the node in the past day will have on the node score. |
| Weight of average **memory** utilization in the past 5 minutes | The greater the weight, the greater influence the **average** memory utilization of the node in the past 5 minutes will have on the node score. |
| Weight of max **memory** utilization in the past hour | The greater the weight, the greater influence the **max** memory utilization of the node in the past hour will have on the node score. |
| Weight of max **memory** utilization in the past day | The greater the weight, the greater influence the **max** memory utilization of the node in the past day will have on the node score. |






## Directions
### Dependency Deployment

Dynamic Scheduler makes scheduling decisions based on the actual load of nodes at the current time and over a previous period. This requires monitoring components, such as Prometheus, to obtain the actual load information of nodes. Before using Dynamic Scheduler, you need to deploy monitoring components such as Prometheus. In TKE, users can use the self-built Prometheus monitoring service or use the cloud native monitoring provided by TKE.

[](id:rules)
<dx-tabs>
::: Self-built\sPrometheus\smonitoring\sservices
#### Deploying node-exporter and prometheus

We use node-exporter to monitor node metrics. You can deploy node-exporter and prometheus based on your own requirements.


#### Aggregation rule configuration

After node-exporter obtains node monitoring data, Prometheus must aggregate the data collected in the native node-exporter. To obtain metrics required by Dynamic Scheduler, such as `cpu_usage_avg_5m`, `cpu_usage_max_avg_1h`, `cpu_usage_max_avg_1d`, `mem_usage_avg_5m`, `mem_usage_max_avg_1h`, and `mem_usage_max_avg_1d`, you need to configure rules in Prometheus as follows:

``` yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
    name: example-record
spec:
    groups:
      - name: cpu_mem_usage_active
        interval: 30s
        rules:
        - record: cpu_usage_active
         expr: 100 - (avg by (instance) (irate(node_cpu_seconds_total{mode="idle"}[30s])) * 100)
        - record: mem_usage_active
          expr: 100*(1-node_memory_MemAvailable_bytes/node_memory_MemTotal_bytes)
      - name: cpu-usage-5m
        interval: 5m
        rules:
        - record: cpu_usage_max_avg_1h
          expr: max_over_time(cpu_usage_avg_5m[1h])
        - record: cpu_usage_max_avg_1d
          expr: max_over_time(cpu_usage_avg_5m[1d])
      - name: cpu-usage-1m
        interval: 1m
        rules:
        - record: cpu_usage_avg_5m
          expr: avg_over_time(cpu_usage_active[5m])
      - name: mem-usage-5m
        interval: 5m
        rules:
        - record: mem_usage_max_avg_1h
          expr: max_over_time(mem_usage_avg_5m[1h])
        - record: mem_usage_max_avg_1d
          expr: max_over_time(mem_usage_avg_5m[1d])
      - name: mem-usage-1m
        interval: 1m
        rules:
        - record: mem_usage_avg_5m
          expr: avg_over_time(mem_usage_active[5m])
```

#### Prometheus file configuration

1. After defining the rules for the calculation of metrics needed by Dynamic Scheduler, you need to set the rules for Prometheus. You can refer to a common Prometheus configuration file, The example is shown as follows:

```
global:
      evaluation_interval: 30s
      scrape_interval: 30s
      external_labels:
rule_files:
- /etc/prometheus/rules/*.yml # /etc/prometheus/rules/*.yml is the file that defines the rules.
```
2. Copy the configuration of rules to a file (such as dynamic-scheduler.yaml), place the file under `/etc/prometheus/rules/` of the above Prometheus container.
3. Reload Prometheus server to obtain the metrics needed by Dynamic Scheduler from Prometheus.

<blockquote class="doc-tip"><p class="doc-tip-tit"><i class ="doc-icon-tip"></i>Note</p><p>Normally, the above Prometheus configuration file and rules configuration file are stored via configmap and then mounted to the Prometheus server container. Therefore, you only need to modify the relevant configmap.</a></p></blockquote>

:::
::: Cloud\snative\smonitoring\svia\sPrometheus
1. Log in to the TKE console and click **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** in the left sidebar to go to the **Cloud Native Monitoring** page.
2. Create a cloud native monitoring RPOM instance under the same VPC as the target cluster, and associate it with the user cluster.
3. After associating the instance with a native managed cluster, go to the user cluster to check that node-exporter has been installed on each node.
4. Set the Prometheus aggregation rules. The rule content is the same as the aggregation rules configured in [Self-built Prometheus monitoring services](#rules).

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
    name: example-record
spec:
    groups:
      - name: cpu_mem_usage_active
        interval: 30s
        rules:
        - record: cpu_usage_active
         expr: 100 - (avg by (instance) (irate(node_cpu_seconds_total{mode="idle"}[30s])) * 100)
        - record: mem_usage_active
          expr: 100*(1-node_memory_MemAvailable_bytes/node_memory_MemTotal_bytes)
      - name: cpu-usage-5m
        interval: 5m
        rules:
        - record: cpu_usage_max_avg_1h
          expr: max_over_time(cpu_usage_avg_5m[1h])
        - record: cpu_usage_max_avg_1d
          expr: max_over_time(cpu_usage_avg_5m[1d])
      - name: cpu-usage-1m
        interval: 1m
        rules:
        - record: cpu_usage_avg_5m
          expr: avg_over_time(cpu_usage_active[5m])
      - name: mem-usage-5m
        interval: 5m
        rules:
        - record: mem_usage_max_avg_1h
          expr: max_over_time(mem_usage_avg_5m[1h])
        - record: mem_usage_max_avg_1d
          expr: max_over_time(mem_usage_avg_5m[1d])
      - name: mem-usage-1m
        interval: 1m
        rules:
        - record: mem_usage_avg_5m
          expr: avg_over_time(mem_usage_active[5m])
```
:::
</dx-tabs>




### Installing the add-on



1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster) and click **Cluster** in the left sidebar.
2. On the “**Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. Click **Create** above the **Add-on List** and select **DynamicScheduler** in the **Create Add-on** page.
5. Click **Parameter Configurations** and set the parameters according to [Add-on Parameter Description](#parameter).
6. Click **Done**. After the add-on is installed successfully, Dynamic Scheduler can run normally, without the need for extra configuration.

