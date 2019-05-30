## Operation Scenario

This document guides you through the process of creating a cluster.

## Directions

1. <span id="step1">Log in to the [TKE console](https://console.cloud.tencent.com/tke2). </span>
2. In the left sidbar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. On the cluster management page, click **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/5d4bc55fd7ad81ffb15c4acb5537cb02.png)
4. On the "Create a cluster" page, set the basic information of the cluster. See the figure below:
![Create a cluster](https://main.qcloudimg.com/raw/a3f2dd27df6f766b4811369d615e101b.png)
 - **Cluster name**: The name of the cluster to be created. Up to 60 characters.
 - **Project for new resources**: Select based on actual needs. Newly added resources will be automatically assigned to this project.
 - **Kubernetes version**: Multiple Kubernetes versions are available. For a comparison of the features of different versions, see [Supported Versions of the Kubernetes Documentation](https://kubernetes.io/docs/home/supported-doc-versions/).
 - **Region**: It is recommended that you select a region that is close to your location. This can reduce the access latency and increase the download speed.
 - **Cluster network**: Assign IP addresses within the node network address range to the servers in the cluster. For more information, see [Container and Node Network Settings](https://cloud.tencent.com/document/product/457/9083).
 - **Container network**: Assign IP addresses within the container network address range to the containers in the cluster. For more information, see [Container and Node Network Settings](https://cloud.tencent.com/document/product/457/9083).
 - **Cluster description**: Enter the information about the cluster, which will be displayed on the **Cluster information** page.
 - **Advanced settings**: You can set IPVS.
 IPVS is well suited for scenarios where large-scale services will be run in the cluster and cannot be disabled once enabled. For more information, see [Enabling IPVS for a Cluster](https://cloud.tencent.com/document/product/457/32193).
5. Click **Next**.
6. In "Select a model", select the deployment mode and model. See the figure below:
 ![Select a model](https://main.qcloudimg.com/raw/d3357e6dec76b2501c08bd232f6243ac.png)
 Main parameters include:
 - **Master**: The deployment method of the "Master" determines the management mode of your cluster. Two cluster hosting modes are available. For more information, see [Cluster Hosting Mode Description](https://cloud.tencent.com/document/product/457/31013).
 - **Node**: "Node" configures the working node that is actually used to run the service in the cluster. You can purchase a CVM instance as a Node node when creating the cluster, or add a Node node after creating the cluster.
 - **Billing method**: Two billing methods are available: "prepaid" and "pay-as-you-go". For a detailed comparison, see [Billing Method](https://cloud.tencent.com/document/product/213/2180).
 - **Node model**: "Node" configures the working node that is actually used to run the service in the cluster. You can purchase a CVM instance as a Node node when creating the cluster, or add a Node node after creating the cluster.
    - **Availability zone**: You can select multiple availability zones at the same time to deploy your Master or Node nodes to ensure higher availability of the cluster.
    - **Node network**: You can select multiple subnet resources at the same time to deploy your Master or Node nodes to ensure higher availability of the cluster.
    - **Model**: For more information about how to select an appropriate model, see [Instance Type Overview](https://cloud.tencent.com/document/product/213/11518#.E5.8F.AF.E7.94.A8.E5.AE.9E.E4.BE.8B.E7.B1.BB.E5.9E.8B2) and [Selecting a CVM Configuration Scheme](https://cloud.tencent.com/document/product/213/2764#.E7.A1.AE.E5.AE.9A.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8.E9.85.8D.E7.BD.AE.E6.96.B9.E6.A1.88).
    - **System disk**: The default value is "Local disk - 50 GB". You can select local disk, HDD cloud disk, SSD cloud disk, or premium cloud disk based on actual needs. For more information about how to select a system disk, see [Storage Overview](https://cloud.tencent.com/document/product/213/4952).
    - **Data disk**: As it is recommended not to deploy other applications in the Master, no data disk is configured for it by default. You can add a cloud disk to it after purchase. You can configure a data disk for the Node at the time of purchase.
    - **Public network bandwidth**: Select **Public network access** and the system will assign a public IP for free. Two billing methods are available. For a detailed comparison, see [Public Network Billing Method](https://cloud.tencent.com/document/product/213/10578).
7. <span id="step7">Click **Next**. </span>
8. In "CVM configuration", configure other settings for the CVM instance. See the figure below:
![CVM configuration](https://main.qcloudimg.com/raw/6f1a1f36812d3379f721e73575761fef.png)
Main parameters include:
 - **OS**: An OS version adjusted and verified for compatibility is provided by default. If you use a GPU model, please select an OS appropriate for the GPU.
 - **Security group**: The security group has a firewall feature used to set the network access control of the CVM instance. See [TKE Security Group Settings](https://cloud.tencent.com/document/product/457/9084).
 - **Login method**: Three login methods are available.
   - **Set a password**: Set a corresponding password as prompted.
   - **Associate a key now**: A key pair is a pair of parameters generated by an algorithm. It is a way to log in to a CVM instance more secure than regular passwords. For details, see [SSH Key](https://cloud.tencent.com/document/product/213/6092).
   - **Generate a password automatically**: A password will be automatically generated and sent to you through internal message.
 - **Automatic adjustment**: A scaling group with a maximum of 2 nodes can be created automatically.
9. Click **Next** to check and confirm the configuration information.
10. Click **Finish** to complete the creation.


## Notes on the OS

- The OS is configured at the cluster level and determines the OS used after subsequently creating a node, creating a security group, adding an existing node, upgrading a node in the cluster.
- Change of the OS only takes effects for newly added or reinstalled nodes, but not existing nodes.
- Currently, you can only change the OS of the same type, for example, CentOS > CentOS-type custom image.
- To use the custom image feature, please apply by [submitting a ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&level3_id=718&radio_title=%E5%AE%B9%E5%99%A8%E9%9B%86%E7%BE%A4%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98&queue=97&scene_code=16798&step=2).

>! If you use the custom image feature, please create custom images based on the basic image provided by TKE.

