## Overview

Tencent Cloud TKE provides basic monitoring features to all clusters by default. Use the steps below to view TKE monitoring data.
- [Cluster Metrics](#check1)
- [Node Metrics](#check2)
- [Pod Metrics on the Node](#check3)
- [Viewing Workload Metrics](#check4)
- [Viewing Pod Metrics in a Workload](#check5)
- [Viewing Container Metrics in a Pod](#check6)

## Prerequisites
Log in to TKE console and open the **[cluster management](https://console.cloud.tencent.com/tke2/cluster?rid=1)** page.

## Directions

[](id:check1)
### Viewing Cluster Metrics
Click <img src="https://main.qcloudimg.com/raw/fef90a2f69f50758b30e4c4b5e0bc7de.png" style="margin-bottom: -2px;;"></img> in the row of the cluster for which you want to view the monitoring data. You will see that cluster’s monitoring information as shown in the figure below:
![](https://main.qcloudimg.com/raw/444d1c462cf681ec7456229b25373c3a.png)

[](id:check2)
### Viewing Node Metrics
Use the steps below to view monitoring information for nodes and Master & Etcd nodes.
1. Click the ID/name of the target cluster to go to the cluster management page.
2. Expand **Node Management** to view monitoring information for ordinary nodes and Master & Etcd nodes.
 - Select **Node** > **Monitor** to go to the **Node Monitoring** page and view the monitoring information. See the figure below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EPbK891_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206162908.png)
 - Select **Master & Etcd** > **Monitoring** to go to the **Master & Etcd Monitoring** page and view the monitoring information. See the figure below:
![](https://main.qcloudimg.com/raw/b178510aaf43b2907d64835d7384a5b1.png)

[](id:check3)
### Viewing Metrics of Pods in a Node
1. Click the ID/name of the target cluster to go to the cluster management page.
2. Select **Node Management** > **Node** to go to the node list page.
3. Click a node name, click the **Pod Management** tab, and click **Monitor** to view the curve chart of the monitored metrics for the pods on that node. See the figure below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WeGI357_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206163502.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Rfbs680_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206163616.png)

[](id:check4)
### Viewing Workload Metrics
1. Click the ID/name of the target cluster to go to the cluster management page.
2. Select **Workload** > Any workload type. In this example, **Deployment** is selected.
3. Click **Monitoring** to view the workload monitoring information.
![](https://main.qcloudimg.com/raw/392b8235bb98367b50bc4b20e6ad3118.png)

[](id:check5)
### Viewing Metrics of Pods in a Workload
1. Select the ID/name of the cluster you want to view to go to the cluster management page.
2. Select **Workload** > Any workload type. In this example, **Deployment** is selected.
3. Click a workload name. On the **Pod management** tab of the workload, click **Monitor** to view the comparison charts of the monitored metrics of all Pods of the workload.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/nhMM324_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206164052.png)


[](id:check6)
### Viewing Metrics of Containers in a Pod

1. Click the ID/name of the target cluster to go to the cluster management page.
2. Select **Workload** > Any workload type. In this example, **Deployment** is selected.
3. Click a workload name. On the **Pod management** tab of the workload, click ![](https://qcloudimg.tencent-cloud.cn/raw/73074e1d0fd941c5dcdfa52ed415195a.png) on the left of the instance name to view the container information of the Pod.
4. Click ![](https://qcloudimg.tencent-cloud.cn/raw/1655cff483b7ec789d487e17dd54b12c.png) to view the comparison charts of the monitored metrics of the containers in the Pod.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/whLQ650_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230206164130.png)

 
