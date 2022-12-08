
## Background

Public clouds are leased instead of purchased services with complete technical support and assurance, greatly contributing to business stability, scalability, and convenience. But more work needs to be done to reduce costs and improve efficiency, for example, adapting to application development, architecture design, management and Ops, and reasonable use in the cloud. Resource utilization is improved after IDC cloud migration, but not that much; the average utilization of containerized resources is only 13%, indicating a long and uphill way towards improvement.

This article details:
1. The reason for low **CPU and memory utilization** in Kubernetes clusters
2. TKE productized methods for easily improving resource utilization

## Resource Waste Scenarios

To figure out why utilization is low, let's look at a few cases of resource use:

#### Scenarios 1: Over 50% of reserved resources are wasted
The `Request` field in Kubernetes manages the CPU and memory reservation mechanism, which reserves certain resources in one container from being used by another. For more information, see [Resource Management for Pods and Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/). If `Request` is set to a small value, resources may fail to accommodate the business, especially when the load becomes high. Therefore, users tend to set `Request` to a very high value to ensure the service reliability. However, the business load is not that high most of the time. Taking CPU as an example, the following figure shows the relationship between the resource reservation (request) and actual usage (cpu_usage) of a container in a real-world business scenario:
![](https://main.qcloudimg.com/raw/21f3cdbc2488b2d4761bbc76664b2879.png)
As you can see, resource reservation is way more than the actual usage, and the excessive part cannot be used by other loads. Obviously, setting `Request` to a very high value leads to great waste. In response, you need to set a proper value and limit infinite business requests as needed, so that resources will not be occupied overly by certain businesses. You can refer to `ResourceQuota` and `LimitRange` discussed later. In addition, TKE will launch a smart request recommendation product to help you narrow the gap between `Request` and `Usage`, effectively improving resource utilization while guaranteeing business stability.

#### Scenario 2: Business resource utilization sees an obvious change pattern, and resource waste is serious during off-peak hours, which usually last longer than peak hours
Most businesses see an obvious change pattern in resource utilization. For example, a bus system usually has a high load during the day and a low load at night, and a game often starts to experience a traffic surge on Friday night, which drops on Sunday night.
![](https://main.qcloudimg.com/raw/a470b67939b85e346024a5b854c210ec.png)
As you can see, the same business requests different amounts of resources during different time periods. If `Request` is set to a fixed value, utilization will be low when the load is low. The solution is to dynamically adjust the number of replicas to sustain different loads. For more information, see **HPA, HPC, and CA** discussed later.

#### Scenario 3: Resource utilization differs greatly by business type
Online businesses usually have a high load during the day and require a low latency, so they must be scheduled and run first. In contrast, offline businesses generally have low requirements for the operating time period and latency and can run during off-peak hours of online business loads. In addition, some businesses are computing-intensive and consume a lot of CPU resources, while others are memory-intensive and consume a lot of memory resources.
![](https://main.qcloudimg.com/raw/59f6d72a28b1bc436779836966499db0.png)
As shown above, online/offline hybrid deployment helps dynamically schedule offline and online businesses in different time periods to improve resource utilization. For computing-intensive and memory-intensive businesses, affinity scheduling can be used to find the right node. For detailed directions, see online/offline hybrid deployment and affinity scheduling discussed later.

## Improving Resource Utilization in Kubernetes

TKE has productized a series of tools based on a large number of actual businesses, helping you easily and effectively improve resource utilization. There are two ways: 1. manual resource allocation and limitation based on Kubernetes native capabilities; 2. automatic solution based on business characteristics.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Q4dz737_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221208154512.png)

### 1. Resource allocation and limitation

Imagine that you are a cluster admin and your cluster is shared by four business departments. You need to allow for on-demand use while ensuring stability. In order to improve the overall utilization, you need to limit the maximum amount of resources available for each business and prevent excessive usage by setting default values.

Ideally, `Request` and `Limit` values are set as needed. Here, `Request` is resource occupation, indicating the minimum amount of resources available for a container; `Limit` is resource limit, indicating the maximum amount of resources available for a container. This contributes to healthier container running and higher resource utilization, despite the fact that `Request` and `Limit` are often left unspecified. In the case of cluster sharing by teams/projects, `Request` and `Limit` tend to be set to high values to ensure stability. When you create a load in the TKE console, the following default values will be set for all containers, which are based on actual business analysis and estimation and may deviate from real-world requirements.

|     Resource        | Request | Limit |
| ----------- | ------- | ----- |
| CPU (core)     | 0.25    | 0.5   |
| Memory (MiB) | 256     | 1,024  |

**To fine-tune resource allocation and management, you can set namespace-level `ResourceQuota` and `LimitRange` in TKE.**
<dx-tabs>
::: `ResourceQuota` for resource allocation
If your cluster has four businesses, you can use the namespace and `ResourceQuota` to isolate them and limit resources.
`ResourceQuota` is used to set a quota on resources in a namespace, which is an isolated partition in a Kubernetes cluster. A cluster usually contains multiple namespaces to house different businesses. You can set different `ResourceQuota` values for different namespaces to limit the cluster resource usage by a namespace, thus implementing preallocation and limitation. `ResourceQuota` applies to the following. For more information, see [Resource Quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/).
1. Computing resources: Sum of `Request` and `Limit` values of CPU and memory for all containers.
2. Storage resources: Sum of storage requests of all PVCs.
3. Number of objects: Total number of resource objects such as PVC, Service, ConfigMap, and Deployment.

#### `ResourceQuota` use cases
- Assign different namespaces to different projects/teams/businesses and set the `ResourceQuota` for each namespace for allocation.
- Set an upper limit on the amount of resources available for a namespace to improve cluster stability and prevent excessive preemption and consumption of resources by a single namespace.

#### `ResourceQuota` in TKE 
TKE has productized `ResourceQuota`. You can directly use it in the console to limit the resource usage of a namespace. For detailed directions, see [Namespace](https://intl.cloud.tencent.com/document/product/457/30660).
![](https://qcloudimg.tencent-cloud.cn/raw/71d27d6c118bdfcc766178380329cab9.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c3c7572d3482f0347578b7f170f9f264.png)

:::
::: `LimitRange` for resource limitation
What if `Request` and `Limit` are left unspecified or set to high values? If you are the admin, you may set different default values and ranges for different businesses to limit excessive resource preemption by businesses while facilitating creation.

Unlike `ResourceQuota`, which limits the overall resource usage of a namespace, `LimitRange` applies to a single container in a namespace. It can prevent creating containers that request too many or too few resources in a namespace and address the situation where `Request` and `Limit` are left unspecified. `LimitRange` applies to the following. For more information, see [Limit Ranges](https://kubernetes.io/docs/concepts/policy/limit-range/).
1. Computing resources: Sets the range of CPU and memory usage for all containers.
2. Storage resources: Sets the range of storage that can be requested for all PVCs.
3. Ratio setting: Controls the ratio of `Request` to `Limit` of a resource.
4. Default: Sets default `Request`/`Limit` values for all containers. If no custom values are specified for a container, the default values will apply.

#### `LimitRange` use cases
1. Set the default value for resource usage to prevent it from being left unspecified and prevent important Pods from being drained by [QoS](https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod/).
2. Different businesses generally run in different namespaces and have different levels of resource utilization. Setting `Request` and `Limit` by namespace can improve resource utilization.
3. Limit the maximum and minimum amounts of resources available for a container to prevent it from requesting too many resources while ensuring its normal running.

#### `LimitRange` in TKE
TKE has productized `LimitRange`. You can directly manage it by namespace in the console. For detailed directions, see [Limit Ranges](https://kubernetes.io/docs/concepts/policy/limit-range/).
![](https://qcloudimg.tencent-cloud.cn/raw/778c86b97794d55d2b34fe0ef946d3f8.png)
:::
</dx-tabs>


### 2. Automatic improvement of resource utilization

`ResourceQuota` and `LimitRange` for resource allocation and limitation respectively rely on experience and manual operations, mainly addressing unreasonable resource requests and allocation. This section describes how to improve resource utilization through automated dynamic adjustments from the perspectives of elastic scaling, scheduling, and online/offline hybrid deployment.

#### 2.1 Elastic scaling
<dx-tabs>
::: HPA for elastic scaling by metric
In scenario 2 of resource waste, if your business goes through peak and off-peak hours, a fixed `Request` value is bound to cause resource waste during off-peak hours. In this case, you can consider automatically increasing and decreasing the number of replicas of the business load during peak and off-peak hours respectively to enhance the overall utilization.

Horizontal Pod Autoscaler (HPA) can automatically increase and decrease the number of Pod replicas in Deployment and StatefulSet based on metrics such as CPU and memory utilization to stabilize workloads and achieve truly on-demand usage.

#### HPA use cases
1. Traffic bursts: If traffic surges suddenly, the number of Pods is automatically increased promptly at overload.
2. Automatic scale-in: If traffic becomes light, the number of Pods is automatically decreased to avoid waste at underload.

#### HPA in TKE
TKE supports many metrics for elastic scaling based on the custom metrics API, covering CPU, memory, disk, network, and GPU in most HPA scenarios. For more information on the list, see [HPA Metrics](https://intl.cloud.tencent.com/document/product/457/34025). In complex scenarios such as automatic scaling based on the QPS per replica, the prometheus-adapter can be installed. For detailed directions, see [Using Custom Metrics for Auto Scaling in TKE](https://intl.cloud.tencent.com/document/product/457/38941).
![](https://qcloudimg.tencent-cloud.cn/raw/40373c0c3d81c8c326b2dc4906554841.png)
:::
::: HPC for scheduled scaling
Suppose you are planning 11/11 shopping spree promotions for your business on an e-commerce platform. You may consider using HPA for automatic scaling. However, HPA needs to monitor metrics first before responding, which means it may not be fast enough to scale out to promptly sustain heavy traffic. If you expect a traffic surge, consider adding replicas in advance.
Horizontal Pod Cronscaler (HPC) is a proprietary add-on of TKE designed to control the number of replicas on schedule to scale and trigger the impact of insufficient resources during dynamic scale-outs in advance. Compared with community CronHPA, HPC supports:

1. Combination with HPA: You can enable and disable HPA on schedule to make your business more resilient during peak hours.
2. Exceptional date setting: You can set exceptional dates to reduce manual adjustment of HPC, as business traffic is unlikely to remain regular all the time.
3. Single execution: It makes you more flexible in promotion use cases, as previous CronHPA executions are permanent like CronJob executions.

#### HPC use cases
In the case of gaming services, the number of players skyrockets from Friday night to Sunday night. You can scale out the game server before Friday night and scale it in to the original size after Sunday night to ensure a better experience. If HPA is used, services may suffer because scaling out is not fast enough.

#### HPC in TKE
TKE has productized HPC that uses the crontab syntax format, but you need to install it on the **Add-On Management** page in advance in the following steps:
1. Install
![](https://qcloudimg.tencent-cloud.cn/raw/6339eced5612a77955abe8162794f67a.png)
2. Use
![](https://qcloudimg.tencent-cloud.cn/raw/6339eced5612a77955abe8162794f67a.png)
![](https://qcloudimg.tencent-cloud.cn/raw/134dc01838c70507fe77546c72cae9cd.png)
:::
::: CA for automatic adjustment of the number of nodes
Both HPA and HPC increase and decrease the number of replicas automatically at the business load level to adapt to traffic fluctuations and improve resource utilization. However, at the cluster level, the total amount of resources is fixed, and HPA and HPC only allow for more spare resources. Is there a way to reclaim some resources during idle hours and scale out the cluster during busy hours? Such cluster-level elastic scaling is quite cost-efficient, as the overall resource usage of a cluster determines the bill.

Cluster Autoscaler (CA) automatically adjusts the number of cluster nodes to truly improve resource utilization and save costs. It is the key to cost reduction and efficiency improvement.

#### CA use cases
1. Add nodes based on the surge in the business load during peak hours.
2. Release redundant nodes based on resource availability during off-peak hours.

#### CA in TKE
CA in TKE is provided in the form of node pools. We recommend you use CA together with HPA, as the former performs resource-layer (node-layer) scaling, while the latter application-layer scaling. When the overall resources are insufficient after an HPA scale-out, Pods will be pending, and CA will expand the node pool to increase the overall resource volume in the cluster.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nQtK669_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221208161028.png)
For more information on parameter configuration methods and use cases, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).
:::
</dx-tabs>


#### 2.2 Scheduling
The Kubernetes scheduling mechanism is a native resource allocation mechanism which is efficient and graceful. Its core feature is to find the right node for each Pod. In TKE scenarios, the scheduling mechanism contributes to the transition from application-layer to resource-layer elastic scaling. A reasonable scheduling policy can be configured based on business characteristics by properly leveraging Kubernetes scheduling capabilities to effectively enhance resource utilization in clusters.
<dx-tabs>
::: Node affinity
If one of your CPU-intensive businesses is scheduled to a memory-intensive node through the Kubernetes scheduler by accident, all the CPU of the node will be taken up, but its memory will be barely used, resulting in serious waste. In this case, you can label such node as CPU-intensive and label a business load during creation to indicate that it needs to run on a CPU-intensive node. The Kubernetes scheduler will then schedule the load to a CPU-intensive node. This way of finding the right node helps effectively improve resource utilization.

When creating Pods, you can set node affinity to specify nodes to which Pods will be scheduled (these nodes are specified with Kubernetes labels).

#### Node affinity use cases
Node affinity is ideal for scenarios where workloads with different resource requirements run simultaneously in a cluster. For example, CVM nodes can be CPU-intensive or memory-intensive. If certain businesses require much higher CPU usage than memory usage, using general CVM instances will inevitably cause a huge waste of memory. In this case, you can add a batch of CPU-intensive CVM instances to the cluster and schedule CPU-intensive Pods to them, so as to improve the overall utilization. Similarly, you can manage heterogeneous nodes (such as GPU instances) in the cluster, specify the amount of GPU resources needed in the workloads, and have the scheduling mechanism find the right nodes to run these workloads.

#### Node affinity in TKE
TKE provides an identical method to use node affinity as native Kubernetes. You can use this feature in the console or by configuring a YAML file. For detailed directions, see [Proper Resource Allocation](https://intl.cloud.tencent.com/document/product/457/37010).

:::
::: Dynamic Scheduler
The native Kubernetes scheduling policy, such as the default `LeastRequestedPriority`, tends to schedule Pods to nodes with more resources remaining. However, this kind of resource allocation is static, and `Request` does not indicate the actual usage, leading to a certain level of waste. If the scheduler can schedule resources based on the actual resource utilization of nodes, it will avoid resource waste to some extent.

The proprietary Dynamic Scheduler of TKE is a solution, which works as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4MMW770_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221208162651.png)

#### Dynamic Scheduler use cases
In addition to reducing resource waste, the dynamic scheduler can well mitigate scheduling hotspots in a cluster.
1. The Dynamic Scheduler counts the number of Pods scheduled to a node over time to avoid scheduling too many Pods to the same node.
2. The Dynamic Scheduler supports setting a load threshold for a node to filter out nodes that exceed the threshold during scheduling.

#### Dynamic Scheduler in TKE
You can install and use the Dynamic Scheduler in an extended add-on:
![](https://qcloudimg.tencent-cloud.cn/raw/35a2224ade0aeec26492ccc91630ac54.png)
For more information on the Dynamic Scheduler guide, see [DynamicScheduler](https://intl.cloud.tencent.com/document/product/457/39119).
:::
</dx-tabs>



#### 2.3 Online/Offline hybrid business deployment

If you have both online web businesses and offline computing businesses, you can use TKE's online/offline hybrid deployment technology to dynamically schedule and run businesses to improve resource utilization.

In the traditional architecture, big data and online businesses are independent and deployed in different resource clusters. Generally, big data businesses are for offline computing and experience peak hours during nights, during which online businesses are barely loaded. Leveraging complete isolation capabilities of containers (involving CPU, memory, disk I/O, and network I/O) and strong orchestration and scheduling capabilities of Kubernetes, cloud-native technologies implement the hybrid deployment of online and offline businesses to fully utilize resources during idle hours of online businesses.

#### Use cases of online/offline hybrid deployment
In the Hadoop architecture, offline and online jobs are in different clusters. Online and streaming jobs experience obvious load fluctuations, which means a lot of resources will be idle during off-peak hours, leading to great waste and higher costs. In clusters with online/offline hybrid deployment, offline tasks are dynamically scheduled to online clusters during off-peak hours, significantly improving resource utilization. Currently, Hadoop YARN can only statically allocate resources based on the static resource status reported by `NodeManager`, making it unable to well support hybrid deployment.

#### Online/Offline hybrid deployment in TKE 
Online businesses experience obvious and regular load fluctuations, with a low resource utilization at night. In this case, the big data management platform delivers resource creation requests to Kubernetes clusters to increase the computing power of the big data application.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/JGI4705_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221208163653.png) 

## How to Balance Resource Utilization and Stability
Besides costs, system stability is another metric that weighs heavily in enterprise Ops. It's challenging to balance the two. On the one hand, the higher the resource utilization, the better for cost reduction; on the other hand, a too high resource utilization may cause overload and thereby OOM errors or CPU jitters.
To help enterprises get rid of the dilemma, TKE provides the **DeScheduler** to keep the cluster load under control. It is responsible for protecting nodes with risky loads and gracefully draining businesses from them. The relationship between the DeScheduler and the Dynamic Scheduler is as shown below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WF5a355_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221208165538.png)

### DeScheduler in TKE
You can install and use the DeScheduler in an extended add-on. For detailed directions, see [DeScheduler](https://intl.cloud.tencent.com/document/product/457/39146).
![](https://qcloudimg.tencent-cloud.cn/raw/62a9bd573eb7fd0795b53e301efc3c2f.png)

