## Overview

This document describes how to implement mutual access between the resources in your current VPC and TDMQ for Pulsar, so as to ensure that the deployed producer/consumer clients can properly communicate with TDMQ for Pulsar.

> ?Currently, only clusters on v2.6.1 require configuring an access point, and for clusters on v2.7.1 or above, you can directly copy the access address from the **Cluster Management** page in the console. For directions, see [Getting Access Address](https://intl.cloud.tencent.com/document/product/1110/42928).

## Prerequisites

You have purchased CVM or TKE resources and configured a VPC.

## Directions

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq), enter the **Cluster Management** page, and select the target cluster.
2. Click **Access Address** in the **Operation** column to enter the access point configuration page of the cluster.
  ![](https://qcloudimg.tencent-cloud.cn/raw/17f1b8410d6c38d0c5dcc3d7a6ab4333.png)
3. Click **Create**. Then, select the VPC and subnet and enter the remarks in the VPC access point creation window.
	- VPC: select the VPC of the deployed producer or consumer.
	- Subnet: select an appropriate subnet according to your IP allocation method.
	- Remarks (optional): enter the remarks of up to 128 characters.
4. Click **Submit**.
5. Configure a security group policy.
   Make sure that the security group of the test program has opened TCP ports 6000–7000.

You can see the created access point in the access point list, which contains the parameters to be configured in the client (route ID and address). For more information, see the [SDK documentation](https://intl.cloud.tencent.com/document/product/1110/42945).

