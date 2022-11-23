## Basic Settings
The **Basic Settings** section allows you to set the node quantity range of the automatic scaling feature, configure the elastic resource type, and configure whether to support graceful scale-in for automatic scaling. It also displays the number of elastic node resources in the current cluster and supports quickly releasing elastic instances.
![](https://qcloudimg.tencent-cloud.cn/raw/1109503066a2ed8a0b083ee7e08af0ef.jpg)

- Min Number of Instances: The minimum number of task nodes a cluster can have when the automatic scaling policy is triggered.
- Max Number of Instances: The maximum number of task nodes a cluster can have when the automatic scaling policy is triggered; the accumulated number of task nodes under one or more rules or policies cannot exceed the max number of instances.
![](https://qcloudimg.tencent-cloud.cn/raw/c6118ed39437d42e9095b1ba948f5c59.jpg)
- Release All: Clears all nodes added in an automatic scaling action with one click.
- Release spot instances: Clears all spot instances added in an automatic scaling action with one click.
- Release pay-as-you-go instances: Clears all pay-as-you-go instances added in an automatic scaling action with one click.

- Global Graceful Scale-In: This feature is disabled by default. It applies to all scale-in rules and can be disabled for individual scale-in rules.
- Resource Type: HOST resources are billed on a pay-as-you-go or spot basis, whereas POD resources are billed on a pay-as-you-go basis and can only be used to assume the NodeManager role of YARN.
>! When you switch the resource type, the corresponding scaling specification and instance selection policy will also be switched to take effect.

## Scaling Specification Management
Scaling specifications refer to node specifications for automatic scaling. You can configure each cluster with up to five scaling specifications. When a scale-out rule is triggered, the scaling will be carried out according to the specification priority. When the high-priority specification has fewer resources than the number of resources to be added, the specification of the next priority will be used for supplement. In order to maintain the linear change of the cluster load, we recommend you keep the CPU and memory of the scaling specifications consistent.
- Instance selection policy: Two policies are supported: **Pay-as-you-go** and **Spot instances preferred**.
	- Pay-as-you-go: Only pay-as-you-go instances are added to provide the required computing power when a scaling rule is triggered.
	- Spot instances preferred: Spot instances will be preferred if they are available to provide the required computing power when a scaling rule is triggered.
		- Min proportion of pay-as-you-go instances: The minimum proportion of pay-as-you-go instances to the scale-out quantity.
<dx-alert infotype="explain" title="For example:">
If ten nodes are to be added and this proportion is 20%, at least two pay-as-you-go nodes will be added when a scaling rule is triggered, with the remaining eight being spot nodes. When spot nodes are insufficient, additional pay-as-you-go nodes will be added to make up the difference.
</dx-alert>
- You can add, delete, change, and query the instances in the scaling specifications, and adjust the priority of scaling specifications as needed.
- The sequence of the five specifications for scale-out is as follows (same for pay-as-you-go and spot instances):
	- When the resources are sufficient: 1 > 2 > 3 > 4 > 5
<dx-alert infotype="explain" title="For example:">
If five preset specifications are available **and** the resources are sufficient, when a scale-out rule is triggered to add ten nodes, ten nodes with specification 1 will be added according to the sequence, and other preset specifications will not be selected.
</dx-alert>
	- When the resources are insufficient: 1 + 2 > 1 + 2 + 3 > 1 + 2 + 3 + 4 > 1 + 2 + 3 + 4 + 5
<dx-alert infotype="explain" title="For example:">
If there are eight nodes with specification 1, four nodes with specification 2, and three nodes with specification 3, when a scale-out rule is triggered to add 13 nodes, eight nodes with specification 1, four nodes with specification 2, and one node with specification 3 will be added according to the sequence.
</dx-alert>
	- When a resource specification is out of stock (e.g., specification 2): 1 + 3 > 1 + 3 + 4 > 1 + 3 + 4 + 5
<dx-alert infotype="explain" title="For example:">
1. If there are eight nodes with specification 1, no nodes with specification 2 (out of stock), and three nodes with specification 3, when a scale-out rule is triggered to add ten nodes, eight nodes with specification 1 and two nodes with specification 3 will be added according to the sequence, while specification 2 will not be selected.
2. If there are eight nodes with specification 1 and nodes with other preset specifications are all out of stock, when a scale-out rule is triggered to add ten nodes, eight nodes with specification 1 will be added, and the scale-out will be partially successful.
</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/e718eca7930cf58723482812ba8486cd.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/4bc7f0a738b52bb9a2d679d4aba7c20f.jpg)

## Scaling Rule Management
Scaling rules are business policies used to configure the triggering conditions of scaling actions and the number of nodes to be added or removed. Automatic scaling supports two kinds of policies, load-based scaling and time-based scaling. You can choose to use either of the two kinds of policies, but not both at the same time. When you switch the policies, the original scaling rules will be retained in an invalid state and will not be triggered. Those already added nodes will also be retained unless a scale-in rule is triggered. Each policies can be configured with up to 10 scaling rules. When two rules are triggered at the same time, the rule of the higher priority will be executed first.
![](https://qcloudimg.tencent-cloud.cn/raw/ab392972529b2d7228a8fba4247518e7.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/fa6ab6598e82e83e2b5c88ca03179295.jpg)
To set a scaling rule, select **Load-based scaling** or **Time-based scaling** for **Auto Scaling Type** in the **Scaling Rule Management** module and click **Add Rule**.

### Load-based scaling
When it is impossible to accurately estimate the peak and trough of cluster computing, you can configure the scaling policy based on the load to ensure that important jobs are completed on time. The load is mainly based on the preset YARN metric statistics rules and the task nodes are automatically adjusted when the preset conditions are triggered.
![](https://qcloudimg.tencent-cloud.cn/raw/43b058b725ff2a0072cb3145855ccb3c.jpg)
To add a load-based scaling rule, select **Load-based scaling** as the **Auto Scaling Type**, click **Add Rule**, and configure the following fields:

- Rule Status: Used to mark whether the rule is enabled. The default status of a rule is "enabled". When you don't want a rule to be executed but still wish to retain it, you can set the rule status to "disabled".
- Rule Name: The name of the scaling rule. The scaling rule names in the same cluster must be unique (including scale-out and scale-in rules).
- Valid Time: The load-based scaling rule can be triggered only within the valid time. **Unlimited** is selected by default and you can customize the valid time.
- Scale-out Service: By default, the selected component will inherit the cluster-level configuration and fall into the default configuration group for that node type. You can also set the configuration of the target component through the **Specify configuration** parameter.
- Node Label: This field is empty by default, and the added nodes will be assigned the default label. If you have set a label, resources will be added to the node with this label.
- Load Metric: Set the condition rule for triggering threshold based on the selected cluster load metric. Here refers to the load metric of YARN.

| EMR Automatic Scaling Metric | Description |
|---------|---------|
| AvailableVCores#root	| Number of virtual cores available in the root queue |
| PendingVCores#root	| Number of virtual cores waiting to be available in the root queue |
| AvailableMB#root	| Amount of memory available in the root queue in MB |
| PendingMB#root	| Amount of memory waiting to be available in the root queue in MB |
| AvailableMemPercentage	| Available memory in percentages |
| ContainerPendingRatio	| Ratio of the number of containers to be allocated to the number of allocated containers |
| AppsRunning#root	| Number of running tasks in the root queue |
| AppsPending#root	| Number of pending tasks in the root queue |
| PendingContainers#root	| Number of containers to be allocated in the root queue |
| AllocatedMB#root	| Amount of memory allocated in the root queue |
| AllocatedVCores#root	| Number of virtual cores allocated in the root queue |
| ReservedVCores#root	| Number of virtual cores reserved in the root queue |
| AllocatedContainers#root	| Number of containers allocated in the root queue |
| ReservedMB#root| 	Amount of memory reserved in the root queue |
| AppsKilled#root	| Number of tasks terminated in the root queue |
| AppsFailed#root	| Number of tasks failed in the root queue |
| AppsCompleted#root	| Number of tasks completed in the root queue |
| AppsSubmitted#root	| Number of tasks submitted in the root queue |
| AvailableVCoresPercentage#root	| Proportion of virtual cores available in the root queue in percentages |

- Statistical Rule: The cluster load metric selected by the user is triggered once when the threshold is reached according to the selected aggregated dimension (average value) within a specific statistical period.
- Statistical Period: The statistical duration of the metric. Currently, three statistical periods are supported: 300 seconds, 600 seconds, and 900 seconds.
- Repeat Count: The number of times that the threshold of the aggregated load metric is reached. When the repeat count is reached, the cluster will be automatically scaled.
- Scale-out mode: You can select **Node**, **Memory**, or **Core**, and their values must be an integer other than 0.
	- In case of scale-out in core or memory mode, the quantity of nodes guaranteeing the maximum computing power will be added.
<dx-alert infotype="explain" title="For example:">
1. In core mode, if ten cores are to be added, but the specification for automatic scaling is to add eight cores in order of priority, then **two 8-core nodes** will be added when the rule is triggered.
2. In memory mode, if 20 GB memory is to be added, but the specification for automatic scaling is to add 16 GB memory in order of priority, then **two 16 GB MEM nodes** will be added when the rule is triggered.
</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/fe9824460bd3105e6a35f6ccacf89520.jpg)
- Scale-in mode: You can select **Node**, **Memory**, or **Core**, and their values must be an integer other than 0.
	- In case of scale-in in core or memory mode, a minimum quantity of nodes will be released in reverse chronological order while keeping the business running properly, with at least one node released.
<dx-alert infotype="explain" title="For example:">
1. In core mode, if 20 cores are to be released, and when a scale-in rule is triggered, there are three 8-core 16 GB MEM elastic nodes and two 4-core 8 GB MEM elastic nodes in reverse chronological order in the cluster, then **two 8-core 16 GB MEM nodes** will be released.
2. In memory mode, if 30 GB memory is to be released, and when a scale-in rule is triggered, there are three 8-core 16 GB MEM elastic nodes and two 4-core 8 GB MEM elastic nodes in reverse chronological order in the cluster, then **one 8-core 16 GB MEM node** will be deleted.
</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/bca1f916bc44b87655f651802bcd3f13.jpg)
- Cooldown Period: The interval (60 to 43,200 seconds) before carrying out the next automatic scaling action after the rule is successfully executed.
- Graceful Scale-In: After this feature is enabled, if the scale-in action is triggered when a node is executing tasks, the node will not be released immediately. Instead, the scale-in action will be executed after the tasks are completed. However, the scale-in action will still be executed if the tasks are not completed within the specified time.
![](https://qcloudimg.tencent-cloud.cn/raw/94d581710e32eadc790d30775d906f04.jpg)

### Time-based scaling
There are obvious peaks and troughs in cluster computing volume during a certain period. You can configure scaling policies based on time to ensure that important jobs are completed on time. Time–based scaling policies allows you to set to automatically add or remove task nodes daily, weekly, or monthly at a fixed time period.
![](https://qcloudimg.tencent-cloud.cn/raw/339a47bcf3219a39a3b250f26c4e840f.jpg)
To add a time-based scaling rule, select **Time-based scaling** as the **Auto Scaling Type**, click **Add Rule**, and configure the following fields:

- Rule Name: The name of the scaling rule. The scaling rule names in the same cluster must be unique (including scale-out and scale-in rules).
- Scale-out Service: By default, the selected component will inherit the cluster-level configuration and fall into the default configuration group for that node type. You can also set the configuration of the target component through the **Specify configuration** parameter.
- Once: Triggers a scaling action once at a specific time, accurate to the minute.
- Recurring: Triggers a scaling action daily, weekly, or monthly at a specific time or time period.
- Retry Time after Expiration: Automatic scaling may not be executed for various reasons at the specified time. After you set the retry time after expiration, the system will try to execute the scaling once a while within the time until it is executed when the conditions are met.
- Valid To: The time-based scaling rule is valid until the end of the date specified here.
- Scale-out mode: You can select **Node**, **Memory**, or **Core**, and their values must be an integer other than 0.
	- In case of scale-out in core or memory mode, the quantity of nodes guaranteeing the maximum computing power will be added.
<dx-alert infotype="explain" title="For example:">
1. In core mode, if ten cores are to be added, but the specification for automatic scaling is to add eight cores in order of priority, then **two 8-core nodes** will be added when the rule is triggered.
2. In memory mode, if 20 GB memory is to be added, but the specification for automatic scaling is to add 16 GB memory in order of priority, then **two 16 GB MEM nodes** will be added when the rule is triggered.
</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/96e59e8c87878869aaece3b869b751af.jpg)
- Scale-in mode: You can select **Node**, **Memory**, or **Core**, and their values must be an integer other than 0.
	- In case of scale-in in core or memory mode, a minimum quantity of nodes will be released in reverse chronological order while keeping the business running properly, with at least one node released.

<dx-alert infotype="explain" title="For example:">
1. In core mode, if 20 cores are to be released, and when a scale-in rule is triggered, there are three 8-core 16 GB MEM elastic nodes and two 4-core 8 GB MEM elastic nodes in reverse chronological order in the cluster, then **two 8-core 16 GB MEM nodes** will be released.
2. In memory mode, if 30 GB memory is to be released, and when a scale-in rule is triggered, there are three 8-core 16 GB MEM elastic nodes and two 4-core 8 GB MEM elastic nodes in reverse chronological order in the cluster, then **one 8-core 16 GB MEM node** will be deleted.
</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/4bd338e10a4314bc951d0b4a54d184e1.jpg)
- Cooldown Period: The interval (60 to 43,200 seconds) before carrying out the next automatic scaling action after the rule is successfully executed.
- Scheduled termination: You can specify the usage duration for the added nodes, so that the nodes will not be affected when a scale-in rule is triggered. **Unlimited** is selected by default. You can enter an integer between 1–24 hours here.
<dx-alert infotype="explain" title="Use case:">
This field applies when you need more computing resources for a specified period of time (within one day) and the resources should not be affected by other scale-in rules.
</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/c334c587b15221f1e52bbbf4e570f339.jpg)
- Rule Status: Used to mark whether the rule is enabled. The default status of a rule is "enabled". When you don't want a rule to be executed but still wish to retain it, you can set the rule status to "disabled".
- Graceful Scale-In: After this feature is enabled, if the scale-in action is triggered when a node is executing tasks, the node will not be released immediately. Instead, the scale-in action will be executed after the tasks are completed. However, the scale-in action will still be executed if the tasks are not completed within the specified time.
![](https://qcloudimg.tencent-cloud.cn/raw/a83debcb7c2b80fffd23e83e7ae9e649.jpg)

