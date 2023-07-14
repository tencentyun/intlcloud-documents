## Overview
The **Node status** page displays the monitoring overview and list of all nodes in the current cluster. It enables you to view heat maps of all nodes. You can manage the status information and metrics of nodes in the EMR console.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. Select **Cluster resources > Node status** to view the monitoring information of all nodes in the cluster.
3. On the **Node status** page, view aggregated monitoring metrics and list of all nodes in the cluster.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/euSN626_%E5%9B%BD%E9%99%8581.png)
 - **Overview**: Displays aggregated monitoring metrics of all nodes during a specified period of time and the statistical rule of each metric. You can click **Set metrics** to customize the displayed metrics.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/gcCp483_%E5%9B%BD%E9%99%8582.png)
 - **Heat map**: Displays the loads of nodes. You can view the maps for a specified period of time and under specified load conditions. Load heat maps consist of two parts: the aggregated map of all nodes in the current cluster and individual heat map of each node.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/BxSx969_%E5%9B%BD%E9%99%8583.png)
 - **Node list**: Displays all nodes in the cluster, including type, CPU utilization, memory utilization, disk utilization, and other items. You can click the IP of a node to view its basic configurations, deployment status, load status, and monitoring information.
        - Basic configurations: Display basic information of the node, such as type, resource name, resource ID, billing mode, and spec.
     ![](https://staticintl.cloudcachetci.com/yehe/backend-news/iTWa237_%E5%9B%BD%E9%99%8584.png)
        - Deployment status: Display services deployed in the node, process type, and process status.
     ![](https://staticintl.cloudcachetci.com/yehe/backend-news/y7JN099_%E5%9B%BD%E9%99%8585.png)
        - Load status: Displays top N processes in the node. You can view the data on a specified date.
     ![](https://staticintl.cloudcachetci.com/yehe/backend-news/Bp4g364_%E5%9B%BD%E9%99%8586.png)
       - Node monitoring: Displays load maps of metrics (6 by default and max 12) of the node. You can click **Set metrics** to customize the displayed metrics.
     ![](https://staticintl.cloudcachetci.com/yehe/backend-news/XVKg491_%E5%9B%BD%E9%99%8587.png)
