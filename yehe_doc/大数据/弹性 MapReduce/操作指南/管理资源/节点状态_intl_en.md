## Feature Overview
The "Node Status" page displays the monitoring overview of all nodes in the current cluster and the list of all nodes. It supports viewing heat maps of all nodes. During daily use, you can log in to the Elastic MapReduce Console to manage the status and metric information of nodes.
## Directions
1. Log in to the [Elastic MapReduce Console](https://console.cloud.tencent.com/emr) and click the **ID/name** of the target cluster in **Cluster List** to enter the cluster details page.
2. Select **Cluster Resources** > **Node Status** to view the monitoring information of all nodes in the cluster.
3. In node monitoring, you can view an aggregated overview of monitoring metrics of all nodes in the current cluster and the list of all nodes.
![](https://main.qcloudimg.com/raw/745169626c6d481fa469375e6b1f1f27.png)
 - **Overview** intuitively displays the aggregated monitoring metrics and their statistical rules of all nodes in the corresponding time period. The system displays a maximum of 6 metrics by default. You can click **Set Metric** to customize the displayed metrics.
![](https://main.qcloudimg.com/raw/1cff3fb7d4b6fb87745db3e015d24588.png)
 - **Heat Map** more intuitively displays the loads of nodes and supports viewing by specified time range and load condition. The load heat map mainly divides into two parts. The first part contains an aggregated load map of all nodes in the current cluster, while the second part contains individual heat maps of each node where you can visually view the load of all nodes.
![](https://main.qcloudimg.com/raw/6480cb463f2b73057f74d3b70cfc871e.png)
 - **Node List** displays the deployed node type, CPU utilization, memory utilization, and disk utilization of all current nodes. Click a node IP to view the basic configuration, deployment status, load status, node monitoring, and other metrics of one single node.
        - Basic Configuration: it displays the basic information of the current node, such as the node type, instance ID, resource ID, billing mode, and specification.
![](https://intl.cloud.tencent.com/document/product/1026/31119)
        - Deployment Status: it displays the deployment status of services on the current node, such as whether the processes are standard ones and whether they are running properly.
![](https://main.qcloudimg.com/raw/d7d2746efe442d64e8bbf74ab45a024c.png)
        - Load Status: it displays the top N processes with the highest load on the current node. You can specify a time to view the load status.
![](https://main.qcloudimg.com/raw/dc6ce906148b1ceb3f1763197f2059cf.png)
       - Node Monitoring: it displays the load trend of each metric group of the current node. 6 metrics are displayed by default, and up to 12 metrics can be displayed. You can click **Set Metric** to customize the displayed metrics.
![](https://main.qcloudimg.com/raw/2949a56dfa4e4b9a25b26d8a75e976dc.png)
