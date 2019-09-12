## Operation Scenario

When creating a cluster, you can use both new CVMs and existing CVMs as the initial nodes. This article guides you through these two cluster creation methods.

## Notes on the OS

- Change to the OS only take effect for newly added or reinstalled nodes, but not for existing nodes.
- Currently, you can only change an OS to one of the same type, for example, CentOS > CentOS-type custom image.
- To use the custom image feature, apply by [Submitting a Ticket](https://console.qcloud.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&level3_id=718&radio_title=%E5%AE%B9%E5%99%A8%E9%9B%86%E7%BE%A4%E7%9B%B8%E5%85%B3%E9%97%AE%E9%A2%98&queue=97&scene_code=16798&step=2).

> If you use the custom image feature, create custom images based on the basic image provided by TKE.

## Directions

### Entering Cluster Information

1. <span id="step1">Log in to the [TKE Console](https://console.cloud.tencent.com/tke2). </span>
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. On the cluster management page, click **Create**. this is shown in the following figure:
   ![](https://main.qcloudimg.com/raw/5d4bc55fd7ad81ffb15c4acb5537cb02.png)
4. On the **Create a Cluster** page, configure the basic information of the cluster. This is shown in the following figure:
   ![Create a Cluster](https://main.qcloudimg.com/raw/39c59f047d281cbd2d390c3c92f16d0a.png)

- **Cluster Name**: The name of the cluster to be created, with a length limited to 60 characters.
- **Project**: Select based on actual needs. Newly added resources will be automatically assigned to this project.
- ** Kubernetes Version**: Multiple Kubernetes versions are provided. For a comparison of the features of different versions, see [Supported Versions of Kubernetes Documentation](https://kubernetes.io/docs/home/supported-doc-versions/).
- **Region**: Select the closest region based on your location. This helps minimize access latency and improve download speed.
- **Cluster Network**: Assigns an IP address that is within the node’s network address range to the CVMs in the cluster. For details, see [Container and Node Network Configuration](https://intl.cloud.tencent.com/document/product/457/9083).
- **Container Network**: Assigns an IP address that is within the container’s network address range to the containers in the cluster. For details, see [Container and Node Network Configuration](https://intl.cloud.tencent.com/document/product/457/9083).
- **Cluster Description**: Enter the information about the cluster, which will be displayed on the **Cluster Information** page.
- **Advanced Settings**: You can set IPVS.
  IPVS is suitable for scenarios where large-scale services are run in a cluster. It cannot be disabled after being enabled. For operation details, see [Enabling IPVS in a Cluster](https://intl.cloud.tencent.com/document/product/457/30641).

5. Click **Next**.

## Selecting a Model

6. In **Select a Model**, determine whether to create a cluster using an existing CVM. This is shown in the following figure:
   ![](https://main.qcloudimg.com/raw/66cb674ce01a0b687396db7baed50bc4.png)

- Check **Create a cluster using existing CVMs** if you want to [create a cluster using existing CVMs](#UseExistingCVMCreateCluster).
- Uncheck **Create a cluster using existing CVMs** if you [don’t want to use existing CVMs to create a cluster](#NotUseExistingCVMCreateCluster).

<span id="UseExistingCVMCreateCluster"></span>

#### Using an Existing CVM to Create a Cluster

> When using an existing CVM to create a cluster, you must pay attention to the following points:
>
> - The selected CVM must be reinstalled. After reinstallation, the data on the CVM system disk will be erased.
> - The selected CVM will be migrated to the project to which the cluster belongs.
> - Migrating a CVM to another project will cause the original security group to be unbound. You must rebind the security group.

7. In **Select a model**, select the deployment mode and model. This is shown in the following figure:
   ![](https://main.qcloudimg.com/raw/1b873fd0387c8243bacbaff27aeeabd5.png)
    Main parameters include:

- **Master**: The deployment method of `Master` determines the management mode for your cluster. We provide two cluster hosting modes you can choose from. For more information, see [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635).
- **Node**: Node configured here is the worker node that is actually used by the cluster to run services. You can purchase a CVM as the node when you create the cluster, or you can add the node after the cluster creation.
- **Master&Etcd Model**: Select the CVM according to the following requirements.
  -The selected CVM must have at least 4-core CPU, and at least 3 CVMs must be selected.
  - The CVM cannot be the node of another TKE cluster.
  - The CVM status must be **Running**.
  - You can select across availability zones. 
- **Node Model**: This can be selected when **Node** is selected as **Add New**. You can also add a node after the cluster is created.

8. Click **Next**, [Configure the CVM](#ConfigureCVM).

<span id="NotUseExistingCVMCreateCluster"></span>

#### Not Using an Existing CVM to Create a Cluster

9. In **Select a model**, select the deployment mode and model. This is shown in the following figure:
   ![Select a model](https://main.qcloudimg.com/raw/d4f5410e1a85e2e5cc89cc0fe4658060.png)
    Main parameters include:

- **Master**: The deployment method of `Master` determines the management mode for your cluster. We provide two cluster hosting modes you can choose from. For more information, see [Cluster Overview](https://intl.cloud.tencent.com/document/product/457/30635).
- **Node**: The node configured here is the worker node that is actually used by the cluster to run services. You can purchase a CVM as the node when you create the cluster, or you can add the nodes after the cluster creation.
- **Billing Mode**: This provides the **Pay as you go** billing mode. For more  information, see [Billing Mode](https://intl.cloud.tencent.com/document/product/213/2180).
- **Master&Etcd Model**:
  - **Availability Zone**: You can select multiple availability zones at the same time to deploy your `Master` or `Etcd` to ensure the higher availability of the cluster.
  - **Node Network**: You can select multiple subnets at the same time to deploy your `Master` or `Etcd` to ensure the higher availability of the cluster.
  - **Model**: Select a model with at least 4-core CPU. For more information about how to select an appropriate model, see [Instance Type Overview](https://intl.cloud.tencent.com/document/product/213/11518#.E5.8F.AF.E7.94.A8.E5.AE.9E.E4.BE.8B.E7.B1.BB.E5.9E.8B2) and [Selecting a CVM Configuration Scheme](https://intl.cloud.tencent.com/document/product/213/2764#.E7.A1.AE.E5.AE.9A.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8.E9.85.8D.E7.BD.AE.E6.96.B9.E6.A1.88).
  - **System Disk**: You can select a local disk, HDD cloud disk, SSD cloud disk, or premium cloud disk according to the availability zone and model. For more information about storage media selections, see [Storage Overview](https://intl.cloud.tencent.com/document/product/213/4952).
  - **Data disk**: As it is recommended not to deploy other applications in the `Master` and `Etcd`, no data disk is configured for it by default. You can add a cloud disk to it after purchase.
  - **Public network bandwidth**: Select **Assign Free Public IP** and the system will assign a public IP for free. Bill-by-traffic mode is provided. For more information, see [Public Network Billing Method](https://intl.cloud.tencent.com/document/product/213/10578).
- **Node Model**: This can be selected when **Node** is selected as **Add New**.
  - **Availability Zone**: You can select multiple availability zones at the same time to deploy your `Master` or `Etcd` nodes to ensure the higher availability of the cluster.
  - **Node Network**: You can select multiple subnet resources at the same time to deploy your `Master` or `Etcd` nodes to ensure the higher availability of the cluster.
  - **Model**: For information about how to select a model, see [Instance Type Overview](https://intl.cloud.tencent.com/document/product/213/11518#.E5.8F.AF.E7.94.A8.E5.AE.9E.E4.BE.8B.E7.B1.BB.E5.9E.8B2) and [Selecting a CVM Configuration Scheme](https://intl.cloud.tencent.com/document/product/213/2764#.E7.A1.AE.E5.AE.9A.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8.E9.85.8D.E7.BD.AE.E6.96.B9.E6.A1.88).
  - **System Disk**: You can select a local disk, HDD cloud disk, SSD cloud disk, or premium cloud disk according to the availability zone and model. For more information about storage media selections, see [Storage Overview](https://intl.cloud.tencent.com/document/product/213/4952).
  - **Data disk**: As it is recommended not to deploy other applications in the `Master`, no data disk is configured for it by default. You can add a cloud disk to it after purchase. You can configure the data disk while purchasing a node.
  - **Public network bandwidth**: Select **Assign Free Public IP** and the system will assign a public IP for free. Bill-by-traffic mode is provided. For more information, see [Public Network Billing Method](https://intl.cloud.tencent.com/document/product/213/10578).
  - **Number**：Set to >=3 units.

10. <span id="step7">Click **Next**, [Configure CVM](#ConfigureCVM).</span>

<span id="ConfigureCVM"></span>

### Configuring a CVM

11. In **CVM Configuration**, configure the CVM. This is shown in the following figure:
    ![CVM Configuration](https://main.qcloudimg.com/raw/649cbb0a1ffe56e7cc7689aaa74de5a8.png)
    Main parameters include:

- **Data Disk Mounting**: Selected by default.
- **Security Group**: The security group has a firewall functions, which is used to set the network access control for the CVM. For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
- **Login Method**: Three login methods are available.
  - **Set a Password**: Set a corresponding password as prompted.
  - **SSH Key Pair**: A key pair is a pair of parameters generated by an algorithm. It is a more secure way to log in to a CVM instance than regular passwords. For more information, see [SSH Key](https://cloud.tencent.com/document/product/213/6092).
  - **Random Password**: A password will be automatically generated and sent to you through internal message.
- **Automatic Adjustment**: A scaling group with a maximum of 2 nodes can be created automatically.

12. Click **Next** to check and confirm the configuration information.
13. Click **Finish**.

