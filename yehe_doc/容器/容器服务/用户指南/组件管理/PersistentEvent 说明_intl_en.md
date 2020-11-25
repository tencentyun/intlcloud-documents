## Overview

### Add-on description

Kubernetes Events contains information on the operations of Kubernetes clusters and the scheduling of various resources, which can help OPS personnel observe daily changes in resources and locate problems. TKE supports event persistence for all clusters. After this feature is enabled, cluster events will be exported to the configured storage in real time. TKE also supports the searching of event flows by using PAAS services provided by Tencent Cloud or by using open-source software tools.


## Kubernetes Objects Deployed in a Cluster


| Kubernetes Object Name | Type | Default Resource Consumption | Namespaces |
| -------------------- | ---------- | --------------- | ------------ |
| tke-persistent-event | deployment | 0.2-core CPU and 100-MB memory | kube-system |

## Use Cases

Kubernetes Events are records generated for resource lifecycle, resource scheduling, and exception alerts. These events give insight into what is happening inside the cluster. For example, they can shed light on a decision made by a scheduler or analyze why certain pods are evicted from a node.

Kubernetes only retains Kubernetes Events for one hour by default. PersistentEvent provides a feature that can store Kubernetes Events persistently and allows you to store cluster events to your personal storage.

## Limits
- Installing PersistentEvent consumes cluster resources of 0.2-core CPU and 100-MB memory.
- Supports clusters with Kubernetes version 1.8 and later.

## Usage

### Installing and configuring the storage location
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. At the top of the "Cluster Management" page, select the ID of the target cluster under its region to go to the cluster details page.
3. In the left sidebar, click **Add-On Management** to go to the "Add-On List" page.
4. On the "Add-On List" page, click **Create**. On the "Create an Add-On" page that appears, select **PersistentEvent**, configure the event persistence storage location, and click **Finish** to complete installation.
Main parameters are described as follows:
 - **Storage Location**: you can choose to store events to **[Elasticsearch](https://intl.cloud.tencent.com/document/product/845/16478)** or **[CLS](https://intl.cloud.tencent.com/document/product/614/11254)**.
 - **Parameter details**:
	 - To store events to **Elasticsearch**, you need to provide the Elasticsearch address and index.
	 - To store events to **CLS**, you need to provide a CLS instance. If no suitable instance is available, you can create a logset by referring to [Creating Logsets](https://console.cloud.tencent.com/cls/logset).



### Searching for events in the CLS console
1. Log in to the CLS console and select **[Logset Management](https://console.cloud.tencent.com/cls/logset)** in the left sidebar.
2. On the top of the **Logset Management** page, select the region of the logset configured by PersistentEvent.
3. In the logset list, click the name of the logset configured by PersistentEvent to go to the logset details page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/e8c357efec0bf528521d8ee9f6d9d753.png)
4. Click **Manage** for the logset configured by PersistentEvent to go to the **Log Topic** details page.
5. Click the **Search Configuration** tab page. On this page, enable index configuration and click **Save** to enable the log indexing feature, as shown in the figure below:
![](https://main.qcloudimg.com/raw/0ac7b395a3250e8d21f2fd5022d8ddf0.png)
6. Select **[Log Index](https://console.cloud.tencent.com/cls/search)** in the left sidebar. Then, select the log service configured by PersistentEvent in the **Logset** and **Log Topic** drop-down lists, select the period for which to search for logs, and click **Query Analysis** to view event data, as shown in the figure below:
![](https://main.qcloudimg.com/raw/348f807a187842b773a200c986185012.png)

