## Overview
When the demand for resources in your cluster grows or shrinks, the automatic scaling feature automatically add or remove the task nodes, helping you save costs while meeting the requirement for cluster computing power. Automatic scaling supports two kinds of scaling policies: load-based scaling and time-based scaling.

## Prerequisites
1. The automatic scaling feature scales task nodes only.
2. The automatic scaling feature is only available for Hadoop clusters.
3. You can use either the load-based scaling policy or time-based scaling policy, but not both at the same time.

## Directions
Log in to the [EMR console](https://console.cloud.tencent.com/emr), click a **Cluster ID/Name** in the cluster list to enter the cluster details page, and select **Auto Scaling** > **Basic Settings** > **Edit** to configure a scaling policy.
![](https://main.qcloudimg.com/raw/daeb0420d0cf9803526169ba30544c03.png)


### Basic settings
Policy restriction is used to specify the number of automatic scaling task nodes allowed in a cluster when an automatic scaling rule is triggered.
- Min Number of Instances: The minimum number of tasks nodes a cluster can have when the auto scaling policy is triggered.
- Max Number of Instances: The maximum number of task nodes a cluster can have when the auto scaling policy is triggered; the accumulated number of task nodes under one or more rules or policies cannot exceed the max number of instances.
![](https://main.qcloudimg.com/raw/f912e2b7a9fe03f03f5bc6da8bf220f5.png)
- Release all: Clears all nodes added in an automatic scaling action with one click.
- Release spot instances: Clears all spot instances added in an automatic scaling action with one click.
- Release pay-as-you-go instances: Clears all pay-as-you-go instances added in an automatic scaling action with one click.


### Setting scaling specifications
Scaling specifications refer to node specifications for automatic scaling. You can configure each cluster with up to three scaling specifications, supporting pay-as-you-go and spot instance. When a scale-out rule is triggered, the scaling will be carried out according to the specification priority. When the high-priority specification has fewer nodes than the number of nodes to be added, the specification of the next priority will be used. In order to maintain the linear change of the cluster load, you are advised to keep the CPU and memory of the scaling specifications consistent.
- The scaling specifications support up to three kinds of instances, and the scaling priority order is 1 > 2 > 3.
- You can add, delete, change, and query the instances in the scaling specifications, and adjust the priority of scaling specifications as needed.

![](https://main.qcloudimg.com/raw/45f69ce71bddc950669f88cc2368de84.png)
![](https://main.qcloudimg.com/raw/3869d69900a8f74d60fe62ce31141917.png)

### Setting scaling rules
Scaling rules are business policies used to configure the triggering conditions of scaling actions and the number of nodes to be added or removed. Automatic scaling supports two kinds of policies, load-based scaling and time-based scaling. You can choose to use either of the two kinds of policies, but not both at the same time. When you switch the policies, the original scaling rules will be retained in an invalid state and will not be triggered. Those already added nodes will also be retained unless a scale-in rule is triggered. Each policies can be configured with up to 10 scaling rules. When two rules are triggered at the same time, the rule of the higher priority will be executed first.
![](https://main.qcloudimg.com/raw/542494e6a15c96cb0a9503715beaef99.png)

To set a scaling rule, select **Load-based scaling** or **Time-based scaling** for **Auto Scaling Type** in the **Scaling Rule Management** module and click **Add Rule**.
![](https://main.qcloudimg.com/raw/e1f8703dc9b3a125139aed3b90f9ee7d.png)

#### Load-based scaling
When it is impossible to accurately estimate the peak and trough of cluster computing, you can configure the scaling policy based on the load to ensure that important jobs are completed on time. The load is mainly based on the preset YARN metric statistics rules and the task nodes are automatically adjusted when the preset conditions are triggered.

To add a load-based scaling rule, select **Load-based scaling** as the **Auto Scaling Type**, click **Add Rule**, and configure the following fields:
- Rule Name: The name of the scaling rule. The scaling rule names in the same cluster must be unique (including scale-out and scale-in rules).
- Valid Time: The load-based scaling rule can be triggered only within the valid time. **Unlimited** is selected by default and you can customize the valid time.    
- Load Metric: Set the condition rule for triggering threshold based on the selected cluster load metric. Here refers to the load metric of YARN.
<table>
<thead>
<tr>
<th><strong>EMR - Automatic Scaling Metric</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody><tr>
<td>AvailableVCores#root</td>
<td>Number of virtual cores available in the root queue</td>
</tr><tr>
<td>PendingVCores#root</td>
<td>Number of virtual cores waiting to be available in the root queue</td>
</tr><tr>
<td>AvailableMB#root</td>
<td>Amount of memory available in the root queue in MB</td>
</tr><tr>
<td>PendingMB#root</td>
<td>Amount of memory waiting to be available in the root queue in MB</td>
</tr><tr>
<td>AvailableMemPercentage</td>
<td>Available memory in percentages</td>
</tr><tr>
<td>ContainerPendingRatio</td>
<td>Ratio of the number of containers to be allocated to the number of allocated containers</td>
</tr><tr>
<td>AppsRunning#root</td>
<td>Number of running tasks in the root queue</td>
</tr><tr>
<td>AppsPending#root</td>
<td>Number of pending tasks in the root queue</td>
</tr><tr>
<td>PendingContainers#root</td>
<td>Number of containers to be allocated in the root queue</td>
</tr><tr>
<td>AllocatedMB#root</td>
<td>Amount of memory allocated in the root queue</td>
</tr><tr>
<td>AllocatedVCores#root</td>
<td>Number of virtual cores allocated in the root queue</td>
</tr><tr>
<td>ReservedVCores#root</td>
<td>Number of virtual cores reserved in the root queue</td>
</tr><tr>
<td>AllocatedContainers#root</td>
<td>Number of containers allocated in the root queue</td>
</tr><tr>
<td>ReservedMB#root</td>
<td>Amount of memory reserved in the root queue</td>
</tr><tr>
<td>AppsKilled#root</td>
<td>Number of tasks terminated in the root queue</td>
</tr><tr>
<td>AppsFailed#root</td>
<td>Number of tasks failed in the root queue</td>
</tr><tr>
<td>AppsCompleted#root</td>
<td>Number of tasks completed in the root queue</td>
</tr><tr>
<td>AppsSubmitted#root</td>
<td>Number of tasks submitted in the root queue</td>
</tr><tr>
<td>AvailableVCoresPercentage#root</td>
<td>Proportion of virtual cores available in the root queue in percentages</td>
</tr>
</tbody></table>
- Statistical Rule: The cluster load metric selected by the user is triggered once when the threshold is reached according to the selected aggregated dimension (average value) within a specific statistical period.
- Statistical Period: The statistical duration of the metric. Currently, three statistical periods are supported: 300 seconds, 600 seconds, and 900 seconds.
- Repeat Count: The number of times that the threshold of the aggregated load metric is reached. When the repeat count is reached, the cluster will be automatically scaled.
- Scale-out Quantity: The number of task nodes to be added each time when the rule is triggered.
- Scale-in Quantity: The number of task nodes to be removed each time when the rule is triggered.
- Cooldown Period: The interval (600 to 43,200 seconds) before carrying out the next automatic scaling action after the rule is successfully executed.
- Rule Status: Used to mark whether the rule is enabled. The default status of a rule is "enabled". When you don't want a rule to be executed but still wish to retain it, you can set the rule status to "disabled".     

![](https://main.qcloudimg.com/raw/751758d5778cc0ff2623843be3a8a224.png)

#### Time-based scaling
There are obvious peaks and troughs in cluster computing volume during a certain period. You can configure scaling policies based on time to ensure that important jobs are completed on time. Time–based scaling policies allows you to set to automatically add or remove task nodes daily, weekly, or monthly at a fixed time period.

To add a time-based scaling rule, select **Time-based scaling** as the **Auto Scaling Type**, click **Add Rule**, and configure the following fields:
- Rule Name: The name of the scaling rule. The scaling rule names in the same cluster must be unique (including scale-out and scale-in rules).
- Once: Triggers a scaling action once at a specific time, accurate to the minute.
- Recurring: Triggers a scaling action daily, weekly, or monthly at a specific time or time period.
- Retry Time after Expiration: Automatic scaling may not be executed for various reasons at the specified time. After you set the retry time after expiration, the system will try to execute the scaling every 30 seconds within the time until it is executed when the conditions are met.
- Valid To: The time-based scaling rule is valid until the end of the date specified here.
- Scale-out Quantity: The number of task nodes to be added each time when the rule is triggered.
- Scale-in Quantity: The number of task nodes to be removed each time when the rule is triggered.
- Cooldown Period: The interval (600 to 43,200 seconds) before carrying out the next automatic scaling action after the rule is successfully executed.
- Rule Status: Used to mark whether the rule is enabled. The default status of a rule is "enabled". When you don't want a rule to be executed but still wish to retain it, you can set the rule status to "disabled".
- Graceful Scale-In: After this feature is enabled, if the scale-in action is triggered when a node is executing tasks, the node will not be released immediately. Instead, the scale-in action will be executed after the tasks are completed. However, the scale-in action will still be executed if the tasks are not completed within the specified time.

![](https://main.qcloudimg.com/raw/bec5a2e47dff41cdd7cd20210355aef9.png)

### Viewing automatic scaling records
The records of automatic scaling actions can be viewed in **Scaling History**.
- Supports filtering the scaling records by time and searching by policy name.
- Supports sorting by execution time, policy name, scaling type, execution status. You can click **Details** in the **Operation** column to view detailed information.
- There are four execution statuses of automatic scaling:
 - Executing: The automatic scaling is being executed.
 - Successful: All nodes are added to or removed from the cluster.
 - Partially successful: Some nodes are successfully added to or removed from the cluster and some failed to be added or removed due to disk quota management or CVM inventory.
 - Failed: No node is added to or removed from the cluster.
