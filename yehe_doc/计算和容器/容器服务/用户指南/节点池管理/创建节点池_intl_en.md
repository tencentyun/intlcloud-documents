## Overview
This document describes how to create a node pool in a cluster via the TKE console and describes node pool-related operations, such as viewing, managing, and deleting a node pool.


## Prerequisites
- You are familiar with the [Node Pool Concepts](https://intl.cloud.tencent.com/document/product/457/35900).
- You have [created a cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Notes
TKE allows you to convert an existing scaling group in a cluster to a node pool. If a scaling group has already been created in the cluster, you can create a node pool by using the existing scaling group.
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster** page, click the desired cluster ID to open the **Deployment** page.
3. In the left sidebar, choose **Node Management** > **Scaling group** to open the “Scaling group list” page.
![](https://main.qcloudimg.com/raw/3f7687f710e9a09e81d93b6bb4f5cbd8.png)
4. In the **Operation** column of the desired scaling group, choose **More** > **Create Node Pool**. In the window that appears, click **OK**.
>?After the node pool is created, you can view the related information of the node pool. For more information, see [Viewing a Node Pool](https://intl.cloud.tencent.com/document/product/457/35902). The original **Scaling group** cannot be viewed again.


## Directions

1. On the “Cluster” page, click the desired cluster ID to open the “Deployment” page.
2. In the left sidebar, choose **Node Management** > **Node pool** to open the “Node pool list” page.
![](https://main.qcloudimg.com/raw/d58e9454d7e191c669b382caedd2f547.png)
3. Click **Create Node Pool** to open the “Create Node Pool” page. Specify the configurations according to the following descriptions.
![](https://main.qcloudimg.com/raw/ccabf536db92a234c7df3851f4cf7fa1.png)
 - **Node Pool Name**: you can customize the name of the node pool based on service requirements to facilitate subsequent resource management.
 - **Operating System**: select an OS based on actual needs. This OS takes effect on the node pool level and can be modified. After modification, the new OS only take effect for the new nodes in the node pool, rather than the existing nodes.
 - **Billing Mode**: valid values include **Pay-as-you-go** and **Spot**. You can select the value as needed. For more information, see [Payment Modes](https://intl.cloud.tencent.com/document/product/213/2180).
 - **Supported Network**: the system will assign IP addresses within the address range of the node network for servers in the cluster.
>! This field is specified at the cluster level, which cannot be modified after configuration.

 - **Model Configuration**: click **Select a model**. On the “Model Settings” page, select the values as needed based on the following descriptions:
    - **Availability Zone**: launch configurations do not contain availability zone information. This option is only used to filter available instance types in the availability zone.
    - **Model**: you can select the model by specifying the number of CPU cores, memory size, and instance type. For more information, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518) and [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
    - **System disk**: controls the storage and schedules the operating of Cloud Virtual Machines (CVMs). You can view the system disk types available for the selected model and select the system disk as needed. For more information, see [Cloud Disk Types](https://intl.cloud.tencent.com/document/product/362/31636).
    - **Data disk**: stores all the user data. You can specify the values according to the following descriptions. Each model corresponds to different data disk settings. For more information, see the following table:
  <table>
  <tr>
  <th>Model</th>
  <th>Data Disk Settings</th>
  </tr>
  <tr>
  <td>Standard, Memory Optimized, Computing, and GPU</td>
  <td>No option is selected by default. If you select any of these options, you must specify the cloud disk settings and formatting settings.</td>
  </tr>
  <tr>
  <td>High I/O and Big Data</td>
  <td>These options are selected by default and cannot be cleared. You can customize the formatting settings for the default local disks.</td>
  </tr>
  <tr>
  <td>Batch-based</td>
  <td>This option is selected by default, but can be cleared. If this option is selected, you can purchase only default local disks. You can customize the formatting settings for the default local disks.</td>
  </tr>
  </table>
  - **Add Data Disk (Optional)**: click **Add Data Disk** and specify the settings according to the preceding table.
    - **Public Bandwidth**: **Assign free public IP** is selected by default. The system assigns a free public IP address. You can select Bill By Traffic or Bill by Bandwidth for the billing mode as required and customize the network speed. For more information, see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).
 - **Login Methods**: you can select any one of the following login methods as required:
    - **SSH Key Pair**: a key pair is a pair of parameters generated by using an algorithm. Using a key pair to log in to a CVM instance is more secure than using regular passwords. For more information, see [SSH Key](https://intl.cloud.tencent.com/document/product/213/6092).
     - **SSH Key**: this configuration item is available only when **SSH Key Pair** is selected. You can select an existing key from the drop-down list. If you need to create an SSH key pair, see [Creating an SSH Key Pair](https://intl.cloud.tencent.com/document/product/213/16691).
    - **Random Password**: the system sends an automatically generated password to you via an [Internal Message](https://console.cloud.tencent.com/message). 
    - **Custom Password**: set a password as prompted.
 - **Security Groups**: the default value is the security group specified when the cluster is created. You can replace the security group or add a security group as required.
 - **Quantity**: the desired capacity. You can specify this value as required.
>! If auto scaling has been enabled for the node pool, this quantity will be automatically adjusted based on the loads of the cluster.

 - **Node Quantity Range**: the number of nodes will be automatically adjusted within the specified node quantity range, which will not exceed the specified range.
 - **Supported subnets**: select an available subnet as required.
>? The default multiple subnets scale-out policy of node pool is that if you have configured multiple subnets, when the node pool performs scale-out (manual scale-out and auto scaling), it creates nodes based on the priority determined by the order in the subnet list. If a node can be successfully created in the subnet of the highest priority, all nodes will be created in the subnet.

4. (Optional) Click **More Settings** to view or configure more information, as shown in the following figure.
![](https://main.qcloudimg.com/raw/f3018ed7f3bebcc5163cd34e5eb94e49.png)

 - **CAM Role**: binds the same CAM role to all nodes in the node pool, granting the authorization policy of this role to the nodes. For more information, please see [Managing Roles](https://intl.cloud.tencent.com/document/product/213/38290).
 - **Container Directory**: after selecting this option, you can specify directories for storing containers and images. We recommend that you store the containers and images in a data disk, such as `/var/lib/docker`.
  - **Security Reinforcement**: DDoS Protection, Web Application Firewall (WAF), and Cloud Workload Protection are activated by default. For more information, see [Cloud Workload Protection](https://intl.cloud.tencent.com/product/cwp).
  - **Cloud Monitor**: Tencent Cloud service monitoring, analysis, and alarms are activated by default, and components are installed to obtain CVM monitoring metrics. For more information, see [Cloud Monitor](https://intl.cloud.tencent.com/product/cm).
  - **Auto Scaling**: **Enable** is selected by default.
  - **Cordon Initial Node**: after **Cordon this node** is selected, no new Pod can be scheduled to this node. To uncordon the node, you must manually uncordon the node or run the [Uncordon command](https://intl.cloud.tencent.com/document/product/457/30654) in custom data and specify the values as needed.
  - **Label**: click **New Label** and customize the settings of the label. The specified label here will be automatically added to nodes created in the node pool to help filter and manage nodes using labels.
  - **Taints**: taints are node attributes. This parameter is usually used with `Tolerations`. You can specify this parameter for all the nodes of the node pool so that Pods that do not meet the relevant conditions cannot be scheduled to these nodes and any such Pods already on these nodes will be drained.
>?The value of Taints usually consists of `key`, `value`, and `effect`. Valid values of `effect`:
> - **PreferNoSchedule**: optional condition. Try not to schedule a Pod to a node with a taint that cannot be tolerated by the Pod.
> - **NoSchedule**: when a node contains a taint, a Pod without the corresponding toleration cannot be scheduled.
> - **NoExecute**: when a node contains a taint, a Pod without the corresponding toleration to the taint will not be scheduled to the node and any such Pods already on the node will be drained.

  Assume that Taints is set to `key1=value1:PreferNoSchedule`. The following figure shows the configurations in the TKE console:
  ![](https://main.qcloudimg.com/raw/9f8c0a99099ff58c12ee0d0ad2349b9e.png)
  - **Retry Policy**: select one of the following policies as required.
    - **Try again**: retry immediately. The system stops retrying after failing five times in a row.
    - **Retry with incremental intervals**: the retry interval extends as the number of consecutive failures increases. The value ranges from seconds to one day.
   - **Scaling Mode**: select one of the following two scaling modes as required.
     - **Release Mode**: if this mode is selected, the system automatically releases idle nodes as determined by Cluster AutoScaler during scale-in and automatically creates and adds a node to scaling groups during scale-out.
     - **Shutdown Mode**: if this mode is selected, during scale-out, the system preferably starts nodes that have been shut down, and if the number of nodes still fails to meet requirements, the system creates the desired number of nodes. During scale-in, the system shuts down idle nodes. If the nodes support the No Charges When Shut Down feature, the nodes that are shut down will not be billed, but remaining nodes are still billed. For more information, see [No Charges When Shut down for Pay-as-You-Go Instances Details](https://intl.cloud.tencent.com/document/product/213/19918).
   - **Custom data**: specifies custom data to configure the node. This means that, when the node starts, the system runs the configured script. You must ensure that the script is reentrant and a retry logic is configured for the script. You can view the script and the log file generated by the script in the `/usr/local/qcloud/tke/userscript` path of the node.

5. Click **Create Node Pool** to create the node pool.

## References

After a node pool is created, you can manage the node pool according to the following documents:

- [Viewing a Node Pool](https://intl.cloud.tencent.com/document/product/457/35902)
- [Adjusting a Node Pool](https://intl.cloud.tencent.com/document/product/457/35903)
- [Deleting a Node Pool](https://intl.cloud.tencent.com/document/product/457/35904)
