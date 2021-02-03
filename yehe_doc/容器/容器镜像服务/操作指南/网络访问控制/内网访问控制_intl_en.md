## Overview
Tencent Container Registry (TCR) Enterprise Edition supports private-network access control. A Virtual Private Cloud (VPC) access link can be used to restrict instance access by clients in the VPC. In actual production scenarios involving container computing, pulling container images through the VPC can effectively improve the pulling speed and reduce public-network bandwidth costs. TCR allows users to connect their VPCs to a TCR Enterprise Edition instance to implement private-network access and access control.
This document describes how to configure private-network access control for a TCR Enterprise Edition instance.

## Prerequisites

Before configuring private-network access control for a TCR Enterprise Edition instance, complete the following tasks:
- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must grant the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).
- Activate the [VPC](https://console.cloud.tencent.com/vpc) service and create a VPC and subnet in the region where the TCR Enterprise Edition instance is deployed.

## Directions
### Creating an access link
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and choose **Access Control** > **Private Network** in the left sidebar.
2. On the "Private Network" page, click **Create**.
3. In the "Create Private Network Access Link" window that appears, configure the VPC and subnet information, as shown in the figure below.
![](https://main.qcloudimg.com/raw/b05dbba1213da652a4dcc2039b2ee38c.png)
  - **Instance**: target instance, for which the private network access is enabled. You can change the instance by going to the **Instance** drop-down list at the top of the **Private network** page.
 - **Virtual Private Cloud**:
    1. Connected VPC. Select the VPC that you want to connect. The drop-down list displays all available VPCs in the region of the current instance.
    2. Any subnet in the VPC. Select a subnet in the VPC that has usable private IP addresses. Creating a VPC access link occupies a private IP address and uses this IP address as the destination address for private-network resolution of the instance domain name. The subnet will be used only for the allocation of private network access addresses. After the link is created, CVMs in any subnet in the VPC can access the TCR Enterprise Edition instance through the link.
4. Click **OK** to start creating the VPC access link.
If "Access Linkage Status" becomes **Normal linkage** and "Private network parse IP" is not empty, the private network access link was successfully created.
![](https://main.qcloudimg.com/raw/4937a7031e5ab8c9e748a13206221153.png)

### Configuring private-network resolution
After the private-network access link is established, CVMs in the associated VPC can access the instance through the private network by accessing the private-network resolution IP address. By default, the default domain name of the instance (for example, tcr-demo.tencentcloudcr.com) and private network domain name (for example, tcr-demo-vpc.tencentcloudcr.com) will not be automatically resolved to the private-network resolution IP address in the VPC. You can implement private-network domain name resolution by [using the TCR plug-in for automatic configuration](#TCR) or [using the VPC resolution VPCDNS for automatic configuration](#VPCDNS).
<span id="TCR"></span>
#### Using the TCR plug-in for automatic configuration (recommended)
If you are using TKE, refer to [Using a Container Image in a TCR Enterprise Edition Instance to Create a Workload](https://intl.cloud.tencent.com/document/product/457/36838) to install the TCR plug-in in the TKE cluster. This plug-in can automatically configure private-network resolution for the associated TCR instance for nodes in the cluster. This enables secret-free pulling of images in the instance through the private network, as shown in the figure below:
![](https://main.qcloudimg.com/raw/85b74261a8b539f627b96139f5571611.png)
<span id="VPCDNS"></span>

#### Using VPC resolution VPCDNS for automatic configuration (beta)
>? Tencent Cloud DNS resolution DNSPod provides the VPC resolution feature, which supports resolution within a specified VPC. This feature is now available for trial use in the Beijing, Shanghai, Guangzhou, and Silicon Valley regions.

You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for trial use of this feature and provide the list of VPCs for which you want to enable this feature. After this service is activated, you can configure automatic resolution in the associated VPC of an instance after creating a private-network access link. In addition, you can select the default domain name or private domain name to use, as shown in the figure below:
![](https://main.qcloudimg.com/raw/cf1498ae284fe0c2c26684b479fbca81.png)

#### Manually configuring the CVM host 
This solution is applicable to CVMs or nodes in self-built Kubernetes clusters in VPCs that need to access an Enterprise Edition instance temporarily.
Here, a Linux CVM is used as an example. Log in to the CVM and run the following command:
```
echo '172.21.17.69 demo.tencentcloudcr.com' >> /etc/hosts
```
Replace `172.21.17.69` and `demo.tencentcloudcr.com` with your actual private-network resolution IP address and TCR instance domain name.
