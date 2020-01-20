## Overview

### Add-on description

Kubernetes Events contains information about the operations of Kubernetes clusters and the scheduling of various resources, which can help Ops personnel observe daily changes in resources and locate problems. TKE supports event persistence for all your clusters. After this feature is enabled, your cluster events will be exported to the configured storage in real time. TKE also supports the searching of event flows using PaaS services provided by Tencent Cloud or open-source software tools.


### Kubernetes objects deployed in a cluster

Deploying PersistentEvent Add-on in a cluster will deploy the following Kubernetes objects in the cluster:

| Kubernetes Object Name             | Type                       | Default Resource Occupation | Namespaces |
| -------------------- | ---------- | --------------- | ------------ |
| tke-persistent-event | deployment | 0.2 core CPU, 100MB memory | kube-system  |

## Use Cases

Kubernetes Events are records generated for resource lifecycle, resource scheduling, and exception alerts. Events can be used to give insight into what is happening inside the cluster. For example, they can shed light on a decision made by a scheduler or can offer an analysis of why certain Pods are evicted from a node.

Kubernetes only retains Kubernetes Events for one hour by default. PersistentEvent provides a feature that can store Kubernetes Events persistently. It allows you to use PersistentEvent to save cluster events to your personal storage side.

## Limits
- Installing PersistentEvent occupies cluster resources of 0.2 core CPU and 100MB memory.
- Supports clusters with Kubernetes version 1.8 and above.

## Usage

### Installing and configuring the storage location
1. Log in to the [TKE Console](https://console.qcloud.com/tke2), and select **Add-ons** in the left sidebar.
2. On the top of the **Add-ons** management page, select the region and the cluster for installing PersistentEvent, and click **Create**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/672f9156620c9643ffb7baa4ec1e1d27.png)
3. In the **Create Add-on** page, select **PersistentEvent**, configure the persistent storage side, and click **Complete** to install it.
PersistentEvent supports two storage options, [Elasticsearch](https://intl.cloud.tencent.com/document/product/845/16478) and [CLS](https://intl.cloud.tencent.com/document/product/614/11254). It is recommended that you use CLS. You can choose which to use according to your actual circumstances. This document uses CLS as an example.




### Updating the storage location
1. Log in to the [TKE Console](https://console.qcloud.com/tke2), and select **Add-ons** in the left sidebar.
2. On the top of the **Add-on** page, select the region with the cluster whose PersistentEvent you want to update, and click **Update Configurations** on the right. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/cde73e9c1c54d943045bb7e0f538d47a.png)
3. In the **Update PersistentEvent** page, adjust the storage location for events, and click **Complete** to finish updating configurations.

### Searching events in the CLS Console
1. Log in to the CLS Console, and select **[Logset Management](https://console.cloud.tencent.com/cls/logset)** in the left sidebar.
2. On the top of the **Logset Management** page, select the domain of the logset configured by PersistentEvent.
3. In the logset list, click the name of the logset configured by PersistentEvent to go to the logset details page. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/be97c45c1b40311a49d5ce8514143965.png)
4. Click **Manage** on the right of row containing the logset configured by PersistentEvent to go to the **Log Topic** details page.
5. Select the **Search Configuration** tab page. On the page, enable the index configuration and click **Save** to turn on the log indexing feature. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/bb30c2912f760ee81e70170412373332.png)
6. Select **[Log Index](https://console.cloud.tencent.com/cls/search)** in the left sidebar, and select the log service configured by PersistentEvent in the **Logset** and **Log Topic** drop-down lists, as well as the time period for which to search logs, and click **Query Analysis** to view the event data. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/490b164af5d62d345eb7436a852bfd64.png)

