## Overview
Tencent Container Registry (TCR) Enterprise Edition supports private network access control. A private network access link can be used to restrict instance access by clients in a Virtual Private Cloud (VPC). In actual production scenarios involving container computing, pulling container images through a VPC can effectively improve the pulling speed and reduce public network bandwidth costs. TCR allows users to connect their VPCs to a TCR Enterprise Edition instance to implement private network access and access control.

This document describes how to configure private network access control for a TCR Enterprise Edition instance. After completing the following configuration, you can use a CVM in a specified VPC to pull images from a TCR instance through the private network, or pull container images in TKE and other container clusters through the cluster private network. For more information, see [TKE Clusters Use the TCR Addon to Enable Secret-free Pulling of Container Images via Private Network](https://intl.cloud.tencent.com/document/product/1051/38386).

## Prerequisite

Before configuring private network access control for a TCR Enterprise Edition instance, complete the following tasks:
- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must have granted the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).
- Activate the [VPC](https://console.cloud.tencent.com/vpc) service and create a VPC and subnet in the region where the TCR Enterprise Edition instance is deployed.
- Activate [Private DNS](https://console.cloud.tencent.com/privatedns) service.

## Directions
### Creating an access link
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Access Control** > **Private Network Access** in the left sidebar.
2. On the "Private Network Access" page, click **Create**.
3. In the "Create a private network access linkage" window that appears, configure the VPC and subnet information, as shown in the figure below.
![](https://main.qcloudimg.com/raw/abd0607d3866119e3b9dd78e2bcbebf7.png)
 - **Associated Instance**: the target instance, for which the private network access policy is configured. To change the instance, select another instance name from the "Instance Name" drop-down list at the top of the "Private Network Access" page.
 - **Region**: the region where the VPC to access resides, which is the same as the region where the current instance is deployed by default. If the multi-region replication feature is enabled for the current instance and replicas are configured for the instance in multiple regions, you can select the region where a replica is deployed to access the VPC of the replica. For more information, see [Configuring Instance Replication](https://intl.cloud.tencent.com/document/product/1051/39845).
 - **Virtual Private Cloud**:
    - The connected VPC. Select the VPC that you want to connect with. The drop-down list displays all available VPCs in the region of the current instance.
    - Any subnet in the VPC. Select a subnet with usable private IP addresses in the VPC. Creating a private network access linkage occupies a private IP address in the subnet. The IP address is also used as the destination IP address for private network resolution of the instance domain name. The subnet is only used to assign private network access addresses. After the linkage is created, CVMs in subnets of the VPC can access the TCR Enterprise Edition instance through the linkage.
4. Click **OK** to start creating the private network access linkage.
If "Access Linkage Status" changes to **Normal linkage** and "Private network parse IP" is not empty, the private network access linkage was successfully created.
![](https://main.qcloudimg.com/raw/4937a7031e5ab8c9e748a13206221153.png)

<dx-alert infotype="notice" title="">
The access domain name of the instance is only configured resolution for public network access by default. After connecting to the specified VPC and obtaining the private network parse IP, click **Manage Auto-parsing** to configure the dedicated private network parsing for the instance domain name in the VPC.
</dx-alert>


### Managing private network parsing
After the private network access linkage is established, CVMs in the associated VPC access the instance through the private network by accessing the private network parse IP. By default, the default domain name of the instance (for example, tcr-demo.tencentcloudcr.com) and private network domain name (for example, tcr-demo-vpc.tencentcloudcr.com) will not be automatically resolved to the private network parse IP in the VPC. You need to use the **Manage Auto-parsing** feature to configure private network parsing, or use an external DNS service to manage it.

#### Using Private DNS for auto-configuring (default)[](id:PrivateDNS)
Tencent Cloud [Private DNS](https://console.cloud.tencent.com/privatedns) service is used to configure the domain name resolution in VPC by default. You need to activate the service before using this feature.
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Access Control** > **Private Network Access** in the left sidebar.
2. On the "Private Network Access" page, click **Manage Auto-parsing** next to the created private network access linkage.
3. In the "Manage Auto-parsing" window that appears, configure domain name resolution for the linkage, as shown in the figure below.
![](https://main.qcloudimg.com/raw/16eec3cf0331453eee3fb9f0eb21f8ab.png)
 - **DNS Service**: it indicates whether the current Private DNS service is activated. If the service is not activated, click **Activate Service** to activate it. No additional fees will be charged on the products using Private DNS service.
 - **Resolution Configuration**: it is disabled by default. You can click to enable the automatic resolution of default domain name. After enabling, the instance domain name will be resolved to the private IP x.x.x.x in the VPC instead of being resolved to a public IP address of the instance. The instance will be used to push and pull images in the private network without the need to configure the domain name resolution manually or by using the TCR add-on.
 - **Advanced Configuration**: you can configure the auto-parsing of VPC domain names. VPC domain names are dedicated domain names in VPCs. You can use a VPC domain name in VPCs to distinguish it from the default domain name used in public networks. By default, the image repository provides the access address of the default domain name and related operation instructions. If you use a VPC dedicated domain name, modify the access address configuration of the image repository.
4. Click **OK**.

#### Using TCR add-on for auto-configuring[](id:TCR)
This solution is applicable to the scenarios where Private DNS has not provided services in the region where the TKE cluster is located. It is not recommended by default.

If you are using TKE, refer to [TCR](https://intl.cloud.tencent.com/document/product/457/38710) to install the TCR add-on in the TKE cluster and select **Enable Private Network Parsing** in the **TCR Add-on Parameter Settings** window. For nodes in the cluster, this add-on can automatically configure private network parsing for the associated TCR instance. This enables secret-free pulling of images in the instance through the private network.

#### Manually configuring CVM host
This solution is applicable to CVMs or nodes located in self-built Kubernetes clusters in VPCs that require temporary access to TCR Enterprise Edition instances. It is not recommended by default.

Here, a Linux CVM is used as an example. Log in to the CVM and run the following command:
```
echo '172.16.1.95 techo-demo.tencentcloudcr.com' >> /etc/hosts
```
Replace `172.21.17.69` and `demo.tencentcloudcr.com` with the private network parse IP and TCR instance domain name that you use.
