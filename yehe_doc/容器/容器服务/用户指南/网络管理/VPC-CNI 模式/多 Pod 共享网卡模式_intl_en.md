
## How It Works

The following diagram illustrates how the multiple pods sharing ENI in VPC-CNI mode work.
![](https://main.qcloudimg.com/raw/d8f0de10f2f6ac320d8afd2abe93b79e.png)

- The cluster network is the user's VPC, and the nodes and container subnets belong to this VPC.
- The container subnet can select multiple subnets in the VPC.
- You can set whether to enable the static IP address. For more information, see [Static IP Address Usage](https://intl.cloud.tencent.com/document/product/457/38975).
  - Non-static IP address mode (by default): cluster will apply for an ENI for each new node. TKE will apply for the IP resources of the maximum number of IPs that the ENI can bind for this ENI at one time, which is used for the Pod IP address on the node.
  - Static IP address mode: cluster will apply for an ENI for each new node. No secondary IP will be bound in advance. When the cluster creates a new Pod using the VPC-CNI mode, it will immediately apply to bind the secondary IP to the ENI of the corresponding node.
- When the node is deleted, the IP resources occupied by the ENI will be released.


## Usage


To use VPC-CNI, ensure that `rp_filter` is disabled. You can refer to the following code sample:
``` bash
sysctl -w net.ipv4.conf.all.rp_filter=0
# Assume that eth0 is the primary ENI.
sysctl -w net.ipv4.conf.eth0.rp_filter=0
```
>! The `tke-eni-agent` component automatically sets the node kernel parameters. If you manually maintain the kernel parameters and enable `rpfilter`, network connection will fail.


### Enabling VPC-CNI

#### Enabling VPC-CNI when creating the cluster

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click **Create** above the cluster list.
3. On **Create Cluster** page, select **VPC-CNI** for **Container Network Add-on**.


>? By default, the VPC-CNI mode **does not enable the static IP address**. You can enable the static IP address only when [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637). If you need to enable the static Pod IP address for the cluster, see [Static IP Address Usage](https://intl.cloud.tencent.com/document/product/457/38975).




#### Enabling VPC-CNI for the existing clusters
When creating a cluster, select the Global Router network plug-in. On the basic information page of the cluster, enable the VPC-CNI mode (by default, both modes are enabled).
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On **Cluster Management** page, select a cluster ID that needs to enable VPC-CNI and go to its details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the **Node and Network Information** section, enable **VPC-CNI mode**.
5. Select the subnet and set the **IP Reclaiming Policy** in the pop-up window.
>! 
>- In static-IP scenarios, after enabling VPC-CNI, you need to set the IP reclaiming policy to specify how long the IP addresses are returned after pods are terminated.
>- Pods with non-static IP addresses are not affected by these settings because their IP addresses are immediately released upon pod termination.
6. Click **Submit**.

### Disabling VPC-CNI
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On **Cluster Management** page, select a cluster ID that needs to enable VPC-CNI and go to its details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the **Node and Network Information** section, enable **VPC-CNI mode**.
5. Click **Submit** in the pop-up window.









