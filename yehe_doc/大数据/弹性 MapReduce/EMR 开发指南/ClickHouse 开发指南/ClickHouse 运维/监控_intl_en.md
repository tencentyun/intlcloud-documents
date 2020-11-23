Tencent Cloud EMR provides a complete monitoring system for the ClickHouse cluster, which consists of **cluster overview**, **service monitoring**, and **server monitoring**.

## Cluster Overview

The cluster overview page displays the overview information of the ClickHouse cluster, such as the cluster running status, number of servers, and ZooKeeper status.

In addition, it displays the aggregate service and server metric information by cluster, so that you can intuitively view the overall cluster running status.
- Service monitoring has four aggregate metrics, namely, number of queries, number of active data blocks, size of operation queue, and number of network connections. The aggregate graph on the cluster overview page displays the sum of the corresponding metric values of all servers in the ClickHouse cluster.
- Server monitoring has four aggregate metrics, namely, CPU utilization, memory utilization, disk utilization, and network traffic. The aggregate graph on the cluster overview page displays the overall server resource usage in the ClickHouse cluster.

![](https://main.qcloudimg.com/raw/522491dc5b6f999bf617141e7c3ddfd5.png)                          

- The deployment status section provides real-time monitoring on the cluster process status. If a process is missing, it will be promptly displayed on the monitoring page.
- In the server status section, you can view the top 10 servers with the highest resource usage in the last 7 days, so that you can quickly locate the servers where the cluster bottleneck exists.

 In addition, you can click **Server Metric Comparison** to compare the resource usage in a time period between multiple servers.
![](https://main.qcloudimg.com/raw/3823b4734519117cbb39c5f8a542f4b1.png)


## Service Monitoring

ClickHouse cluster service monitoring is simple, as the services include only ClickHouse and ZooKeeper (for HA clusters). In the role list on the service monitoring page, you can view basic information of roles. ZooKeeper has only one role (`Zookeeper`), and ClickHouse also has only one role (`ClickHouse-Server`). You can enter the server monitoring page of a server in the node IP section.

Under a specific role, you can view its detailed service monitoring data in a time period up to the last 30 days and at a desired time granularity. In addition, you can select the metrics to be displayed. Click **Set Metric** and you can view all the monitoring metrics of the role, all of which can also be previewed. You can check the needed metrics to display them by default. Currently, up to 12 metrics can be displayed.
![](https://main.qcloudimg.com/raw/d28330a6d44c7aea35054601e7ee578d.png)
Here, ClickHouse monitoring metrics can be divided into three groups, which come from three ClickHouse system tables `metrics`, `events`, and `asynchronous_metrics`, respectively.

## Server Monitoring

Server monitoring divides into server monitoring overview page and server monitoring details page.

### Server monitoring overview page

The server monitoring overview page displays the server monitoring metrics of the cluster. Currently, 12 aggregate metrics in four dimensions of CPU, memory, disk, and network are provided to show the overall server resource usage in the cluster. Similar to service monitoring, you can set the aggregate metrics to be displayed in **Set Metric**.
![](https://main.qcloudimg.com/raw/9bae314630bbe124b61e106e6c30a8dd.png)
In addition, server monitoring provides the heat map feature that shows each server's load concerning a server metric in the specified time period. Taking memory utilization as an example, the curve above shows the memory utilization of the cluster. In the load distribution section, each small square represents a server, and the color represents the server utilization range. The deeper the color, the higher the memory utilization. Statistics are displayed in descending order, and top 3 servers with the highest memory utilization are displayed by default, making it easy for you to find the differences between servers.
![](https://main.qcloudimg.com/raw/601d6d0158bc8e1cc0925794c9e92077.png)
The monitoring overview page also displays the list of all nodes in the cluster. You can filter the nodes by type, search for them by IP, or sort and display them by CPU, memory, and disk utilization. You can click the IP of a node to enter its server monitoring details page.
![](https://main.qcloudimg.com/raw/7cf962d881c423844dafedd7b7475aa8.png)

### Server monitoring details page

The server monitoring details page consists of four sections: basic configuration, deployment status, load status, and server monitoring.

- The basic configuration section displays the basic hardware information of the server. Specifically, it provides a disk list to show the server's disk information. If a disk name and disk mount point change, the change will be perceived in 30 minutes. You can click the name of a disk to view its monitoring metrics.
![](https://main.qcloudimg.com/raw/dffe3b4ba8aeabe64d4bdec8fdc077b6.png)
- The deployment status section displays the real-time status of processes of services deployed on the server, helping you monitor the server processes.
- The load status section displays the server snapshot information at a certain time point, including the CPU, memory, IO, and network usage of processes and list of processes on the server, through which you can view the server snapshot at the target time point.
![](https://main.qcloudimg.com/raw/7de190a8e61b8a5757e64d46b416790a.png)
- The server monitoring section displays the status of specific monitoring metrics of the server. The metrics cover various aspects such as CPU, memory, file handle, disk, network, and process. Similar to service monitoring, you can set the metrics to be displayed.


## Summary

The complete ClickHouse cluster monitoring system is constructed by integrating cluster overview, service monitoring, and server monitoring, which greatly facilitates ClickHouse cluster OPS.
