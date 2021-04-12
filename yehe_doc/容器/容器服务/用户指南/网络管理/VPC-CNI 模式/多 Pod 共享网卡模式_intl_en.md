
## How It Works

The following diagram illustrates how the multiple Pods with shared ENI in VPC-CNI mode work.
![](https://main.qcloudimg.com/raw/d8f0de10f2f6ac320d8afd2abe93b79e.png)

- The cluster network is the user's VPC, and the nodes and container subnets belong to this VPC.
- The container subnet can select subnets in multiple VPCs.
- You can set whether to enable the static IP address. For more information, see [Static IP Address Usage](https://intl.cloud.tencent.com/document/product/457/38975).

### IP Address Management Principle

#### Non-static IP address mode
- TKE will apply for an ENI for each new node in the cluster, and at the same time apply for the maximum number of IP addresses that can be bound to the ENI at a time. These IP addresses will be used as the available IP address pool of the node for the Pods on the node to use.
- When the Pod is created, an available IP address is randomly assigned from the available IP address pool bound to the node.
- When the Pod is terminated, the IP address is released and returned to the available IP address pool of the node. The unbinding of IP address from the ENI will not be triggered. Therefore, the IP address will not be returned to the VPC subnet.
- When the node is deleted, the IP addresses occupied by the ENI will be released.
- When there are multiple container subnets, the ENI is preferentially assigned to the subnet that has the largest number of available IP addresses and meets the quota requirement of the ENI's IP addresses. If there is no subnet that fully meets the quota requirement, the ENI is preferentially assigned to the subnet with the largest number of available IP addresses.

#### Static IP address mode
- TKE network add-on maintains a cluster-level available IP address pool.
- TKE will apply for an ENI for each new node in the cluster. No secondary IP address will be bound in advance, but the number of IP addresses that meets the IP address quota requirements of the ENI is reserved for this node in the network add-on.
- When a new Pod with VPC-CNI mode is created, the IPAMD add-on will assign an IP address based on the subnet where the ENI bound to the node is located, and then apply for binding the secondary IP to the ENI of the corresponding node immediately.
- When the Pod is terminated, the IP address will be returned to the available IP address pool of the cluster, the unbinding of IP address from the ENI is triggered, and the IP address will be released and returned to the VPC subnet.
- The static IP address of the terminated Pod will be retained in the TKE cluster, and this IP address will be used again when a Pod with the same name as the terminated Pod is created.
- When the node is deleted, the IP addresses occupied by the ENI will be released.
- When there are multiple container subnets, the ENI is preferentially assigned to the subnet that has the largest number of available IP addresses and meets the quota requirement of the ENI's IP addresses. If there is no subnet that fully meets the quota requirement, the node will fail to bind the ENI.


## Usage


To use VPC-CNI, ensure that `rp_filter` is disabled. You can refer to the following code sample:
``` bash
sysctl -w net.ipv4.conf.all.rp_filter=0
# Assume that eth0 is the primary ENI
sysctl -w net.ipv4.conf.eth0.rp_filter=0
```
>! The `tke-eni-agent` component automatically sets the node kernel parameters. If you have manually maintained the kernel parameters and enabled `rpfilter`, network connection would fail.


### Enabling VPC-CNI

#### Enabling VPC-CNI when creating the cluster

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click **Create** above the cluster list.
3. On **Create Cluster** page, select **VPC-CNI** for **Container Network Add-on**, as shown below:
![](https://main.qcloudimg.com/raw/26af6272145e26b2b3f8c92d79318635.png)

>? By default, the VPC-CNI mode **does not enable the static IP address**. You can enable the static IP address only when [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637). If you need to enable the static Pod IP address for the cluster, see [Static IP Address Usage](https://intl.cloud.tencent.com/document/product/457/38975).




#### Enabling VPC-CNI for the existing clusters
When creating a cluster, select the Global Router network add-on. Then, enable the VPC-CNI mode on the basic information page of the cluster (by default, both modes are enabled).
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On **Cluster Management** page, select a cluster ID that needs to enable VPC-CNI and go to its details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the **Node and Network Information** section, enable **VPC-CNI mode**.
5. Select the subnet and set the **IP Reclaiming Policy** in the pop-up window, as shown in the figure below:
![](https://main.qcloudimg.com/raw/3246c6d4a6217f176e7da51d986bc628.png)
>! 
>- For scenarios that use static IP addresses, when enabling VPC-CNI, you need to set the IP reclaiming policy to specify when to reclaim the IP addresses after Pods are terminated.
>- Pods with non-static IP addresses are not affected by these settings because their IP addresses are immediately released upon Pod termination. These IP addresses are not returned to the VPC, but returned to the IP address pool managed by the container.
6. Click **Submit**.

### Disabling VPC-CNI
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On **Cluster Management** page, select a cluster ID that needs to enable VPC-CNI and go to its details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the **Node and Network Information** section, disable the **VPC-CNI mode**.
5. Click **Submit** in the pop-up window to disable the VPC-CNI mode.









