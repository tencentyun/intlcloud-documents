### VPC-CNI mode description
VPC-CNI is an extended network mode supported by Tencent Cloud TKE. In VPC-CNI mode, Tencent Cloud ENI assigns IP addresses within the VPC instance to pods in the cluster, and the Tencent Cloud VPC instance is responsible for routing. In this way, the data plane and control plane of pods and nodes can be located on the same network layer. VPC-CNI nodes can use all product features of Tencent Cloud VPC.
The VPC-CNI mode has use limits, and therefore you need to evaluate its adaptability with your application scenarios.

### VPC-CNI use cases
After enabling VPC-CNI for your cluster, you can specify workloads to use VPC-CNI when creating them to support the following:
Pods with static IP addresses supported by StatefulSet. The IP addresses of these pods do not change after they are restarted or migrated. Therefore, they are suitable for scenarios such as restricting access based on source IP addresses and query logs based on IP addresses.

### VPC-CNI use limits
1. Only Kubernetes 1.10, 1.12, 1.14 and 1.16 clusters are supported.
2. CNI support must be enabled for clusters.
3. In VPC-CNI mode, nodes cannot be scheduled across availability zones because VPC-CNI currently only supports a single subnet.
4. Subnets in VPC-CNI mode cannot be used by other cloud resources such as CVMs and CLBs.
5. You can only create VPC-CNI pods on nodes in the same availability zone as the subnet. Therefore, carefully plan your subnets in VPC-CNI mode in advance.
6. You need to specify the maximum number of VPC-CNI pods on a single node, which cannot be modified after creation. We recommend that nodes in a cluster share the same configuration.

### How to use VPC-CNI
#### Enabling VPC-CNI
1. Log in to the [TKE console](https://console.qcloud.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page. Then, click **Basic Information**.
3. In the "VPC-CNI" field, select "Enable". Then, select the subnet and confirm the use limits, as shown below:
![](https://main.qcloudimg.com/raw/19ec70c11d5eb083612dd4dec806b958.png)

#### Disabling VPC-CNI
1. Log in to the [TKE console](https://console.qcloud.com/tke2).
2. In the left sidebar, click **Clusters** to go to the cluster management page. Then, click **Basic Information**.
3. In the **VPC-CNI** field, select **Disable** (VPC-CNI can be disabled only when no VPC-CNI pods exist in the cluster), as shown below:
![](https://main.qcloudimg.com/raw/e404afd6d5f3871aa7f913c6a045b144.png)
