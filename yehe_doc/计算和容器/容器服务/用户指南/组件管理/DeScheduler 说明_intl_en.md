## Introduction
### Add-on description

DeScheduler is a plug-in provided by TKE based on the [DeScheduler](https://github.com/kubernetes-sigs/descheduler) Kubernetes native community in order to implement rescheduling based on actual node loads. After it is installed in a TKE cluster, this plug-in will work together with Kube-scheduler to monitor high-load nodes in the cluster in real time and drain low-priority pods. We recommend that you use it together with the TKE [Dynamic Scheduler add-on](https://intl.cloud.tencent.com/document/product/457/39119) to ensure cluster load balancing in multiple dimensions. 
This plug-in relies on the Prometheus monitoring component and relevant rule configurations. We recommend that you read [Dependency Deployment](#Dependency-deployment) carefully before installing this plug-in to prevent plug-in operation failures.



### Kubernetes objects deployed in a cluster

| Kubernetes Object Name | Type | Requested Resources | Namespace |
| :----------------- | :----------------- | :------------------------------------------ | ------------- |
| descheduler | Deployment | Each instance: CPU: 200m, Memory: 200Mi, a total of 1 instance | kube-system |
| descheduler | ClusterRole | - | kube-system |
| descheduler | ClusterRoleBinding | - | kube-system |
| descheduler | ServiceAccount | - | kube-system |
| descheduler-policy | ConfigMap | - | kube-system |
| probe-prometheus | ConfigMap | - | kube-system |


## Use Cases

DeScheduler performs rescheduling to resolve the improper operations of existing nodes in your cluster. The policy adopted by the community version of DeScheduler is based on the data in the APIServer, instead of actual node loads. Therefore, we can add node monitoring so that rescheduling can be performed based on actual loads.

The self-developed ReduceHighLoadNode policy of TKE relies on the monitoring data of Prometheus and node_exporter to perform pod draining and rescheduling based on metrics such as node CPU utilization, memory utilization, network I/O, and system loadavg. This can prevent extremely high loads on nodes. ReduceHighLoadNode of DeScheduler needs to be used in combination with the load-based scheduling policy of the self-developed Dynamic Scheduler of TKE.



## Limits

- Kubernetes version v1.10.x or later
- In certain scenarios, some pods are rescheduled to nodes that need rescheduling, so the pods will be repeatedly drained. In such cases, based on the actual circumstances, you can change the schedulable nodes of pods or mark pods as exempt from draining. 
- This component is already interconnected with the monitoring and alarm system of TKE.
- We recommend that you enable event persistence for your cluster to better monitor component exceptions and locate faults. When Descheduler drains pods, the corresponding event will be generated. You can check events with "reason" being "Descheduled" to see whether pods are drained repeatedly.
- To prevent DeScheduler from draining key pods, by default, the designed algorithm does not drain pods. For pods that can be drained, you need to indicate the workload to which the pods belong. For example, for objects such as statefulset and deployment, set an annotation to indicate that draining is allowed.
- Draining large numbers of pods will result in service unavailability.
   Native Kubernetes provides the PDB object to prevent the draining API from causing too many pods of a workload to be unavailable. However, you need to manually create this PDB configuration. The self-developed DeScheduler add-on of TKE introduces a safety net measure: before the draining API is called, DeScheduler checks whether the number of pods ready in the workload is larger than the number of replicas. If not, the draining API is not called.





## How It Works

Based on the rescheduling idea of the [community version of DeScheduler](https://github.com/kubernetes-sigs/descheduler), DeScheduler regularly scans the pods running on each node. After discovering any pods that do not comply with its policies, DeScheduler will drain and reschedule them. The community version of DeScheduler has provided some policies based on data in the APIServer. For example, the `LowNodeUtilization` policy relies on the request and limit data of pods. This data can be used to effectively balance cluster resource distribution and prevent resource fragments. However, the community policies lack support for actual node resource occupation. For example, if node A and node B are allocated the same resources, their loads will be different because of differences in CPU consumption, memory consumption, and load in peak periods resulting from the actual running of pods.

Therefore, Tencent Cloud TKE launched DeScheduler, which performs rescheduling based on the monitoring of actual node loads. It obtains the load statistics of cluster nodes from Prometheus, and based on the user-set load threshold, regularly executes the check rule in the policy to drain pods from high-load nodes.
![](https://main.qcloudimg.com/raw/4f515486529dad48e8bbaa3a459e2fb8.png)


## Add-on Parameter Description

### Prometheus data query address


>! To ensure that the add-on can pull the required monitoring data and the scheduling policy can take effect, please configure the monitoring data collection rule in accordance with the directions of **[Dependency Deployment](#Dependency-deployment)** > **Prometheus File Configuration**.

- If you use a self-built Prometheus instance, directly enter the data query URL (HTTPS/HTTPS).
- If you use a managed Prometheus instance, select the managed instance ID, and the system will automatically resolve the ID into the corresponding data query URL.

### Utilization threshold and target utilization

>! Default values have been set for load threshold parameters. If you do not have extra requirements, you can directly use them.

If the average CPU utilization or average memory usage of a node over the past 5 minutes exceeds the set threshold, DeScheduler will regard the node as a high-load node and execute the pod draining logic. It will try to reduce the node load to below the target utilization level through pod rescheduling.



## Directions
### Dependency deployment

The DeScheduler add-on relies on the actual load of nodes at the current moment and over a past period to make scheduling decisions. It requires monitoring components such as Prometheus to obtain actual node load information from the system. Before you use the DeScheduler add-on, we recommend that you adopt self-built Prometheus monitoring or TKE cloud native monitoring.

<span id ="rules"></span>
<dx-tabs>
::: Self-built\sPrometheus\smonitoring\sservice
##### Deploying node-exporter and Prometheus

We use node-exporter to monitor node metrics. You can deploy node-exporter and Prometheus based on your own requirements.

##### Aggregation rule configuration

After node-exporter obtains node monitoring data, Prometheus is required to perform aggregation calculation of the data collected in the native node-exporter. To obtain the metrics required by DeScheduler, such as `cpu_usage_avg_5m` and `mem_usage_avg_5m`, you need to configure rules in Prometheus. See the sample below:

<dx-codeblock>
:::  yaml
```
groups:
   - name: cpu_mem_usage_active
     interval: 30s
     rules:
     - record: mem_usage_active
       expr: 100*(1-node_memory_MemAvailable_bytes/node_memory_MemTotal_bytes)
   - name: cpu-usage-1m
     interval: 1m
     rules:
     - record: cpu_usage_avg_5m
       expr: 100 - (avg by (instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
   - name: mem-usage-1m
     interval: 1m
     rules:
     - record: mem_usage_avg_5m
       expr: avg_over_time(mem_usage_active[5m])
```
:::
</dx-codeblock>

>! When you use the DynamicScheduler provided by TKE, you need to configure the aggregation rules for obtaining node monitoring data in Prometheus. The aggregation rules of the DynamicScheduler partly overlap with those of DeScheduler, but they are not exactly the same. Therefore, mutual overwriting is not allowed during rule configuration. When you use DynamicScheduler and DeScheduler together, configure the following rules:
<dx-codeblock>
:::  yaml
```
groups:
   - name: cpu_mem_usage_active
     interval: 30s
     rules:
     - record: mem_usage_active
       expr: 100*(1-node_memory_MemAvailable_bytes/node_memory_MemTotal_bytes)
   - name: mem-usage-1m
     interval: 1m
     rules:
     - record: mem_usage_avg_5m
       expr: avg_over_time(mem_usage_active[5m])
   - name: mem-usage-5m
     interval: 5m
     rules:
     - record: mem_usage_max_avg_1h
       expr: max_over_time(mem_usage_avg_5m[1h])
     - record: mem_usage_max_avg_1d
       expr: max_over_time(mem_usage_avg_5m[1d])
   - name: cpu-usage-1m
     interval: 1m
     rules:
     - record: cpu_usage_avg_5m
       expr: 100 - (avg by (instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
   - name: cpu-usage-5m
     interval: 5m
     rules:
     - record: cpu_usage_max_avg_1h
       expr: max_over_time(cpu_usage_avg_5m[1h])
     - record: cpu_usage_max_avg_1d
       expr: max_over_time(cpu_usage_avg_5m[1d])
```
:::
</dx-codeblock>

#### Prometheus file configuration
1. The above step defined the rules for metric calculation needed by DeScheduler. Now you need to configure the rules in Prometheus, with reference to a general Prometheus configuration file. See the sample below:
```
global:
   evaluation_interval: 30s
   scrape_interval: 30s
   external_labels:
rule_files:
 - /etc/prometheus/rules/*.yml # /etc/prometheus/rules/*.yml is the file that defines the rules.
```
2. Copy the rules configuration to a file (such as de-scheduler.yaml) and place the file in the `/etc/prometheus/rules/` directory of the above Prometheus container.
3. Reload the Prometheus server to obtain the metrics needed by the Dynamic Scheduler from Prometheus.
>? Normally, the above Prometheus configuration file and rules configuration file are stored via configmap and then mounted to the Prometheus server container. Therefore, you only need to modify the relevant configmap.
:::
:::  Cloud\snative\smonitoring\sPrometheus
1. Log in to the TKE console and click **[Cloud Native Monitoring](https://console.cloud.tencent.com/tke2/prometheus)** in the left sidebar to go to the **Cloud Native Monitoring** page.
2. Create a cloud native monitoring Prometheus instance under the same VPC as the target cluster and associate it with the user cluster, as shown in the figure below:
   ![](https://main.qcloudimg.com/raw/44979847793b5c363e440b9d8d7e29f3.png)
3. After associating the instance with a native managed cluster, go to the user cluster to check that node-exporter has been installed on each node, as shown in the figure below:
   ![](https://main.qcloudimg.com/raw/baef0cd5cd292e4496241a9c8a4463ec.png)
4. Set the Prometheus aggregation rules. The rules are the same as the aggregation rules configured in the above [self-built Prometheus monitoring services](#Self-built-Prometheus-monitoring-service). The rules take effect immediately after being saved, and the server need not be reloaded.
:::
</dx-tabs>



### Installing the add-on

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster) and click **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the "Add-on List" page.
4. Click **Create** on the "Add-on List" page and select **Descheduler** on the "Create Add-on" page.
5. Click **Parameter Configurations** and set the parameters according to [Add-on Parameter Description](#Add-on-Parameter-Description).
6. Click **Done**. After the add-on is installed successfully, DeScheduler can run normally, without the need for extra configuration.
7. If you need to drain workloads (such as statefulset, deployment, and other objects), you can set Annotation as follows:
```plaintext
descheduler.alpha.kubernetes.io/evictable: 'true'
```
