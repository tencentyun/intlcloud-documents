## Overview

Situations in the cluster emerge one after another and are unpredictable, such as abnormal node status and pod restarts. If these situations cannot be perceived in the first place, users will miss the best time to deal with them. It's often too late to find out when the problem worsens and affects businesses.
Event logs record comprehensive information about cluster status changes, helping users find and troubleshoot problems in the first place.

## Event Log Definition

An event log is one of many resource objects in Kubernetes and is usually used to record status changes within a cluster, ranging from cluster node exceptions to pod startup and scheduling success. You can use the 'kubectl describe' command to view the event log information of resources.

## Event Log Fields

![img](https://qcloudimg.tencent-cloud.cn/raw/cfd3f25b635123d9ea29abe6bbf323fe.png)

- Level (`type`): Currently only the Normal and Warning levels are supported. If necessary, you can customize a level.
- Resource type/object (`involvedobject`): Objects involved in the event, such as Pod, Deployment, and Node.
- Event source (`source`): Component that reports the event, such as Scheduler and Kubelet.
- Content (`reason`): Brief description of the current event. Generally, an enumerated value is used. This field is used within the program.
- Detailed description (`message`): Detailed description of the current event.
- Number of occurrences (`count`): Number of times the event occurs

## Using Event Logs for Troubleshooting

CLS provides a one-stop service for Kubernetes event logs, including collection, storage, search, and analysis capabilities. You only need to enable the cluster event log feature with a few clicks to obtain a visual event log analysis dashboard out of the box. With visual charts, you can easily solve most common Ops problems via the console.

### Prerequisites

You have purchased the Tencent Kubernetes Engine (TKE) service and enabled the cluster event log feature. For more information, see [Event Storage](https://intl.cloud.tencent.com/document/product/457/30686).

### Scenario 1: An exception occurred on a node, and you need to locate the cause

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1).
2. On the left sidebar, click **Log Management** > **Event Log**.
3. On the **Event Search** page, click **Event Overview** tab and enter the exception node name as the filter item.

The query result is displayed.

Check the exception event trend and top exception events.

Starting from `2020-11-25`, the node `172.16.18.13` was exceptional due to insufficient disk space. Then Kubelet began to drain pods on the node to repossess the node's disk space.

### Scenario 2: A node triggered expansion, and you need to backtrack the expansion process to determine the cause

For clusters with [node pool](https://intl.cloud.tencent.com/document/product/457/35900) **auto scaling** enabled, the Cluster Autoscaler (CA) component will automatically increase or decrease the number of nodes in the cluster based on the actual load. If the nodes in the cluster are automatically scaled out, users can trace the entire scaling process through event search.
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1).
2. On the left sidebar, click **Log Management** > **Event Log**.
3. On the **Event Search** page, click the **Global Search** tab, and enter the following search command:
```
event.source.component : "cluster-autoscaler"
```
4. In the **Hidden Field** on the left side, select `event.reason`, `event.message`, `event.involvedObject.name`, and `event.involvedObject.name` to display. Sort the query results in reverse order by `Log Time`.

According to the event flow, you can find that the node scaling occurred around `2020-11-25 20:35:45` and was triggered by three NGINX pods (nginx-5dbf784b68-tq8rd, nginx-5dbf784b68-fpvbx, and nginx-5dbf784b68-v9jv5). After three nodes were scaled out, the subsequent scaling was not triggered because the number of nodes in the node pool reached the upper limit.


