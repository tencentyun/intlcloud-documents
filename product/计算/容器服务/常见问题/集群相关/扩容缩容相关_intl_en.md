### What is the difference between Cluster Autoscaler and node auto scaling based on monitoring metrics?

Cluster Autoscaler (CA) ensures that all pods in the cluster can be scheduled regardless of the actual load, while node auto scaling based on monitoring metrics do not take pods into consideration during auto scaling. Therefore, nodes without pods might be added, or nodes with system-critical pods such as kube-dns might be deleted during auto scaling. Kubernetes discourages the latter auto scaling mechanism. In conclusion, these two modes conflict and should not be enabled at the same time. 

### How does CA work with auto scaling groups?

A CA-enabled cluster will, according to the configuration of the selected node, create a launch configuration and bind an auto scaling group to it. The cluster will then perform scale-in/out in this bound auto scaling group. CVM instances scaled out are automatically added to the cluster. Nodes that are automatically scaled in/out are billed on a pay-as-you-go basis. For more information about auto scaling group, see [Auto Scaling (AS)](https://intl.cloud.tencent.com/document/product/377).

### Can a node manually added in the TKE Console be scaled in by CA?

No. CA only scales in the nodes within the auto scaling group. Nodes that are added on the [TKE Console](https://console.cloud.tencent.com/tke2) are not added to the auto scaling group.

### Can a CVM instance be added or removed in the AS Console?

No. We do not recommend making any modifications on the [AS Console](https://console.cloud.tencent.com/autoscaling).

### What configurations of the selected node will be inherited during scaling?

When creating an auto scaling group, you need to select a node in the cluster as a reference to create a [launch configuration](https://intl.cloud.tencent.com/document/product/377/8543). The node configuration for reference includes:
 - vCPU
 - Memory
 - System disk size
 - Data disk size
 - Disk type
 - Bandwidth
 - Bandwidth billing method
 - Whether to assign public IP
 - Security group
 - VPC
 - Subnet

### How do I use multiple auto scaling groups?

Based on the level and type of the service, you can create multiple auto scaling groups, set different labels for them, and specify the label for the nodes scaled out in the auto scaling groups to classify the service.

### What is the maximum quota for scaling?

Each Tencent Cloud user is provided with a quota of 30 pay-as-you go CVM instances in each availability zone. You can submit a ticket to apply for more instances for your auto scaling group.
For more information about the quotas, see [CVM Instance Quantity and Quota](https://console.cloud.tencent.com/cvm/overview) for your current availability zone. In addition, there is a maximum limit of 200 instances for Auto Scaling. You can submit a ticket to apply for a higher quota.

### Is scale-in safe for the cluster?

Since pods will be rescheduled when a node is scaled in, scale-in can be performed only if the service can tolerate rescheduling and short-term interruption. We recommend using [PDB](https://kubernetes.io/docs/tasks/run-application/configure-pdb/). PDB can specify the minimum number/percentage of replicas for a pod set that remains available at all times. With PodDisruptionBudget, application deployers can make sure that the cluster operations that actively remove pods will not terminate too many pods at a time, which helps prevent data loss, service interruption, or unacceptable service degradation.

### What types of pods in a node will not be scaled in?

 - If you set strict PodDisruptionBudget for a pod, and the PDB is not met, it will not be scaled in.
 - Pods under Kube-system.
 - Pods on a node that are not created by controllers such as Deployment, ReplicaSet, Job, or StatefulSet.
 - Pods with local storage.
 - Pods that cannot be scheduled to another node.

### How long does it take to trigger scale-in after the condition is met?

10 minutes.

### How long does it take to trigger scale-in when the node is marked as Not Ready?

20 minutes.

### How often is a node scanned for scaling?

Every 10 seconds.

### How long does it take to scale out a CVM instance?

It generally takes less than 10 minutes. For more information, see [Auto Scaling](https://intl.cloud.tencent.com/document/product/377).

### Why is a node with an unschedulable pod not scaled out?

Please check the following:
- Whether the requested resource of the pod is too large.
- Whether a node selector is set.
- Whether the maximum number of nodes in the auto scaling group has been reached.
- Whether the account balance is sufficient (scale-out cannot be triggered if the account balance is insufficient) or the quota is insufficient. For more information, see [other reasons](https://intl.cloud.tencent.com/document/product/377/32527).


### How can I prevent CA from scaling in a specific node?

``` sh
# You can set the following information in the annotations of the node
kubectl annotate node <nodename> cluster-autoscaler.kubernetes.io/scale-down-disabled=true
```


### Where can I find details on the scaling events?

You can query the scaling events of an auto scaling group and view K8s events in the AS Console. Events can be found in the following three resources:
- kube-system/cluster-autoscaler-status config map
    - **ScaledUpGroup** - CA triggers scale-out.
    - **ScaleDownEmpty** - CA deletes a node with no running pod.
    - **ScaleDown** - CA triggers scale-in.
- node
    - **ScaleDown** - CA triggers scale-in.
    - **ScaleDownFailed** - CA failed to trigger scale-in.
- pod
    - **TriggeredScaleUp** - CA triggers scale-out because of this pod.
    - **NotTriggerScaleUp** - CA cannot find an available auto scaling group to schedule this pod.
    - **ScaleDown** - CA tries to drain this pod to scale in the node.

