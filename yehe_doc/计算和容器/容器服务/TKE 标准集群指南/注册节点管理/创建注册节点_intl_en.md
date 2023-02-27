This document describes how to create a registered node.

## Notes
- To ensure the stability of registered nodes, registered nodes can be accessed only through Direct Connect or CCN (VPN is currently not supported).
- The registered node feature is only available for TKE clusters of **v1.18 or later versions**.
- Registered nodes must use [TencentOS Server 3.1] or [TencentOS Server 2.4 (TK4)].
- To use registered nodes, a cluster must contain cloud nodes. A cluster cannot host registered nodes only.
- For scenarios where nodes on and off the cloud are deployed, the TKE team launched a hybrid cloud container network scheme based on Cilium-Overlay.

## Directions


### Installing the OS for the registered node
Currently, registered nodes must use [TencentOS Server 3.1] or [TencentOS Server 2.4 (TK4)]. Details are as follows:

| **OS** | **Description** | **Download Address** |
| :---- | :---- | :---- |
| TencentOS Server 3.1     | It is compatible with the CentOS 8 user mode and uses the T-Kernel 4 deeply optimized based on LTS kernel 5.4. | [Download](http://mirrors.tencent.com/tlinux/3.1/iso/x86_64/) |
| TencentOS Server 2.4 (TK4) | It is compatible with the CentOS 7 user mode and uses the T-Kernel 4 deeply optimized based on LTS kernel 5.4. | [Download](http://mirrors.tencent.com/tlinux/2.4/iso/) |

>? TencentOS Server is Tencent's Linux operating system designed for cloud scenarios. With specific features and optimized performance, it provides a high-performance, secure, and reliable operating environment for applications in CVM instances.

### Enabling support for registered nodes
For a network where nodes on and off the cloud use Cilium-Overlay, you can add registered nodes to only clusters whose network model is Cilium-Overlay. You can select an existing Cilium-Overlay cluster or create one.
- **Container network add-on**: Select **Cilium Overlay**.
- **Subnet**: TKE will create a proxy ENI in the selected subnet for the registered node to access cloud resources.

After the Cilium-Overlay cluster is created, the registered node feature is enabled by default. To query related information, go to the [TKE console](https://console.cloud.tencent.com/tke2) and choose **Basic Information** > **Node and Network Information**.

 

### Adding a registered node
#### Creating a registered node pool
>? Registered nodes can be managed only through a node pool.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster management** page, click the desired cluster ID to go to the **Basic information** page.
3. Click **Node management** > **Node pool** in the left sidebar to go to the **Node pool list** page.
4. Click **Create node pool** to open the **Create node pool** page. Specify the configurations.
- **Node pool name**: Enter a custom pool name.
   - **Node pool type**: Select **Registered node pool**.
   - **Container Directory**: Select this option to set up the container and image storage directory. We recommend that you store to the data disk, such as `/var/lib/docker`.
   - **Runtime component**: The runtime component of the container. **docker** and **containerd** are supported.
   - **Runtime version**: The version of the runtime component.
   - **Cordon initial nodes**: If **Cordon this node** is selected, new Pods cannot be scheduled to this node. You can uncordon the node manually, or execute the [uncordon command](https://intl.cloud.tencent.com/document/product/457/30654) in custom data as needed.
   - **Label**: Click **New label** and customize the settings of the label. The specified label here will be automatically added to nodes created in the node pool to help filter and manage external nodes using labels.
   - **Taints**: This is a node-level attribute and is usually used with `Tolerations`. You can specify this parameter for all the nodes in the node pool, so as to stop scheduling Pods that do not meet the requirements to these nodes and drain such Pods from the nodes.
     The value of **Taints** usually consists of `key`, `value`, and `effect`. Valid values of `effect`:
       - **PreferNoSchedule**: Optional. Try not to schedule a Pod to a node with a taint that cannot be tolerated by the Pod.
       - **NoSchedule**: When a node contains a taint, a Pod without the corresponding toleration must not be scheduled.
       - **NoExecute**: When a node contains a taint, a Pod without the corresponding toleration to the taint are not be scheduled to the node and any such Pods already on the node are drained. 
   - **Custom Data**: Specify custom data to configure the node, that is, to run the configured script when the node is started up. You need to ensure the reentrant and retry logic of the script. The script and its log files can be viewed at the node path: `/usr/local/qcloud/tke/userscript`.
5. Click **Create node pool**.

#### Adding a registered node
Do the following to add registered nodes to the node pool:
1. On the node pool page, click the desired node pool ID.
2. On the node pool details page, click **Create node** to get the script.
3. In the **Initialize script** window, select the download mode for node initialization, and copy or download the script.
-   **Public network**: Selected by default. For an IDC node, directly download the installation script file (31 KB in size) over the public network.
   -   **Private network**: If your IDC node cannot access the public network, access the private network through a Direct Connect line to download the installation script file.
4. Execute the script on your server.
   <dx-alert infotype="notice" title="">
   The script downloading link is valid for one hour. Since the script is downloaded via COS, you need to ensure that the IDC node can access COS through private/public network.
   </dx-alert>
5. Run the following command to add the node:
```
./ add2tkectl-cls-m57oxxxp-np-xxxx install
```
<dx-alert infotype="explain" title="">
If the node fails to be added because the related Docker and containerd add-ons are installed on the external node, run the following command to delete the add-ons and add the node again:
```
./add2tkectl-cls-m57oxxxp-np-xxxx clear
```
</dx-alert>
