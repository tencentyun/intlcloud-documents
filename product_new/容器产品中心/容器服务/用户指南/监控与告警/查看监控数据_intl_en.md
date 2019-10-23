## Operation Scenario

Tencent Cloud TKE provides basic monitoring features to all clusters by default. Use the steps below to view TKE monitoring data.
- [Cluster Metrics](#check1)
- [Node Metrics](#check2)
- [Pod Metrics on the Node](#check3)
- [Viewing Workload Metrics](#check4)
- [Viewing Pod Metrics in a Workload](#check5)
- [Viewing Container Metrics in a Pod](#check6)

## Prerequisites
Log into TKE console and open **[Cluster Management](https://console.cloud.tencent.com/tke2/cluster?rid=1)** page.

## Steps

<span id="check1"></span>
### Viewing Cluster Metrics
Click <img src="https://main.qcloudimg.com/raw/fef90a2f69f50758b30e4c4b5e0bc7de.png" style="margin-bottom: -2px;;"></img> in the row of the cluster for which you want to view the monitoring data. You will see that cluster’s monitoring information as shown in the figure below:
![](https://main.qcloudimg.com/raw/444d1c462cf681ec7456229b25373c3a.png)

<span id="check2"></span>
### Viewing Node Metrics
Use the steps below to view monitoring information for nodes and Master & Etcd nodes.
1. Select the ID/name of the cluster you want to view to go to the cluster management page.
2. Expand **Node Management** to view monitoring information for ordinary nodes and Master & Etcd nodes.
 - Select **Node** > **Monitoring** to go to the **Node Monitoring** page and view the monitoring information. See the figure below:
![](https://main.qcloudimg.com/raw/c1c1fca1e108f8479b50a895c2d2d0b5.png)
 - Select **Master & Etcd** > **Monitoring** to go to the **Master & Etcd Monitoring** page and view the monitoring information. See the figure below:
![](https://main.qcloudimg.com/raw/b178510aaf43b2907d64835d7384a5b1.png)

<span id="check3"></span>
### Viewing Metrics of Pods in a Node
You can use either of the two methods below to view the metrics of pods in a node.
1. Select the ID/name of the cluster you want to view to go to the cluster management page.
2. Select **Node Management** > **Node** to go to the node list page.
3. Select the method for viewing the metrics of pods in the node based on your needs.
 - Viewing Pod Metrics from the Node List
    1. Click **Monitoring** to go to the **Node Monitoring** page.
    2. Click **Pod** and select **Node** as the node you want to view. This will allow you to view a plot of the monitored metrics for the pods on that node. See the figure below:
![](https://main.qcloudimg.com/raw/e58301ce2675d2de018a867c31fcfb69.png)
 - Viewing Pod Metrics from the Node Details Page
    1. Select the ID/name of the node you want to view to go to the node management page.
    2. Select the **Pod Management** tab and click **Monitoring** to view a plot of the monitored metrics for the pods on that node. See the figure below:
![](https://main.qcloudimg.com/raw/269631374cbe8ff955de4d691c53772c.png)

<span id="check4"></span>
### Viewing Workload Metrics
1. Select the ID/name of the cluster you want to view to go to the cluster management page.
2. Select **Workload** > **Any Workload Type**. For example, select **Deployment** to go to the deployment management page.
3. Click **Monitoring** to view the workload monitoring information. See the figure below:
![](https://main.qcloudimg.com/raw/392b8235bb98367b50bc4b20e6ad3118.png)

<span id="target"></span><span id="check5"></span>
### Viewing Metrics of Pods in a Workload
<span id="first"></span>
1. Select the ID/name of the cluster you want to view to go to the cluster management page.
2. Select **Workload** > **Any Workload Type**. For example, select **Deployment** to go to the deployment management page.
3. Select the name of the workload you want to view to go to the workload management page. <span id="third"></span>
4. Select the **Pod Management** tab and click **Monitoring** to view a plot of the monitored metrics for the pods in that workload. See the figure below:
![](https://main.qcloudimg.com/raw/bda91f0b0fb55cf87cf7258cc471ae1f.png)

<span id="check6"></span>
### Viewing Metrics of Containers in a Pod
1. Refer to [step 1](#first) to [step 3](#third) of [Viewing Pod Metrics in a Workload](#target) to go to the workload details page.
2. Select the **Pod Management** tab and click **Monitoring** to go to the **Pod Monitoring** page.
3. Click **Container** and select **Pod** as the pod you want to view. This will allow you to view a plot of the monitored metrics for the containers in that pod. See the figure below:
![](https://main.qcloudimg.com/raw/28b567cd6eda684fbd0076d89bdadd76.png)


