## Overview 
TKE’s cluster audit and event storage has configured rich visual charts for users to present audit logs and cluster events in multiple dimensions. It is simple to operate and covers most common cluster OPS scenarios. It is easy to find and locate problems, improves OPS efficiency, and maximizes the value of audit and event data.
With several specific usage scenarios and examples, this document describes how to use audit and event dashboards to quickly locate cluster problems.

## Prerequisites

You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1) and enabled [Cluster Audit](https://intl.cloud.tencent.com/document/product/457/38338) and [Event Storage](https://intl.cloud.tencent.com/document/product/457/30686).


## Use case

### Locating the problem of workload disappearance

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cluster Ops** > **Auditing Search** in the left sidebar to go to the **Auditing Search** page.
3. Click **K8s Object Operation Overview** tab and specify the **Operation Type** and **Resource Object** to query in the **Filter Item**.
4. Click **Filter**. 



### Locating the problem of node cordon

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cluster Ops** > **Auditing Search** in the left sidebar to go to the **Auditing Search** page.
3. Click **Node Operation Overview** and specify the cordon node to query in the **Filter Item**.
4. Click **Filter**. 

### Locating the problem of slow apiserver responses

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cluster Ops** > **Auditing Search** in the left sidebar to go to the **Auditing Search** page.
3. Click **Aggregation Search** tab to go to the **Aggregation Search** page. This page displays the trend of apiserver access in multiple dimensions such as [User](#user), [Operation Type](#type), and [Status Code](#statuscode).


### Locating the problem of node exception

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cluster Ops** > **Event Search** in the left sidebar to go to the **Event Search** page.
3. Click **Event Overview** tab. On the **Filter Item** page, enter the exception node IP in the **Resource Object**.
4. Click **Filter**. You can find that there is a "Insufficient Node Disk Space" event record.
5. Click the event to view the trend of exception event.


### Querying the cause of triggering node scale-out

For clusters with node pool **Auto Scaling** enabled, the CA (cluster-autoscler) add-on will automatically increase or decrease the number of nodes in the cluster based on the actual load. If the nodes in the cluster are automatically scaled out, users can trace the entire scaling process through event search.


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cluster Ops** > **Event Search** in the left sidebar to go to the **Event Search** page.
3. Click **Global Search** tab and enter the following command in search analysis box.
```
event.source.component : "cluster-autoscaler"
```
4. Select “`event.reason`”, “`event.message`”, “`event.involvedObject.name`”, and “`event.involvedObject.name`” to display in the **Hide Field** on the left side. Click **Search** to search the analysis log and return the search result.
5. The search result is sorted by “Log Time” in descending order.
