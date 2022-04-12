A weak edge network will trigger the Kubernetes draining mechanism, resulting in unexpected pod draining. In edge computing scenarios, the network environment between an edge server and the cloud is very complex, the network connection cannot be guaranteed, and the API server and node connection can easily be interrupted. If native Kubernetes is used without modification, the node status will be abnormal, triggering the draining mechanism of Kubernetes. Consequently, pods will be drained, EndPoints will be lost, and ultimately, service interruption and fluctuation will occur.

To solve this problem, the [Tencent Kubernetes Engine for Edge](https://intl.cloud.tencent.com/document/product/457/35390) (TKE Edge) introduced the distributed node status determination mechanism, which can better determine the timing of draining to ensure the proper running of the system in weak-network situations and prevent service interruption and fluctuation.

## Requirement Scenario

In edge scenarios, networks on the cloud edge are weak. Edge devices are located in edge cloud data centers and mobile edge sites, and the network environments between them and the cloud are complex. For example, the network connections between the cloud (control end) and the edge as well as the network connections between edge servers can be unreliable.
<span id="SmartFactory"></span>
### Smart factory

In the example of a smart factory, edge servers are located in plant warehouses and workshops, while the control-end Master node is in the Tencent Cloud central data center.

- The network between edge devices in warehouses and workshops and the cloud cluster is complex. It can be implemented via the Internet, 5G, Wi-Fi, and other formats. The network connection is not guaranteed.
- Compared with the network environment on the cloud, the network between edge devices in warehouses and workshops is a local network, which is of better quality and more reliable than the connection between edge devices and the cloud cluster.

### Audio and video pull scenario
In consideration of user experiences and companies’ costs, audio and video pull scenarios often require the improvement of the edge cache hit rate to reduce origin-pull, scheduling of the same user-requested file to the same service pod, and service pod cache files.

In the case of native Kubernetes, if a pod is frequently rebuilt due to network fluctuation, the performance of the service pod cache will be affected, and the scheduling system will schedule user requests to other service pods. Both cases have a major and even unacceptable impact on CDN performance.

In fact, as long as edge servers are running properly, pod draining or rebuilding is unnecessary. To resolve this problem and ensure continuous service availability, the TKE Edge team introduced the distributed node status determination mechanism.

## Requirement Pain Points

### Processing by native Kubernetes

A weak network on the cloud edge can affect the communication between Kubelet on edge servers and the API Server on the cloud. As a result, the API Server on the cloud cannot receive heartbeat or lease renewal from Kubelet and cannot accurately detect the running status of the node and pods on the node. If this situation persists beyond the set threshold, the API Server will deem that the node is unavailable and perform the following actions:

- The status of the unavailable node will be set to NotReady or Unknown, and the taints of NoSchedule and NoExecute will be added to the node.
- Pods on the unavailable node will be drained and be rebuilt on other nodes.
- Pods on the unavailable node will be removed from the Endpoint list of Service.

## Solutions

### Design principles

In edge computing scenarios, it is unreasonable to rely solely on the connection between an edge end and the API Server for determining whether a node is running normally. We need to bring in an additional detection mechanism to make the system more robust.

Compared with the network between the cloud and the edge end, the network between nodes on the edge end is more stable, and the more stable infrastructure can be used to improve accuracy. TKE Edge developed an innovative edge health distributed node status determination mechanism. In addition to considering the connection between a node and the API Server, the mechanism also brings in edge servers as an evaluation factor to judge the status of a node more comprehensively. Proven by testing and a large number of practical cases, this mechanism can greatly improve the accuracy of node status judgment in the case of weak cloud edge networks and guarantee the stable operation of services. The main principles of this mechanism are as follows:
- Each node periodically detects the health status of other nodes.
- All nodes in the cluster periodically vote to determine the status of each node.
- The cloud and edge nodes jointly determine node status.

First of all, the nodes detect and vote among themselves to determine whether a specific node is in an exceptional status. Only by ensuring the consensus of the majority of nodes can the specific status of a node be determined. Secondly, even if the network status between nodes is generally better than the cloud-edge network, the complex network of edge servers should be considered, and the network is not 100% reliable. Therefore, the network between nodes cannot be completely trusted, and the status of nodes cannot be determined by the nodes themselves alone. Joint determination by the cloud and edge is more reliable. Based on this consideration, we developed the following design:

| Ultimate node status | Deemed normal by the cloud | Deemed exceptional by the cloud |
| ---------------- | ------------ | ------------------------------------------------------------ |
| Deemed normal among nodes | Normal | No longer schedule new pods to the node |
| Deemed exceptional among nodes | Normal | Drain existing pods; remove the exceptional node from the EndPoint list; no longer schedule new pods to the node |

### Solution features    

When the cloud determines that a node is exceptional but other nodes determine that the node is normal, existing pods will not be drained. However, to ensure the stability of new services, no new pods will be scheduled to the node. The normal running of existing nodes is also attributable to the edge autonomy of edge clusters.

Due to the particularity of edge networks and their topology, single-point network failures often occur between node groups. For example, in the case of a [smart factory](#SmartFactory), although the warehouses and workshops belong to the plant area, the network connection between them only depends on one key link. Once this link is interrupted, it will cause a split between the node groups. The solution provided in this document can ensure that the majority of nodes in two split node groups will not be judged to be exceptional. This prevents the situation where, due to exception determinations, pods can only be scheduled to a small number of nodes, resulting in excessive node load.

Edge devices may be located in different regions and cannot communicate with each other. The solution provided in this document supports node status determination in multiple regions, and can easily group nodes by region or other methods to realize intra-group check. Even if nodes are re-grouped, there is no need to re-deploy detection components or reinitialize to adapt to the edge computing network layout. After grouping, nodes will only determine the status of nodes in the same group.

## Directions    

The distributed node status determination mechanism is enabled for TKE Edge clusters by default, whereas the multi-region check feature is disabled by default. To enable the multi-region check feature, perform the following operations:

### Grouping nodes by editing labels for nodes

1. Log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and click **Edge Cluster** in the left sidebar.
2. Select the ID of the cluster to which the target node for label editing belongs to go to the cluster management page.
3. Choose **Node Management** > **Node** to go to the node list page, as shown in the figure below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/7eb0f380d0e949961c3d1801f7670e4b.png)
4. In the row of the node for label editing, choose **More** > **Edit a Label** on the right.
5. In the pop-up “Edit a Label” window, add a label based on your need, as shown in the figure below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/866a3570131ce8d80aed1d522dd51d36.png)
6. Click **OK**.

### Enabling multi-region check

> ! When multi-region check is enabled, if nodes have not been grouped, each node is considered as a group by default, and the other nodes of other groups will not be checked.

1. Log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and click **Edge Cluster** in the left sidebar.
2. Click the ID of the cluster for which you want to enable the multi-region check feature to go to the cluster management page.
3. Select **Basic Information** to go to the “Basic Information” page and select **Enable Multi-region Check**.
   
