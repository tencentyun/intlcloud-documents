## Overview
Tencent Container Registry (TCR) Enterprise Edition supports private network access control. A private network access link can be used to restrict instance access by clients in a Virtual Private Cloud (VPC). In actual production scenarios involving container computing, pulling container images through a VPC can effectively improve the pulling speed and reduce public network bandwidth costs. TCR allows users to connect their VPCs to a TCR enterprise edition instance to implement private network access and access control.

This document describes how to configure private network access control for a TCR enterprise edition instance. After completing the following configuration, you can use a CVM in a specified VPC to pull images from a TCR instance through the private network, or pull container images in TKE and other container clusters through the cluster private network. For more information, see [TKE Clusters Use the TCR Plug-In to Enable Secret-Free Pulling of Container Images Through the Private Network](https://intl.cloud.tencent.com/document/product/1051/38386).

## Prerequisites

Before configuring private network access control for a TCR enterprise edition instance, complete the following tasks:
- [Create an enterprise edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).
- Activate the [VPC](https://console.cloud.tencent.com/vpc) service and create a VPC and subnet in the region where the TCR enterprise edition instance is deployed.

## Directions
### Creating an access link
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and choose **Network ACL** > **Private network** in the left sidebar.
2. On the "Private network" page, click **Create**.
3. In the "Create a private network access linkage" window that appears, configure the VPC and subnet information, as shown in the figure below.
![](https://main.qcloudimg.com/raw/abd0607d3866119e3b9dd78e2bcbebf7.png)
 - **Associated Instance**: the target instance, for which the private network access policy is configured. To change the instance, select another instance name from the "Instance Name" drop-down list at the top of the "Private network" page.
 - **Region**: the region where the VPC to access resides, which is the same as the region where the current instance is deployed by default. If the multi-region replication feature is enabled for the current instance and replicas are configured for the instance in multiple regions, you can select the region where a replica is deployed to access the VPC of the replica.
 - **Virtual Private Cloud**:
    - The connected VPC. Select the VPC that you want to connect with. The drop-down list displays all available VPCs in the region of the current instance.
    - Any subnet in the VPC. Select a subnet with usable private IP addresses in the VPC. Creating a private network access link occupies a private IP address in the subnet. The IP address is also used as the destination IP address for private network resolution of the instance domain name. The subnet is only used to assign private network access addresses. After the link is created, CVMs in subnets of the VPC can access the TCR enterprise edition instance through the link.
4. Click **OK** to start creating the private network access link.
If "Access Linkage Status" changes to **Normal linkage** and "Private network parse IP" is not empty, the private network access link was successfully created.
![](https://main.qcloudimg.com/raw/4937a7031e5ab8c9e748a13206221153.png)

### Managing private network resolution
After the private network access link is established, CVMs in the associated VPC access the instance through the private network by accessing the private network resolution IP address. By default, the default domain name of the instance (for example, tcr-demo.tencentcloudcr.com) and private network domain name (for example, tcr-demo-vpc.tencentcloudcr.com) will not be automatically resolved to the private network resolution IP address in the VPC. You can implement private network domain name resolution by [using the VPCDNS for automatic configuration](#VPCDNS) or [using the TCR plug-in for automatic configuration](#TCR).



>! To use the TCR service in Chinese regions (excluding financial regions), we recommend you use the VPCDNS to manage the private network resolution of instance domain names. If the VPCDNS feature is not available in your region, use the TCR plug-in (recommended for TKE users) or manually configure the CVM host (temporary configuration).


<span id="VPCDNS"></span>


#### Using VPCDNS for automatic configuration (default methhod)
Tencent Cloud DNS resolution feature DNSPod provides a [VPC resolution](https://console.cloud.tencent.com/cns/private) feature to create private zones for VPC dedicated domain name resolution. This feature is now available in the Beijing, Shanghai, Guangzhou, Chongqing, Chengdu, and Hong Kong regions.
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and choose **Network ACL** > **Private network** in the left sidebar.
2. On the "Private network" page, click **Manage Auto-parsing** next to the created private network access link.
3. In the "Manage Auto-parsing" window that appears, configure domain name resolution for the link, as shown in the figure below.
![](https://main.qcloudimg.com/raw/16eec3cf0331453eee3fb9f0eb21f8ab.png)
 - **Default Domain Name**: the default domain name allocated to a created instance. If the public network access entry is enabled, the domain name will be resolved to a public IP address in the public network. You can continue to use the default domain name in the private network and enable automatic resolution of the default domain name. After it is enabled, the domain name will be automatically resolved to a private IP address in the private network.
 - **VPC Domain Name**: the dedicated domain name for VPCs. You can use this dedicated domain name in VPCs to distinguish it from the default domain name used in public networks. By default, the image repository provides the access address of the default domain name and related operation instructions. If you use a VPC dedicated domain name, modify the access address configuration of the image repository.
4. Click **Close**.

<span id="TCR"></span>

#### Using the TCR plug-in for automatic configuration (recommended for TKE users)

If you are using TKE, refer to [TCR](https://intl.cloud.tencent.com/document/product/457/38710) to install the TCR plug-in in the TKE cluster and select "Enable Private Network Parsing" in the "TCR Component Parameter Setting" window. For nodes in the cluster, this plug-in can automatically configure private network resolution for the associated TCR instance. This enables secret-free pulling of images in the instance through the private network.

#### Manually configuring the CVM host (temporary configuration)
This solution is applicable to CVMs or nodes located in self-built Kubernetes clusters in VPCs that require temporary access to TCR enterprise edition instances.
Here, a Linux CVM is used as an example. Log in to the CVM and run the following command:
```
echo '172.16.1.95 techo-demo.tencentcloudcr.com' >> /etc/hosts
```
Replace `172.21.17.69` and `demo.tencentcloudcr.com` with the private network resolution IP address and TCR instance domain name that you use.
