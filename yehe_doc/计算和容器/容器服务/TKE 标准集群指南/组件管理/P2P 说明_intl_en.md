## Overview

### Add-on description
The P2P add-on is a Kubernetes plug-in provided by the Tencent Container Registry (TCR) service for the accelerated distribution of container images. Based on P2P technology, this add-on can accelerate the pulling of container images in the gigabytes by massive TKE clusters. It supports concurrent pulling by thousands of nodes.

This add-on consists of `p2p-agent`, `p2p-proxy`, and `p2p-tracker`.
- p2p-agent is deployed on each node in a cluster. It serves as the agent for receiving image pull requests from each node and forwarding these requests to each peer (node) in the P2P network.
- p2p-proxy is deployed on some nodes in a cluster. It serves as the raw seed to connect to the image repository to be accelerated. In addition to serving as seeds, proxy nodes need to pull raw data from the target image repository.
- p2p-tracker is deployed on some nodes in a cluster. It serves as the tracker service of the open-source BitTorrent protocol.

### Kubernetes objects deployed in a cluster

| Kubernetes Object Name | Type | Requested Resource | Namespace |
| :----------------- | ---------- | ---------------------------- | -------------- |
| p2p-agent | DaemonSet | Per node: 0.2 CPU cores and 0.2 GB memory | kube-system |
| p2p-proxy | Deployment | Per node: 0.5 CPU cores and 0.5 GB memory | kube-system |
| p2p-tracker | Deployment | Per node: 0.5 CPU cores and 0.5 GB memory | kube-system |
| p2p-proxy | Service | - | kube-system |
| p2p-tracker | Service | - | kube-system |
| agent | Configmap | - | kube-system |
| proxy | Configmap | - | kube-system |
| tracker | Configmap | - | kube-system |

## Use Cases

This add-on can accelerate the pulling of container images in the gigabytes by massive TKE clusters and supports concurrent pulling by thousands of nodes. Its recommended use cases are as follows:
- The cluster has 500 to 1,000 nodes, and local disks are used to store pulled container images. In this scenario, nodes in the cluster support a maximum concurrent pull speed of 100 MB/s.
- The cluster has 500 to 1,000 nodes, CBS cloud disks are used to store pulled container images, and the cluster is located in a major Chinese region, such as Guangzhou, Beijing, or Shanghai. In this scenario, nodes in the cluster support a maximum concurrent pull speed of 20 MB/s.

## Limits
- If the P2P add-on is enabled in a large-scale cluster to pull container images, a high read/write pressure is imposed on node data disks, which may affect existing businesses in the cluster. If cluster nodes use CBS cloud disks to store pulled container images, select a proper download speed limit based on the region of the cluster or contact your after-sales agent/architect to prevent read/write overload of cloud disks from interrupting existing businesses in the cluster during image pulling or even affecting the normal operations of other users in the region.
- To enable the P2P add-on, you must reserve some resources. During image pull acceleration, the P2P add-on consumes the CPU and memory resources of nodes. These resources are released after the acceleration is completed.
 - The limit of p2p-proxy is 4 CPU cores and 4 GB memory.
 - The limit of p2p-agent is 4 CPU cores and 2 GB memory.
 - The limit of p2p-tracker is 2 CPU cores and 4 GB memory.
- You need to estimate the number of p2p-proxies to be launched based on the node scale of the cluster. The minimum node configuration for running a p2p-proxy is 4 CPU cores and 8 GB memory, with a private network bandwidth of 1.5 GB/s. A single p2p-proxy supports up to 200 cluster nodes.
- You need to select the nodes on which to deploy p2p-proxy and p2p-tracker by manually attaching Kubernetes labels. For more information, see [Usage](#Instructions). The nodes where p2p-proxy and p2p-tracker are located must be able to access the origin server of the repository.
- P2p-agent uses port 5004 of the nodes and P2P dedicated communication ports 6881 (for p2p-agent) and 6882 (for p2p-proxy). P2p-agent and p2p-proxy will create the local work directories `/p2p_agent_data` and `/p2p_proxy_data` respectively to cache container images. Ensure in advance that nodes have reserved sufficient storage space.




<span id="Instructions"></span>
## Usage
1. Select proper nodes on which to deploy and run p2p-proxy.
You can label nodes by running `kubectl label nodes XXXX proxy=p2p-proxy`. Then, p2p-proxy will be automatically deployed on these nodes upon installation of the P2P add-on. After the installation, if you want to adjust the number of p2p-proxies, you can add or delete the labels on the specified nodes and then change the number of p2p-proxy workload replicas under the kube-system namespace of the cluster.
2. Select proper nodes on which to deploy and run p2p-tracker.
You can label nodes by running `kubectl label nodes XXXX tracker=p2p-tracker`. Then, p2p-tracker will be automatically deployed on these nodes upon installation of the P2P add-on. After the installation, if you need to adjust the number of p2p-trackers, you can add or delete the label on the specified nodes, and then change the number of p2p-tracker workload replicas under the kube-system namespace of the cluster.
3. The following configuration must be added to the node security group: in inbound rules, open ports 30000-32768 of TCP and UDP, and open all IP addresses in the VPC to the Internet. In outbound rules, open all ports (the default security group of TKE cluster work nodes already meets this requirement).
4. Select the specified cluster to [activate the P2P add-on](#start). Enter the domain name of the image repository to be accelerated, node pull speed limit, number of p2p-proxies, and number of p2p-trackers. After installation, if you want to adjust the maximum download speed, modify downloadRate and uploadRate in p2p-agent configmap.
5. In the business namespace, create a dockercfg for pulling images where the repository domain name is localhost:5004, and the username and password are the original access credential of the target image repository.
6. Modify the business YAML file by changing the domain name address of the image repository to be accelerated to localhost:5004 (for example, localhost:5004/p2p-test/test:1.0) and using the newly created dockercfg as ImagePullSecret.
7. Use the business YAML file to deploy updated workloads and monitor the image pull speed and the read/write load of the node disks in real time. Adjust the download speed limit of nodes in time to achieve optimal acceleration.




<span id="start"></span>
## Directions
1. Log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the "Add-on List" page.
4. On the "Add-on List" page, click **Create**. On the "Create an Add-on" page that appears, select **P2P**.
5. Choose **Parameter Configuration**. In the displayed "P2P Add-on Parameter Settings" window, specify the domain name of the image repository to be accelerated, node pull speed limit, number of p2p-proxies, and number of p2p-trackers, as shown in the figure below:
![](https://main.qcloudimg.com/raw/c69d1b37a511c9ba0dc95ec3d67d557d.png)
