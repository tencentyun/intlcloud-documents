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
![](https://main.qcloudimg.com/raw/e11cc5383d01d4a5d0df10fc20e9f8f4.png)

<span id="check2"></span>
### Viewing Node Metrics
Use the steps below to view monitoring information for nodes and Master & Etcd nodes.
1. Select the ID/name of the cluster you want to view to go to the cluster management page.
2. Expand **Node Management** to view monitoring information for ordinary nodes and Master & Etcd nodes.
 - Select **Node** > **Monitoring** to go to the **Node Monitoring** page and view the monitoring information. See the figure below:
![](https://main.qcloudimg.com/raw/a3d3c1c07c80c0b2424ae986ce906e88.png)
 - Select **Master & Etcd** > **Monitoring** to go to the **Master & Etcd Monitoring** page and view the monitoring information. See the figure below:
![](https://main.qcloudimg.com/raw/c4b201bad3d329168948781841995303.png)

<span id="check3"></span>
### Viewing Metrics of Pods in a Node
You can use either of the two methods below to view the metrics of pods in a node.
1. Select the ID/name of the cluster you want to view to go to the cluster management page.
2. Select **Node Management** > **Node** to go to the node list page.
3. Select the method for viewing the metrics of pods in the node based on your needs.
 - Viewing Pod Metrics from the Node List
    1. Click **Monitoring** to go to the **Node Monitoring** page.
    2. Click **Pod** and select **Node** as the node you want to view. This will allow you to view a plot of the monitored metrics for the pods on that node. See the figure below:
![](https://main.qcloudimg.com/raw/3d347a95e79587da1a44bc39015f540f.png)
 - Viewing Pod Metrics from the Node Details Page
    1. Select the ID/name of the node you want to view to go to the node management page.
    2. Select the **Pod Management** tab and click **Monitoring** to view a plot of the monitored metrics for the pods on that node. See the figure below:
![](https://main.qcloudimg.com/raw/a5c09c957533a5dd25377ba61bc2d352.png)

<span id="check4"></span>
### Viewing Workload Metrics
1. Select the ID/name of the cluster you want to view to go to the cluster management page.
2. Select **Workload** > **Any Workload Type**. For example, select **Deployment** to go to the deployment management page.
3. Click **Monitoring** to view the workload monitoring information. See the figure below:
![](https://main.qcloudimg.com/raw/9776454078edf627d4dfbd5c368c0221.png)

<span id="target"></span><span id="check5"></span>
### Viewing Metrics of Pods in a Workload
<span id="first"></span>
1. Select the ID/name of the cluster you want to view to go to the cluster management page.
2. Select **Workload** > **Any Workload Type**. For example, select **Deployment** to go to the deployment management page.
3. Select the name of the workload you want to view to go to the workload management page. <span id="third"></span>
4. Select the **Pod Management** tab and click **Monitoring** to view a plot of the monitored metrics for the pods in that workload. See the figure below:
![](https://main.qcloudimg.com/raw/551e7e912946c9c4725831c1f38c2e85.png)

<span id="check6"></span>
### Viewing Metrics of Containers in a Pod
1. Refer to [step 1](#first) to [step 3](#third) of [Viewing Pod Metrics in a Workload](#target) to go to the workload details page.
2. Select the **Pod Management** tab and click **Monitoring** to go to the **Pod Monitoring** page.
3. Click **Container** and select **Pod** as the pod you want to view. This will allow you to view a plot of the monitored metrics for the containers in that pod. See the figure below:
![](https://main.qcloudimg.com/raw/efa8ba01a1ab983d7d0182d7e238a006.png)


