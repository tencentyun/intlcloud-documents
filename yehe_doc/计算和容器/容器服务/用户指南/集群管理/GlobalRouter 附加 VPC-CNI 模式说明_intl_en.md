### VPC-CNI Mode in GlobalRouter
VPC-CNI is an extended network mode supported by Tencent Kubernetes Engine (TKE). In VPC-CNI mode, Tencent Cloud ENI assigns IP addresses within the VPC instance to pods in the cluster, and the Tencent Cloud VPC instance is responsible for routing. In this way, the data plane and control plane of pods and nodes can be located at the same network layer. VPC-CNI pods can use all product features of Tencent Cloud VPC.
The VPC-CNI mode has use limits. We recommend that you check whether the mode adapts to your business scenarios in advance.

### VPC-CNI Use Cases
After enabling VPC-CNI for your cluster, you can specify workloads to use VPC-CNI when creating them.
In VPC-CNI mode, StatefulSet workloads support pods with static IP addresses. The IP addresses of these pods do not change after they are restarted or migrated. Therefore, they are suitable for scenarios such as restricting access based on source IP addresses and querying logs based on IP addresses.

### VPC-CNI Use Limits
- VPC-CNI only supports TKE Kubernetes 1.10 and later versions.
- CNI support must be enabled for clusters.
- Subnets in VPC-CNI mode cannot be used by other cloud resources, such as CVMs and CLBs.
- You can create VPC-CNI pods only on nodes in the same availability zone as the subnet. Therefore, plan your subnets in VPC-CNI mode in advance.
- You need to specify the maximum number of VPC-CNI pods on a single node, which cannot be modified after being specified. We recommend that the value be the same for all nodes in a cluster.

### How to Use VPC-CNI
#### Enabling VPC-CNI
1. Log in to the [TKE console](https://console.qcloud.com/tke2).
2. In the left sidebar, click **Cluster** to go to the cluster management page. Select a cluster and click **Basic Information**.
3. Enable in the **VPC-CNI mode** field. Then, select the subnet and confirm the use limits, as shown below.
![](https://main.qcloudimg.com/raw/19ec70c11d5eb083612dd4dec806b958.png)

#### Disabling VPC-CNI
1. Log in to the [TKE console](https://console.qcloud.com/tke2).
2. In the left sidebar, click **Cluster** to go to the cluster management page. Select a cluster and click **Basic Information**.
3. Disable in the **VPC-CNI mode** field. VPC-CNI can be disabled only when no VPC-CNI pods exist in the cluster.
![](https://main.qcloudimg.com/raw/e404afd6d5f3871aa7f913c6a045b144.png)
