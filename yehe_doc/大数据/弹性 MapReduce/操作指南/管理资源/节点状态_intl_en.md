## Feature Overview
The server status page displays the monitoring overview of all servers in the current cluster and the list of all nodes. It supports viewing heat maps of all servers. You can manage the status and metric information of servers in the EMR Console during daily use.
## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster List**, and click the ID/Name of the target cluster to enter the cluster details page.
2. Select **Cluster Resources** > **Server Status** to view the monitoring information of all servers in the cluster.
3. In server monitoring, you can view an aggregated overview of monitoring metrics of all servers in the current cluster and the list of all nodes.
![](https://main.qcloudimg.com/raw/7f8569a5f4a75b6f44859a3b56b55283.png)
 - **Overview** intuitively displays the aggregated metrics and their statistical rules of all servers in the corresponding time period. The system displays a maximum of 6 metrics by default. You can click "Set Metric" to customize the displayed metrics.
![](https://main.qcloudimg.com/raw/1cff3fb7d4b6fb87745db3e015d24588.png)
 - **Heatmap** more intuitively displays the loads of servers and supports viewing by specified time range and load condition. The load heatmap mainly divides into two parts. The first part contains an aggregated load map of all servers in the current cluster, while the second part contains individual heatmaps of each nodes where you can visually view the load of all nodes.
![](https://main.qcloudimg.com/raw/6480cb463f2b73057f74d3b70cfc871e.png)
 - **Node List** displays the deployed node type, CPU utilization, memory utilization, and disk utilization of all current nodes. Click a node IP to view the basic configuration, deployment status, load status, server monitoring, and other metrics of one single node.
        - Basic Configuration: it displays the basic information of the current server, such as the node type, instance ID, resource ID, billing mode, and specification.
![](https://main.qcloudimg.com/raw/2d4938f79086e7e767a85acd148b20b3.png)
        - Deployment Status: it displays the deployment status of services on the current server, such as whether the processes are standard ones and whether they are running properly.
![](https://main.qcloudimg.com/raw/d7d2746efe442d64e8bbf74ab45a024c.png)
        - Load Status: it displays the top N processes with the highest load on the current server. You can specify a time to view the load status.
![](https://main.qcloudimg.com/raw/dc6ce906148b1ceb3f1763197f2059cf.png)
       - Server Monitoring: it displays the load trend of each metric group of the current server. 6 metrics are displayed by default, and up to 12 metrics can be displayed. You can click **Set Metric** to customize the displayed metrics.
![](https://main.qcloudimg.com/raw/d1660300a091c465ee47114eb9fc52fe.png)
