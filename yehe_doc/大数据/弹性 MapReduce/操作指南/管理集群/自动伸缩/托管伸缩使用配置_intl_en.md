After the managed scaling feature is enabled, the system will continuously monitor the load of the YARN cluster and calculate the peak fluctuations in the last 10 minutes, so as to automatically add or remove task nodes. Managed scaling applies only to clusters containing the YARN component.
## Basic Settings
The **Basic settings** section allows you to set the node quantity range of the automatic scaling feature and the minimum number of pay-as-you-go nodes.
- Min number of nodes: The minimum number of task nodes a cluster can have when the managed scale-in policy is triggered.
- Max number of nodes: The maximum number of task nodes a cluster can have when the managed scale-out policy is triggered. The accumulated number of task nodes under one or more rules cannot exceed the maximum number of nodes.
- Min number of pay-as-you-go nodes: The minimum number of pay-as-you-go nodes to be added after a scale-out is triggered, which is used to set the proportion of pay-as-you-go nodes and spot instances. By default, the value is the maximum number of nodes.
<dx-alert infotype="explain" title="For example:">
If the minimum number of nodes is set to `0`, the maximum number of nodes to `100`, and the minimum number of pay-as-you-go nodes to `10`, at least 10 pay-as-you-go nodes will be added when a scale-out is triggered, with the remaining ones being spot instances. When spot instances are insufficient, additional pay-as-you-go nodes will be added to make up the difference.
</dx-alert>

## Scaling Specifications Management
Scaling specifications refer to node specifications for managed scaling. You can configure each cluster with up to five scaling specifications. When a scale-out rule is triggered, the scaling will be carried out according to the specification priority. When the high-priority specification has fewer resources than the number of resources to be added, the specification of the next priority will be used for supplement. In order to maintain the linear change of the cluster load, we recommend you keep the CPU and memory of the scaling specifications consistent. Managed scaling is supported only for host resources.
- You can add, delete, change, and query the nodes in the scaling specifications, and adjust the priority of scaling specifications as needed.
- The sequence of the five specifications for scale-out is as follows (same for pay-as-you-go and spot instances):
	- When the resources are sufficient: 1 > 2 > 3 > 4 > 5
<dx-alert infotype="explain" title="For example:">
If five preset specifications are available and the resources are sufficient, when a scale-out rule is triggered to add 10 nodes, 10 nodes with specification 1 will be added according to the sequence, and other preset specifications will not be selected.
</dx-alert>
	- When the resources are insufficient: 1 + 2 > 1 + 2 + 3 > 1 + 2 + 3 + 4 > 1 + 2 + 3 + 4 + 5.
<dx-alert infotype="explain" title="For example:">
If there are eight nodes with specification 1, four with specification 2, and three with specification 3, when a scale-out rule is triggered to add 13 nodes, eight nodes with specification 1, four with specification 2, and one with specification 3 will be added following the sequence.
</dx-alert>
	- When a resource specification is out of stock (take specification 2 as an example): 1 + 3 > 1 + 3 + 4 > 1 + 3 + 4 + 5.
<dx-alert infotype="explain" title="For example:">
- If there are eight nodes with specification 1, no nodes with specification 2 (out of stock), and three nodes with specification 3, when a scale-out rule is triggered to add 10 nodes, eight nodes with specification 1 and two nodes with specification 3 will be added according to the sequence, while specification 2 will not be selected.
- If there are eight nodes with specification 1 and nodes with other preset specifications are all out of stock, when a scale-out rule is triggered to add 10 nodes, eight nodes with specification 1 will be added, with the scale-out being partially successful.
</dx-alert>

## Managed scaling monitoring metrics
Managed scaling monitors many metrics and calculates the suggested number of nodes under each metric. Then, it determines on a scale-out or scale-in based on the number of nodes.

| Managed Scaling Monitoring Metric | Description | 
|---------|---------|
| AvailableMemPercentage	| Available memory in percentages | 
| AvailableVCoresPercentage	| Proportion of virtual cores available in YARN in percentages | 

Statistical Rule: The cluster load metric is set to process the peak loads in the last 10 minutes based on the specified aggregation dimension within a statistical period.
Statistical Period: The statistical duration of the metric, which is 1 minute.
By default, managed scaling applies the principle of quick scale-out and cautious and graceful scale-in.

