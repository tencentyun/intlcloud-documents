Tencent Cloud Elastic MapReduce (EMR) provides a complete monitoring system for ClickHouse clusters. The system is divided into three dimensions: **Cluster Overview**, **Service Monitoring**, and **Node Monitoring**.

## Cluster Overview
The cluster overview page displays the overview information of a ClickHouse cluster, such as the running status, number of nodes, and Zookeeper status. This page also shows service metrics and node metrics in the cluster dimension, allowing you to see the overall running status of the cluster visually.

- The service monitoring section has four aggregate metrics: the number of queries, number of active data blocks, size of the operation queue, and number of network connections. The graphs on the cluster overview page show the aggregate of the corresponding metrics for all nodes in the ClickHouse cluster.
- The node monitoring section also has four aggregate metrics: CPU utilization, memory utilization, disk utilization, and network traffic. The graphs on the cluster overview page show the overall usage of the node resources in the ClickHouse cluster.
![](https://main.qcloudimg.com/raw/fa120a13b19128b865aabaeda8009f52.png)                    
- The deployment status section provides real-time monitoring on the cluster process status. If a process is missing, it will be immediately displayed on this page.
- In the node status section, you can view the resource usage of the 10 most used machines for the last seven days to quickly locate the cluster bottleneck.

 You can also click **Node Metric Comparison** to compare the resource usage of multiple nodes during a certain period of time.
![](https://main.qcloudimg.com/raw/572fb6dd5cc20e7c8f92e01e4b949712.png)


## Service Monitoring

The cluster service monitoring of ClickHouse is relatively simple, only consisting of ClickHouse and Zookeeper (if it is an HA cluster). You can see the basic information of the roles in the role list on the service monitoring page. Both Zookeeper and ClickHouse have only one role named Zookeeper and ClickHouse-Server, respectively. You can go to the monitoring page of a specific node from the node IP column.

On the monitoring page of a specific node, you can view the detailed data for up to 30 days, and you can select the time period as needed. Moreover, you can customize the metrics to be displayed by clicking **Set Metrics** and selecting those that you want. Currently, up to 12 metrics can be displayed at a time.
![](https://main.qcloudimg.com/raw/676baba2f25ef75cc7ecc21a96c4a60c.png)
The monitoring metrics of ClickHouse are divided into three groups, which come from the three system tables of ClickHouse: metrics, events, and asynchronous_metrics.

## Node Monitoring

Node monitoring consists of the monitoring overview page and the monitoring details page.

### Monitoring overview
The monitoring overview page displays the aggregate monitoring metrics of the nodes in the cluster. Currently, it provides 12 aggregate metrics in dimensions such as the CPU, memory, disk, and network, reflecting the overall resource utilization of the nodes in the cluster. Like service monitoring, you can select the metrics to be displayed by clicking **Set Metrics**.
![](https://main.qcloudimg.com/raw/a42b77cf113fec80d3d06c39bb6bc407.png)
Node monitoring also provides heat maps that allow you to view the load of each machine in terms of a certain node metric during a certain period of time. For example, the curve on a heap map shows the aggregate memory utilization in the cluster dimension. In load distribution, each small square represents a node, and different colors indicate that the memory utilization of different nodes is in different categories. The darker the color, the higher the memory utilization. Load distribution is displayed in descending order by default and the memory utilization of the top 3 nodes is displayed by default, making it convenient to compare the differences between machines.
![](https://main.qcloudimg.com/raw/ee0aa95b0f21119230b3340867f3889c.png)
The node monitoring overview page also has a list of all nodes in the cluster. You can filter by node type, search by IP, or sort and display by CPU utilization, memory utilization, or disk utilization. Click a node IP to go to the node monitoring details page of the specific machine.
![](https://main.qcloudimg.com/raw/72d0a423ab84ebde4e00ce8e47500c76.png)

### Monitoring details

The monitoring details page consists of four sections: basic configuration, deployment status, load status, and node monitoring.

- Basic configuration displays the basic hardware information and a disk list showing the disk information of the node. If the disk name or mount point is changed, it will be detected within 30 minutes. You can view the monitoring metrics of a disk by clicking the disk name.
  ![](https://main.qcloudimg.com/raw/9f484a9eb7885467e0feb3ad403298a5.png)

- Deployment status shows the real-time status of the deployment service processes of the node, making it convenient to monitor the machine processes.

- Load status shows the snapshot information of the machine at a certain time, including the CPU utilization, memory utilization, IO, and network condition of the processes. You can also see the process list of the machine at a certain time.
  ![](https://main.qcloudimg.com/raw/7de190a8e61b8a5757e64d46b416790a.png)

- Node monitoring shows the specific monitoring metrics of the node, including the CPU, memory, file handle, disk, network, process, and more. Like service monitoring, you can select the metrics to be displayed.

  ![](https://main.qcloudimg.com/raw/3c990c526b1c997253f18616a0c49f49.png)


## Summary

**Cluster Overview**, **Service Monitoring**, and **Node Monitoring** together form a complete monitoring system for ClickHouse clusters, which is very helpful for the OPS of ClickHOuse clusters.
