## Operation Scenario

This document guides you through the process of scaling a cluster. TKE supports the following scaling methods:
- [Manually adding/removing a node](#ManuallyAddAndRemove)
- [Automatically adding/removing a node via Auto Scaling](#AutomaticAddAndRemove)

## Prerequisites

You are logged in to the [TKE console](https://console.cloud.tencent.com/tke2).

## Directions

<span id="ManuallyAddAndRemove"></span>
### Manually Adding/removing a Node

#### Creating a Node

For detailed directions, see [Creating a Node](https://cloud.tencent.com/document/product/457/32203#createNode).
During the creation, you can configure the CVM instance and scale the cluster on the "CVM configuration" page.

#### Adding an Existing Node

>- Currently, you can only add CVM instances in the same VPC.
> - Adding an existing node to the cluster will reinstall the OS of the CVM instance.
> - Adding an existing node to the cluster will migrate the CVM instance to the project set for the cluster.
> - When adding a node with only one data disk to the cluster, you can choose whether to set the container directory. Setting the container directory will format the data disk. For CVM instances with no or multiple data disks, setting the container directory will not take effect.

For detailed directions, see [Adding an Existing Node](https://cloud.tencent.com/document/product/457/32203#addExistingNode).
During the adding process, you can configure the CVM instance to be added to the cluster and scale the cluster on the "CVM configuration" page.

#### Removing a Node

For detailed directions, see [Removing a Node](https://cloud.tencent.com/document/product/457/32204).

<span id="AutomaticAddAndRemove"></span>
### Automatically Adding/removing a Node via Auto Scaling

Cluster Autoscaler (CA) is a standalone program. It can dynamically adjust the number of nodes in a cluster to meet actual needs. When a Pod in the cluster cannot be scheduled due to insufficient resources, scale-up will be triggered automatically, which reduces the labor costs. When a scale-down condition such as node idleness is met, scale-down will be triggered automatically, which reduces the resource costs.

#### Enabling CA

##### Creating a Single Scaling Group
1. Create a cluster as instructed in [step 1](https://cloud.tencent.com/document/product/457/32189#step1) to [step 7](https://cloud.tencent.com/document/product/457/32189#step7) in [Creating a Cluster](https://cloud.tencent.com/document/product/457/32189).
2. In "CVM configuration", configure other settings for the CVM instance and set "Automatic adjustment" to "On". See the figure below:
![Automatic adjustment](https://main.qcloudimg.com/raw/dac7f8a3cf82c0c842698cb4057185a6.png)
3. Click **Next**.
4. Click **Finish** to complete the creation of an automatically scalable cluster.

##### Creating Multiple Scaling Groups

1. <span id="step1">In the left sidebar, Click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=4)** to go to the cluster management page. </span>
2. Click the ID/name of the cluster where multiple scaling groups needs to be created to enter the cluster management page. See the figure below:
![Management page](https://main.qcloudimg.com/raw/e9fc5f8b9859128d7fa52742c7dc8bb4.png)
3. In the left sidebar, select "Node Management" > "Scaling groups" to go to the "Scaling group list" page.
4. Click **Create a scaling group** to pop up the "Create a scaling group" window. See the figure below:
![Create a scaling group](https://main.qcloudimg.com/raw/3876330e9cadc489cac5b7fccc8672a9.png)
5. Set the scaling group based on actual needs. Main parameters include:
 - Name: Custom.
 - Startup configuration: Set based on actual needs.
 - Node quantity limit: Limit the number of nodes in the scaling group.
 - Label: Set the Label for the scaling group. The Label will be set on the nodes that are created during automatic scale-up to implement elastic scheduling policies for services.
6. <span id="step6">Click **Submit** to complete the creation. </span>
7. Repeat [step 1](#step1) to [step 6](#step6) to create multiple scaling groups.


>- You need to configure the request value of the container under the service: Automatic scale-up will be triggered if there is a Pod in the cluster that cannot be scheduled due to insufficient resources, and it is based on the Pod's request value to determine whether the resources are sufficient.
> - Do not directly modify the nodes in a scaling group.
> - All nodes in the same scaling group should have the same configuration (such as model and Label).
> - PodDisruptionBudget (PDB) can be used to prevent a Pod from being deleted during scale-down.
> - Check whether the quota of the availability zone is large enough before setting the minimum/maximum node quantity for the scaling group.
> - It is not recommended to enable monitoring metric-based auto scaling of nodes.
> - Deleting a scaling group will also terminate the CVM instances in it. Please be cautious when doing so.

#### Scaling Trigger Conditions

##### Scale-up Conditions

When a container Pod in a cluster cannot be scheduled due to lack of available resources, the auto scale-up policy will be triggered to try scaling up the node to run the Pod.
Whenever the Kubernetes scheduler cannot find a place to run a Pod, it will set the Pod's PodCondition to false and set the reason to "unschedulable". CA will scan at a set interval to see whether there are unschedulable Pods, and if yes, try scaling up the node to run these Pods.

##### Scale-down Conditions

When the ratios of CPU request and memory request of all Pods on a node are both less than 50%, the node will be scaled down as an alternative. When all of the following scale-down conditions are met, the node can be scaled down only if all Pods on it can be scheduled to another node.
- If the Pod for which you set strict PDB does not satisfy the PDB, it will not be scaled down.
- The Pod is under Kube-system.
- There are Pods that are not created by controllers such as Deployment, ReplicaSet, Job, or StatefulSet on the node.
- The Pod has local storage.
- The Pod cannot be scheduled to another node.

## FAQs

For issues related to scaling, see [FAQs for Scaling](https://cloud.tencent.com/document/product/457/32316).
