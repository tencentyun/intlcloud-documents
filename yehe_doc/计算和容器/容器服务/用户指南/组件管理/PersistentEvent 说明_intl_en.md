## Overview


<dx-alert infotype="alarm" title="">
This add-on will not be updated. If you want to use the event storage feature, please refer to [Event Storage](https://intl.cloud.tencent.com/document/product/457/30686).
</dx-alert>




### Add-on description

Kubernetes Events contains information about the operations of Kubernetes clusters and the scheduling of various resources, which can help OPS personnel monitor daily changes in resources and locate problems. TKE supports event persistence for all clusters. After enabling this feature, your cluster events will be exported to the configured storage in real time. TKE also supports the search of event flows by using PAAS services provided by Tencent Cloud or open-source software tools.


### Kubernetes objects deployed in a cluster


| Kubernetes Object | Type | Required Resources | Namespaces |
| -------------------- | ---------- | --------------- | ------------ |
| tke-persistent-event | deployment | 0.2 core CPU, 100MB memory | kube-system |

## Use Cases

Kubernetes Events are records generated for resource lifecycle, resource scheduling, and exception alerts. These events give insight into what is happening inside the cluster. For example, they can shed light on a decision made by a scheduler or analyze why certain pods are evicted from a node.

Kubernetes only retains Kubernetes Events for one hour by default. PersistentEvent provides a feature that can store Kubernetes Events persistently and allows you to store cluster events to your personal storage.

## Limits
- Installing PersistentEvent consumes cluster resources of 0.2 core CPU and 100 MB memory.
- Supports clusters with Kubernetes version 1.8 and later.

## Usage

### Installing and configuring the storage location
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. At the top of the "Cluster Management" page, select the ID of the target cluster under its region to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. On the "Add-On List" page, click **Create**. On the "Create Add-On" page that appears, select **PersistentEvent**, configure the event persistence storage location, and click **Confirm** to complete installation.
The main parameters are described as follows:
 - **Storage Selection**: you can choose to store events to **[Elasticsearch](https://intl.cloud.tencent.com/document/product/845/16478)** or **[Tencent Cloud CLS](https://intl.cloud.tencent.com/document/product/614/11254)**.
 - **Parameter details**:
	 - To store events to **Elasticsearch**, you need to provide the Elasticsearch address and index.
	 - To store events to **Tencent Cloud CLS**, you need to provide a CLS instance. If no suitable instance is available, you can [create a log topic](https://console.cloud.tencent.com/cls/topic?region=ap-guangzhou).



### Searching for the event in the CLS console
Log in to the CLS console and select **[Log Search](https://console.cloud.tencent.com/cls/search)** in the left sidebar. Select the log service configured by PersistentEvent in the **Logset** and **Log Topic** drop-down lists, as well as the time period for which to search logs, and click **Search and Analysis** to view the event data, as shown in the following figure:
![](https://main.qcloudimg.com/raw/348f807a187842b773a200c986185012.png)



>!You need to enable the full-text index for the log topic to search for the logs.

