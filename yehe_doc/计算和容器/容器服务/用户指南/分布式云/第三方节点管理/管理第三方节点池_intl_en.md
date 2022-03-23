## Overview

This document describes how to manage the external node pools in the cluster.

## Prerequisites

- You have [created a cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- The cluster Kubernetes is v1.18 or later version.





## Directions

### Enabling the support for external nodes

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the desired cluster ID to go to the **Basic Information** page.
3. On the **Node and Network Information** page, click ![](https://main.qcloudimg.com/raw/229ae67159ae90008fae042ce6b13fdf.png) on the right of **Import External Node**.
4. On the page of **Enable External Node**, configure the parameters.
 **Subnet**: A node accesses kube-apiserver through the VPC ENI. You need to provide a VPC subnet, and TKE automatically creates a proxy ENI in the selected subnet.
 - **Container Network Add-on**: **Cilium VXLan** and **Cilium BGP** are supported.
 - **Container Network**: An IP address within the IP range of the container network is assigned to the Pod that is running on the external node.
<dx-alert infotype="explain" title="">
After external node is enabled, the container IP range/container subnet configured when creating the cluster will become invalid and the settings of this container network will take effect.
</dx-alert>
5. Click **Enable**.



### Creating an external node pool
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the target cluster ID to open the **Deployment** page.
3. Click **Node Management** > **Node Pool** in the left sidebar to go to the **Node Pool List** page.
4. Click **Create Node Pool** to open the **Create Node Pool** page. Specify the configurations as instructed below:
![](https://qcloudimg.tencent-cloud.cn/raw/989cff5896cffd96988e0bad762451b6.png)
 - **Node Pool Name**: Enter a custom pool name.
 - **Node Pool Type**: **CVM**, **Virtual Node** and **External Node** are supported. When the external node is enabled, only **External Node** is supported.
 - **Container Directory**: Check this option to set up the container and image storage directory. We recommend that you store to the data disk, such as `/var/lib/docker`.
 - **Runtime Component**: The runtime component of the container. **docker** and **containerd** are supported.
 - **Runtime Version**: The version of the runtime component.
  - **Cordon Initial Nodes**: If **Cordon this node** is checked, new Pods cannot be scheduled to this node. You can uncordon the node manually, or execute the [uncordon command](https://intl.cloud.tencent.com/document/product/457/30654) in custom data as needed.
  - **Label**: Click **New Label** and customize the settings of the label. The specified label here will be automatically added to nodes created in the node pool to help filter and manage external nodes using labels.
<dx-alert infotype="explain" title="">
Instructions on the required Labels (**only enter values and do not change the keys**):
- tke.cloud.tencent.com/location
- If the container network mode is set as **Cilium BGP**, the following two Labels are required:
  - `infra.tce.io/as`: The BGP AS number of the switch where the node resides 
  - `infra.tce.io/switch-ip`: The IP of the switch where the node resides 
  </dx-alert>
 - **Taints**: This is a node-level attribute and is usually used with `Tolerations`. You can specify this parameter for all the nodes in the node pool, so as to stop scheduling Pods that do not meet the requirements to these nodes and drain such Pods from the nodes.
  The value of **Taints** usually consists of `key`, `value`, and `effect`. Valid values of `effect`:
    - **PreferNoSchedule**: Optional. Try not to schedule a Pod to a node with a taint that cannot be tolerated by the Pod.
    - **NoSchedule**: When a node contains a taint, a Pod without the corresponding toleration must not be scheduled.
    - **NoExecute**: When a node contains a taint, a Pod without the corresponding toleration to the taint are not be scheduled to the node and any such Pods already on the node are drained. Assume that **Taints** is set to `key1=value1:PreferNoSchedule`, the configuration in the TKE console is as below. 
      ![](https://qcloudimg.tencent-cloud.cn/raw/bdb231723a67251f8885cbf9db9b6908.png)
 - **Custom data**: specify custom data to configure node, that is, to run the configured script when the node is started up. You need to ensure the reentrant and retry logic of the script. The script and its log files can be viewed at the node path: `/usr/local/qcloud/tke/userscript`.
5. Click **Create Node Pool** to create an external node pool.

### Creating an external node

Do the following to add nodes to the external node pool:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the target cluster ID to open the **Deployment** page.
3. Click **Node Management** > **Node Pool** in the left sidebar to go to the **Node Pool List** page.
4. On the node pool page, click the desired node pool ID.
5. On the node pool details page, click **Create Node** to get the script.
6. In the **Initialize Script** window, copy or download the script, as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/71822060e3fb8e179f4dadc8610a3856.png)
7. Execute the script on your server.
<dx-alert infotype="notice" title="">
The script downloading link is valid for one hour. Since the script is downloaded via COS, you need to ensure that the IDC node can access COS through private/public network.
</dx-alert>
8. Run the following command to add the node:
```
./ add2tkectl-cls-m57oxxxp-np-xxxx install
```






### Modifying an external node pool

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the target cluster ID to open the **Deployment** page.
3. Click **Node Management** > **Node Pool** in the left sidebar to go to the **Node Pool List** page.
4. On the node pool page, select the node pool of which the type is **External Node** and click **Edit**.
5. In the **Adjust External Node Pool Configuration** window, you can modify the node pool name, Labels and Taints.
<dx-alert infotype="notice" title="">
Note that the modifications of Labels and Taints apply to all external nodes in the node pool. 
</dx-alert>


### Deleting an external node pool

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the target cluster ID to open the **Deployment** page.
3. Click **Node Management** > **Node Pool** in the left sidebar to go to the **Node Pool List** page.
4. On the upper-right corner of the desired node pool page, click **Delete**.
5. Click **OK** in the **Delete External Node Pool** window to delete the node pool.
<dx-alert infotype="notice" title="">
- After the external node pool is deleted, all external nodes in the pool are removed from the cluster. The Pods running on the node are not cleared.
- For security reasons, after deleting the node, it is recommended to reinstall the node or run the following command to delete the kube-apiserver access configuration on the node:
```
>rm - rf /etc/kubernetes $HOME/.kube
```
</dx-alert>
