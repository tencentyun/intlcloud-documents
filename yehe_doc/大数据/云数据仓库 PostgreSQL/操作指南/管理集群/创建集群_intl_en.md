## Overview
This document describes how to create a cluster in the CDWPG console.

## Directions
1. Log in to the [CDWPG console](https://console.cloud.tencent.com/cdw) and select the cluster list.
2. Click **Create** to enter the purchase page and configure the parameters as prompted.
 - **Billing Mode**: Monthly subscription and pay-as-you-go billing are supported.                              
 - **Region**: Guangzhou, Shanghai, Beijing, and Singapore regions are supported currently.     
 - **AZ**: Different AZs are not interconnected.        
 - **Network**: Configure the VPC and subnet of the CDWPG cluster as instructed in [VPC](https://console.cloud.tencent.com/vpc/vpc?rid=5).For access from other subnets or public network, see [Applying for Public IP](https://intl.cloud.tencent.com/document/product/1138/45132) and [Creating IP Allowlist](https://intl.cloud.tencent.com/document/product/1138/45133). 
 - **Cluster Name**: Used to distinguish between clusters.
 - **Cluster Version**: Versions supported by the cluster.
 - **Node Type**: nc.large, nc.4xlarge, nc2.large, nc2.4xlarge, ns.large, and ns2.large are currently available. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1138/45140).  
 - **Number of Nodes**: 2–50 nodes are supported. Generally, two or more (50 at maximum) nodes are required.       
 - **Database Port**: 5436, which cannot be modified currently.    
 - **Username**: Username to log in to the CDWPG cluster, which is the cluster admin account and cannot be changed after creation. 
 - **Password**: Password to log in to the CDWPG cluster, which can be changed in the console.
![](https://qcloudimg.tencent-cloud.cn/raw/61a02e8b417153aa0ac5ca21b3fb70da.png)

3. After completing the configuration, click **Buy Now** or **Activate** to create the cluster.
4. Return to the cluster list and use the cluster after its status changes to **Running**.

