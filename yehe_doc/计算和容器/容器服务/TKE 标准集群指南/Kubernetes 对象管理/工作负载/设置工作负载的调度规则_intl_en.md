## Introduction

You can specify the scheduling of the Pods under a workload in the cluster by setting the scheduling policy in the advanced settings of the workload. The following are the typical use cases:
- Run the Pods on a specific node.
- Run the Pods on nodes in a specific scope (which can be an availability zone, a model and so on).
- Force the Pods to run on separate nodes (one for each node, and scheduling of non-eligible Pods is stopped).

## How to Configure Scheduling policies

### Prerequisites

- Kubernetes 1.7 or later, and scheduling policies are configured. Scheduling policies can be found under the Advanced Settings of a workload.
- To ensure that your Pods can be scheduled successfully, the node should have resources available for container scheduling after the scheduling policy is configured.
- You need node labels if you use custom scheduling features. For details, refer to [Setting Node Label](https://intl.cloud.tencent.com/document/product/457/30657).

### Configuring a scheduling policy

If your cluster is created using Kubernetes 1.7 or later, you can set a scheduling policy when creating a workload.
Select one of the following scheduling types:
- **Schedule to a specific node**: schedule Pods to a specific node with matching node labels.
![](https://main.qcloudimg.com/raw/d999b561e17200605ed662f9fb427b33.png)
- **Custom scheduling**: customize how Pods are scheduled by matching Pod labels.
![](https://main.qcloudimg.com/raw/8dc1bb38e4b982de9124eb0f9188359d.png)

Custom scheduling policies have the following modes:
- Conditions that must be met: if a node meets the affinity conditions, the Pods are scheduled to the corresponding node. If not, the scheduling fails.
- Conditions that should be met if possible: if a node meets the affinity conditions, the Pods are scheduled to the corresponding node. If not, the pods are scheduled to a random node.

Multiple custom scheduling policies can be added. The following is a list of operators:
- In: the value of the label is in the list.
- NotIn: the value of the label is not in the list.
- Exists: the key of the label exists.
- DoesNotExits: the key of the label does not exist.
- Gt: the value of the label is greater than the listed value (string match).
- Lt: the value of the label is less than the listed value (string match).

## How It Works

Kubernetes uses YAML files to distribute scheduling policies and the affinity and anti-affinity mechanism ensures that Pods are scheduled according to rules. For more information on this mechanism, refer to [Kubernetes official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity).


