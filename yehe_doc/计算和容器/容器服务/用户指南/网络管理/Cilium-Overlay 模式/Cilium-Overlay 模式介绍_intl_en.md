
## How It Works
The Cilium-Overlay network mode is a container network plugin provided by TKE based on Cilium VXLan. In this mode, you can add external nodes to TKE clusters in distributed cloud scenarios. The features of this mode are as follows:
- Cloud nodes and external nodes share the specified container IP range.
- Container IP ranges are dynamically assigned without occupying other IP ranges in the VPC instance.
- The Cilium VXLan tunnel encapsulation protocol is used to build the Overlay network.

Cross-node Pod access is supported after the VPC network in the cloud and the IDC network of the external node are interconnected through Cloud Connect Network. See the figure below to learn how it works.
![](https://qcloudimg.tencent-cloud.cn/raw/c09deb3c0e07b777a436c62945055158.png)

>? Due to performance loss in the Cilium-Overlay mode, this mode only supports the scenarios where external nodes are configured in distributed cloud, and does not support the scenarios where only cloud nodes are configured. For more information, see [External Node Overview](https://intl.cloud.tencent.com/document/product/457/45354).

 

## Usage Limits
- There is a performance loss of less than 10% when you use the Cilium VXLan tunnel encapsulation protocol.
- The Pod IP cannot be accessed directly outside the cluster.
- You must obtain two IPs from the specified subnet to create a private CLB, so that external nodes in IDC can access APIServer and the public cloud services.
- The IP ranges of the cluster network and container network cannot overlap.
- Static Pod IPs are not supported.


## Container IP Assignment Mechanism
For container network terms and quantity calculation, see [Container Network Overview](https://intl.cloud.tencent.com/document/product/457/38966).


#### Pod IP assignment
The following diagram illustrates how it works:
![](https://qcloudimg.tencent-cloud.cn/raw/7236dc566d0e89934c3e9636a5d04d11.png)

- Nodes in a cluster include cloud nodes and external nodes.
- Each node of the cluster will use the specified IP range in the container CIDR block for the node to assign IPs to Pods.
- The Service IP range of the cluster will select the last segment of the specified IP range in the container CIDR block for Service IPs assignment.
- After the node is released, the corresponding container IP range will be returned to the IP range pool as well.
- The added nodes automatically select the available IP ranges in the container CIDR block cyclically and sequentially.
