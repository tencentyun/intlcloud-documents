Poor edge network conditions will trigger the Kubernetes eviction mechanism to evict Pods that do not meet the expectations. In edge computing scenarios where the network environments of the edge nodes and the cloud are complex, and the network quality cannot be guaranteed, problems such as API server and node disconnection tend to occur. If native Kubernetes is used without modification, the node status will often become abnormal. This causes the Kubernetes eviction mechanism to take effect, where Pods are evicted and the Endpoint is lost, thereby causing service interruption and fluctuation.  

To solve this problem, [TKE Edge](https://intl.cloud.tencent.com/document/product/457/35390) offers the innovative distributed node status determination mechanism. This mechanism can better identify the eviction timing, guarantee system running under poor network conditions, and avoid service interruption and fluctuation.  

## Use Cases

An edge use case is subject to poor network conditions in the cloud. Edge devices are located in edge cloud data centers and mobile edge sites, facing complex network environments for their cloud connectivity, such as unreliable environments at the cloud (console) and edge as well as between edge nodes.  

### Smart factory[](id:SmartFactory)

In a smart factory, edge nodes are located in the warehouse and plant, and the master node in the console is in the central data center of Tencent Cloud, as shown below:
![img](https://qcloudimg.tencent-cloud.cn/raw/84640ef52fcaa52a85b29b1d34fcebb3.png)

- The edge devices in the warehouse and plant and the cloud cluster can be connected over the internet, 5G, and Wi-Fi, with uneven and unguaranteed network quality.  
- The edge devices in the warehouse and plant are connected over the local network, which is better and more reliable than that used to connect to cloud clusters.  

### Audio/Video pull
Audio/Video pull is as shown below:
![img](https://qcloudimg.tencent-cloud.cn/raw/eabfbc0d849a7aac5cc6e6fbac2f5557.png)

Considering user experience and enterprise cost, you often need to improve the edge cache hit rate for audio/video pull to reduce the origin-pull traffic and schedule the same file requested by users to the same service instance and its cache file.  

In the case of native Kubernetes, if Pods are frequently rebuilt due to network fluctuation, the service instance caching performance will be compromised, and the scheduling system will schedule user requests to other service instances. Both may have a significant or even unacceptable impact on the CDN performance.  

In fact, if edge nodes are running normally, it is unnecessary to evict or rebuild Pods. To solve this problem and ensure the service continuity, the TKE Edge team proposed a distributed node status determination mechanism.  

## Challenges

### Native Kubernetes processing method

Poor network conditions at the cloud edge affect the communication between the kubelet running on the edge node and the cloud API server, where the latter cannot receive the kubelet heartbeat or get a renewal and then cannot accurately get the running statuses of the node and its Pods. If the duration exceeds the set threshold, the API server will consider the node unavailable and perform the following operations:

- Set the status of the missing node to `NotReady` or `Unknown` and add the taints of `NoSchedule` and `NoExecute`.  
- Evict the Pods on the missing node and rebuild them on other nodes.  
- Remove the Pods on the missing node from the Service's Endpoint list.  

## Solution

### Design principle

In edge computing, it is unreasonable to determine whether a node is normal solely based on the connection between the edge and the API server. You need an additional determination mechanism to make the system more robust.  

The network between edge nodes is more stable than that between cloud and edge nodes. You can use a more stable infrastructure to improve the accuracy. TKE Edge adopts an innovative distributed mechanism to determine the node status, which considers edge nodes in addition to the connection between nodes and the API server. Tests and practices have shown that this mechanism has improved the accuracy to determine the node status in a system under poor network conditions at the cloud edge, safeguarding service running. It works as shown below:
- Each node regularly checks the health status of other nodes.
- All nodes in the cluster regularly vote on the status of each node.
- Cloud and edge nodes determine the node status together.

First, nodes check and vote for each other to decide whether a node is in abnormal status, and the decision will be made only when most of the nodes agree on the same determination. Second, even though the network between nodes is usually in a better condition than the cloud edge network, the complex situation at the edge node should be considered, as networks are not 100% reliable. Therefore, the network between nodes is not the only standard, and the node status should be decided by both nodes and the cloud edge. In this regard, the following design is made:

| Final Node Status     | Normal to the Cloud | Abnormal to the Cloud                                                 |
| ---------------- | ------------ | ------------------------------------------------------------ |
| Normal to other nodes | Normal         | No more Pods are scheduled to this node.                                    |
| Abnormal to other nodes | Normal         | Existing Pods are evicted and removed from the Endpoint list. No more Pods are scheduled to this node. |

### Solution features    

When the cloud determines that the node status is abnormal, but other nodes consider it normal, although existing Pods will not be evicted, new Pods will not be scheduled to the node to ensure the stability of the additional services. Existing nodes will run normally thanks to the edge autonomy capability of the edge cluster.  

Due to the particularity of the edge network and topology, there are often single points of failure between node groups. In a [smart factory](#SmartFactory), although the warehouse and plant are in the same region, they are connected only through a key linkage. Once the linkage is broken, the network will be disconnected. The solution provided in this document ensures that the node group with more nodes will not be considered abnormal when two node groups are disconnected from each other. Therefore, Pods will always be scheduled to the one with more nodes, avoiding excessive node loads.  

Edge devices may be in different regions and not be connected. The solution provided in this document supports the determination of statuses of nodes in multiple regions. It allows you to easily group nodes by region or other criteria for intra-group checks. Even if nodes are regrouped, you do not need to redeploy or re-initialize detection add-ons to adapt them to the network conditions of edge computing. After grouping, nodes will only determine the statuses of nodes within their group.  


## Prerequisites

To use this feature, you need to open port 51005 of the node for distributed, smart health checks between nodes.

## Directions
>! It takes some time to deploy and configure edge and multi-region checks. They do not take effect immediately.
>
### Enabling edge health[](id:open)
**Edge Health** is disabled by default. It can be manually enabled as instructed below:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/edge?rid=1).
2. On the cluster list page, select the target edge cluster ID to enter the cluster details page.
3. Select **Basic Information** on the left sidebar to enter the **Basic Information** page.
4. On the **Basic Information** page, click **Enable Edge Health**.

### Enabling multi-region

Under **Multi-region**, nodes are grouped by region. Node regions are identified by the `tencent.tkeedgehealth/topology-zone` label on the node. For example, `tencent.tkeedgehealth/topology-zone: zone0` indicates to group the node to `zone0`. Nodes with the same label value are considered to be in the same region. After **Multi-region** is enabled, nodes in the same region will check and vote for each other.
>! 
>- If this feature is enabled without the `tencent.tkeedgehealth/topology-zone` label, the node will only check its own health status.
>- If this feature is not enabled, all nodes in a cluster will check each other, even if the node is labeled `tencent.tkeedgehealth/topology-zone`.



#### Setting node region label in the console
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/edge?rid=1).
2. On the cluster list page, select the target edge cluster ID to enter the cluster details page.
3. Select **Node Management** > **Node** on the left sidebar to enter the **Node List** page.
4. Select **More** > **Edit Label** on the right of the target node.
5. In the **Edit Label** pop-up window, edit the label and click **Submit** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/866a3570131ce8d80aed1d522dd51d36.png)

#### Enabling multi-region
After [enabling Edge Health](#open), click **Enable Multi-region**.
