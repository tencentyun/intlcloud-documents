
## Scenario
The Tencent Container Registry (TCR) Enterprise Edition supports private network access control. A Virtual Private Cloud (VPC) access link can be used to restrict instance access by clients in the VPC. In actual production scenarios involving container computing, pulling container images through the VPC can effectively improve the pulling speed and reduce public network bandwidth costs. TCR allows users to connect their VPCs to a TCR Enterprise Edition instance to implement private network access and access control.
This document describes how to configure private network access control for a TCR Enterprise Edition instance.

## Prerequisites

Before configuring private network access control for a TCR Enterprise Edition instance, complete the following tasks:
- Activate the [VPC](https://console.cloud.tencent.com/vpc) service and create a VPC and subnet in the region where the TCR Enterprise Edition instance is deployed.
- Activate the Domain Name Service (DNS) for the VPC in the [Tencent Cloud DNS](https://console.cloud.tencent.com/cns) console.

## Procedure
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and choose **Access Control** -> **Private network** in the left sidebar.
2. On the "Private network" page, click **Create**.
3. In the "Create Private Network Access Whitelist" window, configure the VPC and subnet information, as shown in the figure below.

 - **Associated Instance**: target instance, for which the private network access policy is configured. You can change the instance by selecting another instance name from the "Instance Name" drop-down list at the top of the "Private network" page.
 - **Virtual Private Cloud**: connected VPC. Select the VPC that you want to connect. The drop-down list displays all VPCs available in the region of the current instance.
 - **Subnet**: any subnet in the VPC. Select a subnet in the VPC that has usable private IP addresses. Creating a VPC access link will occupy a private IP address and use this IP address as the destination address for private network resolution of the instance domain name.
4. Click **OK** to start creating the VPC access link.
If "Access Linkage Status" changes to **Normal linkage**, and "Private network parse IP" is not empty, the VPC access link was successfully created.
5. Log in to the [Tencent Cloud DNS](https://console.cloud.tencent.com/cns) console and select **VPC** to go to the VPC resolution configuration page. Configure the resolution records of "Instance Domain Name" and "Private network parse IP" as prompted.
> Currently, VPC resolution is a beta feature of Tencent Cloud DNS. If this feature is not activated, you can configure these resolution records on a VPC node or in your own DNS service.


