## Overview

You can specify the scheduling of the Pods under a workload in the cluster by setting the scheduling rule in the advanced settings of the workload. This is suitable for the following application scenarios:
- Run the Pods on the specified node.
- Run the Pods on a node in the specified scope (which can be an attribute such as availability zone or model).
- Force the Pods to run on separate nodes (one for each node, and scheduling of non-eligible Pods will be stopped).

## How to Use

### Prerequisites

- A scheduling rule is set in the advanced settings of the workload, and the Kubernetes version of the cluster is 1.7 or higher.
- To ensure that your Pods can be scheduled successfully, please make sure that the node has resources available for container scheduling after the scheduling rule is set.
- When using the custom scheduling feature, you need to set the corresponding Label for the node. For details, see [Setting Node Label](https://intl.cloud.tencent.com/document/product/457/30657).

### Setting a Scheduling Rule

If your cluster is version 1.7 or higher, you can set a scheduling rule when creating a workload.
You can choose one of the following two scheduling types based on your actual needs:
- **Specified node for scheduling**: Set to schedule the Pods to the specified node by matching the node Label.
![](https://main.qcloudimg.com/raw/d999b561e17200605ed662f9fb427b33.png)
- **Custom scheduling rule**: Customize a Pod scheduling rule by matching Pod Label.
![](https://main.qcloudimg.com/raw/8dc1bb38e4b982de9124eb0f9188359d.png)

A custom scheduling rule has the following two modes:
- Mandatory conditions: If a node meets the affinity conditions during the scheduling, the Pods will be scheduled to the corresponding node. If no node satisfies the conditions, the scheduling will fail.
- Preferred conditions: If a node meets the affinity conditions during the scheduling, the Pods will be scheduled to the corresponding node. If no node satisfies the conditions, the Pods will be scheduled to a random node.

Multiple custom scheduling rules can be added. The meanings of each rule operator are as follows:
- In: The value of the Label is in the list.
- NotIn: The value of the Label is not in the list.
- Exists: The key of the Label exists.
- DoesNotExits: The key of the Label does not exist.
- Gt: The value of the Label is greater than the list value (string match).
- Lt: The value of the Label is less than the list value (string match).

## How It Works

The scheduling rule of a service is delivered to the Kubernetes cluster mainly through YAML. The affinity and anti-affinity mechanism of Kubernetes will cause the Pods to be scheduled according to the specific rule. Fore more information about Kubernetes' affinity and anti-affinity mechanism, click [here](https://kubernetes.io/docs/concepts/configuration/assign-Pod-node/).

