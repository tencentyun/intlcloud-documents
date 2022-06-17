## Use Cases  
The cluster auditing and event storage features of TKE are configured with rich visual charts to display audit logs and cluster events in multiple dimensions. Their operations are simple, and most common cluster Ops use cases are covered, making it easy for you to find and locate problems, improve the Ops efficiency, and maximize the value of audit and event data.  
This document describes how to use audit and event dashboards to quickly locate cluster problems for several use cases.  

## Prerequisites

You have logged into the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=1) and enabled [cluster auditing](https://intl.cloud.tencent.com/document/product/457/38338) and [event storage](https://intl.cloud.tencent.com/document/product/457/30686).  


## Samples

### Sample 1. Troubleshooting workload disappearance

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).  
2. On the left sidebar, select **Cluster Ops** > **Auditing Search**.  
3. Select the **K8s Object Operation Overview** tab and specify the operation type and resource object to be checked in **Filters**.
4. Click **Filter** to start the query. The result is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/f6e60629ca780079d5989d4af5ce4239.png)
As shown above, the `10001****7138` account deleted the `nginx` application at `2020-11-30T03:37:13`. For more information on the account, select **CAM** > **[User List](https://console.cloud.tencent.com/cam)**.  



### Sample 2. Troubleshooting node cordoning

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).  
2. On the left sidebar, select **Cluster Ops** > **Auditing Search**.  
3. Select the **Node Operation Overview** tab and specify the name of the cordoned node in **Filters**.
4. Click **Filter** to start the query. The result is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/672957a4a5836f498287d044219c80fa.png)
As shown above, the `10001****7138` account cordoned the `172.16.18.13` node at `2020-11-30T06:22:18`.  

### Sample 3. Troubleshooting slow API server response

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).  
2. On the left sidebar, select **Cluster Ops** > **Auditing Search**.  
3. Select the **Aggregated Search** tab, which provides trend graphs of API server access requests in multiple dimensions, such as [user](#user), [operation type](#type), and [return status code](#statuscode), as shown below:
 - [](id:user)**Operator distribution trend**:
![](https://qcloudimg.tencent-cloud.cn/raw/2dad8bf340b3fe2e3f1b5f8d2b6b21f0.png)
 - [](id:type)**Operation type distribution trend**:
![](https://qcloudimg.tencent-cloud.cn/raw/628762399195378d8c420a2084cfa409.png)
 - [](id:statuscode)**Status code distribution trend**:
![](https://qcloudimg.tencent-cloud.cn/raw/90859325d3dcbed84a71e48291acb5e8.png)
As shown above, the `tke-kube-state-metrics` user has much more access requests than others. The [operation type distribution trend](#type) shows that most of the operations are LIST operations, and the [status code distribution trend](#statuscode) shows that most of the status codes are 403. The business logs show that the `tke-kube-state-metrics` add-on kept requesting API server retries due to the RBAC authentication issue, resulting in a sharp increase in API server access requests. Below is a sample log:
```plaintext
E1130 06:19:37.368981       1 reflector.go:156] pkg/mod/k8s.io/client-go@v0.0.0-20191109102209-3c0d1af94be5/tools/cache/reflector.go:108: Failed to list *v1.VolumeAttachment: volumeattachments.storage.k8s.io is forbidden: User "system:serviceaccount:kube-system:tke-kube-state-metrics" cannot list resource "volumeattachments" in API group "storage.k8s.io" at the cluster scope
```


### Sample 4. Troubleshooting a node exception

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).  
2. On the left sidebar, select **Cluster Ops** > **Event Search**.  
3. Select the **Event Overview** tab and enter the abnormal node IP in the **Resource Object** filter.
4. Click **Filter** to start the query. 
5. Click the event to further view the trend of the abnormal event.  
![](https://qcloudimg.tencent-cloud.cn/raw/47c2fdb36047268beef5c5c705cfd4b5.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c7fd62aa1f2e7b28f351c9a2f84cc3cb.png)
As shown above, starting from `2020-11-25`, the `172.16.18.13` node was abnormal due to insufficient disk space, after which kubelet started to try evicting Pods on the node to repossess the disk space.  


### Sample 5. Locating a node scale-out trigger

The cluster auto-scaler (CA) add-on automatically increases or decreases the number of nodes in the cluster according to the load condition when node pool **elastic scaling** is enabled. If a node in the cluster is automatically scaled, you can backtrack the whole scaling process through event search.  


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).  
2. On the left sidebar, select **Cluster Ops** > **Event Search**.  
3. Select the **Global Search** tab and enter the following search command in the search box:
```
event.source.component : "cluster-autoscaler"
```
4. Select **`event.reason`**, **`event.message`**, and **`event.involvedObject.name`** from the **Hidden Fields** on the left for display. Click **Search and Analysis** and view the results.  
5. Sort the search results by **Log Time** in reverse order as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4128f6a9671cea21d99e25c1daf812d9.png)
As shown above, the event shows that the node scale-out occurred at `2020-11-25 20:35:45`, which was triggered by three Nginx Pods (`nginx-5dbf784b68-tq8rd`, `nginx-5dbf784b68-fpvbx`, and `nginx-5dbf784b68-v9jv5`). As a result, three nodes were added, and further scale-out was not triggered as the maximum number of nodes was reached in the node pool.  
