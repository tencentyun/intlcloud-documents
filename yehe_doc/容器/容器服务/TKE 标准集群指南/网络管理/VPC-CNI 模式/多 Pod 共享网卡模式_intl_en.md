
## How It Works

The following diagram illustrates how the multiple Pods with a shared ENI in VPC-CNI mode work.
![](https://main.qcloudimg.com/raw/d8f0de10f2f6ac320d8afd2abe93b79e.png)

- The cluster network is the user's VPC, and the nodes and container subnets belong to this VPC.
- The container subnet can select subnets in multiple VPCs.
- You can set whether to enable the static IP address. For more information, see [Static IP Address Usage](https://intl.cloud.tencent.com/document/product/457/38975).

### IP Address Management Principle

#### Non-static IP address mode

![](https://qcloudimg.tencent-cloud.cn/raw/ac68ff6ff975501ca91ebcb3d3cd5079.png)

- TKE maintains an auto-scaling IP pool on each node. The number of bound IPs ranges from **the number of Pods + the minimum number of pre-bound IPs** to **the number of Pods + the maximum number of pre-bound IPs**.
	- When **the number of bound IPs is less than the number of Pods + the minimum number of pre-bound IPs**, new IPs will be bound to make **the number of bound IPs = the number of Pods + the minimum number of pre-bound IPs**.
	- When **the number of bound IPs is larger than the number of Pods + the maximum number of pre-bound IPs**, an IP will be released about every 2 minutes until **the number of bound IPs = the number of Pods + the maximum number of pre-bound IPs**.
	- When **the maximum number of bindable IPs is less than the number of bound IPs**, the unnecessary idle IPs will be released directly to make **the number of bound IPs equal to the maximum number of bindable IPs**.
- When a Pod with a shared ENI is created, an available IP is randomly allocated from the node’s available IP pool.
- When a Pod with a shared ENI is terminated, its IP will be released and returned to the IP pool of the node instead of being released (deleted) in the VPC, so that another Pod can continue to use the IP.
- IPs and ENIs are allocated and released based on the **principle of least ENIs** to ensure that the ENIs in use are as few as possible:
	- **Allocate an IP to a Pod**: preferentially allocate IPs on the ENI with the most allocated IPs.
	- **Release an IP**: preferentially release IPs on the ENI with the least allocated IPs.
    - **Bind to a new ENI**: if the IP quota of the bound ENI is exhausted or the IPs of the subnet where the ENI is located is used up, you can apply for a new ENI.
	- **Release an ENI**: if all secondary IPs on the bound ENI have been unbound and you do not want to add IPs, you can unbind and delete the ENI.
- The expansion resource `tke.cloud.tencent.com/eni-ip` will be registered for the node. The allocatable number of the resource is the number of IPs that have been bound. The capacity is the maximum number of IPs that can be bound to the node. Therefore, if a Pod fails to be scheduled to a node, it indicates that the IPs of the node have been used up.
- Select a subnet for a new ENI: preferentially select the subnet with the most available IPs.
- The maximum number of bindable IPs of each node = the maximum number of bound ENIs * the number of bindable IPs of a single ENI
- Currently, **the minimum number of pre-bound IPs** and **the maximum number of pre-bound IPs** are set to five respectively by default.

#### Static IP address mode
- TKE network component maintains an IP pool available at the cluster level.
- Each newly added node in the cluster will not be bound to any secondary IP address or ENI in advance, and IP addresses are totally **allocated on demand**.
- When a Pod in VPC-CNI mode is created, the IPAMD component will find an available ENI for IP address allocation on the corresponding node. The allocation follows the principle of **least ENIs**, that is, the ENI bound to the most number of IP addresses is allocated first.
- If the existing ENI is bound to a maximum number of IP addresses, create an ENI for IP address allocation. The subnet that has the largest number of available IP addresses is preferred for the ENI.
- If the Pod without a static IP address annotation is terminated, the IP address will be returned to the available IP pool of the cluster, the unbinding of the IP address from the ENI will be triggered, and the IP address will be released and returned to the VPC subnet.
- The static IP address of the terminated Pod will be retained in the VPC, and this IP address will be used again when a Pod with the same name as the terminated Pod is created.
- When the node is deleted, the IP addresses occupied by the ENI will be released.
- When there are multiple container subnets, the ENI is preferentially allocated to the subnet that has the largest number of available IP addresses. If there is no such subnet, the ENI binding will fail.

### Data Plane Principle for Multiple ENIs

When a node has bound multiple ENIs, the network packets sent from the Pod will be forwarded to the corresponding ENI according to the policy-based routing.
- You can execute `ip link` on the node to view the information of all network devices on the node, and you can learn about the network devices corresponding to the ENI of the node through comparison of the mac address of the ENI. Generally, `eth0` represents primary ENI, `eth1` and `eth2` represent secondary ENIs:
![](https://qcloudimg.tencent-cloud.cn/raw/b4b357d3b4991195c8a618e817bc8c81.jpg)

- You can execute `ip rule` on the node to view the information of policy-based route table. TKE network component obtains the number of the route table through `<link index>+2000` of the ENI. Network packets sent from the Pod that is bound to the corresponding ENI IP will be forwarded to this route table. In this example, the route table corresponding to `eth1` is 2003, and the route table corresponding to `eth2` is 2010.
![](https://qcloudimg.tencent-cloud.cn/raw/0c3a14cb4402a5c108ac6f9b1f72f5cf.png)

- The default routing to the corresponding ENI is set for the corresponding route table. You can execute `ip route show table <id>` on the node to view it:
![](https://qcloudimg.tencent-cloud.cn/raw/881653493b4188b34a78e3b3e769adc6.png)

When the network packets that are sent to the Pod reach the node, they will be sent to the Veth ENI of the Pod via the primary route table by following the policy-based routing.


## How to Use


To use VPC-CNI, ensure that `rp_filter` is disabled. You can refer to the following code sample:
``` bash
sysctl -w net.ipv4.conf.all.rp_filter=0
# Assume that eth0 is the primary ENI
sysctl -w net.ipv4.conf.eth0.rp_filter=0
```
>! The `tke-eni-agent` component automatically sets the node kernel parameters. If you have manually maintained the kernel parameters and enabled `rpfilter`, network connection would fail.


### Enabling VPC-CNI

#### Enabling VPC-CNI when creating the cluster

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Cluster** on the left sidebar.
2. On the "Cluster management" page, click **Create** above the cluster list.
3. On "Create Cluster" page, select **VPC-CNI** for **Container Network Add-on**, as shown below:
![](https://main.qcloudimg.com/raw/26af6272145e26b2b3f8c92d79318635.png)

>? By default, the VPC-CNI mode **does not enable the static IP address**. You can enable the static IP address only when [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637). If you need to enable the static Pod IP address for the cluster, see [Static IP Address Usage](https://intl.cloud.tencent.com/document/product/457/38975).




#### Enabling VPC-CNI for the existing clusters
When creating a cluster, select the Global Router network add-on. Then, enable the VPC-CNI mode on the basic information page of the cluster (by default, both modes are enabled).
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** on the left sidebar.
2. On "Cluster Management" page, select the ID of the cluster for which VPC-CNI needs to be enabled and go to its details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the **Node and Network Information** section, enable **VPC-CNI mode**.
5. In the pop-up window, specify whether to support static IP addresses and select the subnet as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/22d8257099799f8a527d07eeefcb5602.png)
>! 
>- For scenarios that use static IP addresses, when enabling VPC-CNI, you need to set the IP reclaiming policy to specify when to reclaim the IP addresses after Pods are terminated.
>- Pods with non-static IP addresses are not affected by these settings because their IP addresses are immediately released upon Pod termination. These IP addresses are not returned to the VPC, but returned to the IP address pool managed by the container.
6. Click **Submit** to enable VPC-CNI mode for the cluster.

### Disabling VPC-CNI
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** on the left sidebar.
2. On "Cluster Management" page, select the ID of the cluster for which VPC-CNI needs to be enabled and go to its details page.
3. On the cluster details page, click **Basic Information** on the left.
4. In the **Node and Network Information** section, disable the **VPC-CNI mode**.
5. Click **Submit** in the pop-up window to disable the VPC-CNI mode.









