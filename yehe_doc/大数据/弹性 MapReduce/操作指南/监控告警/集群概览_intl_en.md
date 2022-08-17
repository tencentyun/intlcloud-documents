## Feature overview
Cluster overview displays a summary of cluster operation status, where you can view the cluster operation status, core service metrics, core node metrics, and top 10 nodes.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Monitor** > **Cluster Overview** to view the overall status of the current cluster. The **Cluster Overview** page provides four monitoring views in the cluster dimension, namely, overall status of cluster, key cluster metrics, cluster deployment status, and top 10 nodes.
 - Overall cluster conditions: This view displays the current cluster status, node quantity, metadatabase online status, component health status, and events in the cluster within one hour.
 ![](https://main.qcloudimg.com/raw/6da2026aaa2630e908ac95b290e83486.png)
 - Key cluster metrics: This view displays the total utilization of HDFS, YARN, CPU, memory, and disk as well as total network traffic of the current cluster. You can click **View Trend** in the top-right corner of each metric and select a target time period to view the corresponding usage trend.
![](https://main.qcloudimg.com/raw/b9819f9bedb364b8f6de0f441b1c34f7.png)
![](https://main.qcloudimg.com/raw/a475fbc3b109a66058f3651b9e5c92d8.png)
 - Cluster deployment status: This view displays abnormal, missing, and invalid processes deployed on nodes and the number of nodes in the current cluster, so that you can correct the configuration accordingly.
![](https://main.qcloudimg.com/raw/62124d7eb6014282351ab70d76a45851.png)
 - Top 10 nodes: This view displays the trend of node loads in the current cluster under core metrics. You can select multiple nodes to compare their load trends under the same metric.
![](https://main.qcloudimg.com/raw/191047bc304323356ddf2b203a0597c5.png)
![](https://main.qcloudimg.com/raw/6b4bf84a00ad58508cfc3c470e906162.png)
