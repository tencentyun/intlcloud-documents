
This document describes how to purchase a CTSDB instance in the console.

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
1. Log in to the [CTSDB purchase page](https://buy.intl.cloud.tencent.com/ctsdb), configure the following instance information, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go
 - **Region and AZ**: select the region where to deploy your business. For more information, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/1100/40937).
 - **Configuration Mode**: select **QuickConfig** or **CustomConfig**.
 - **Storage Capacity**: in the QuickConfig mode, the storage (i.e., storage capacity per replica) = total disk capacity of the cluster / number of replicas.
 - **Network**: VPC is supported. We recommend you choose the same VPC in the same region as your CVM instance. For more information, see [Network Environment](https://intl.cloud.tencent.com/document/product/213/5227).
 - **Project**: select a project to which the instance belongs. The default project is used. 
 - **Fees**: for more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1100/40934). 
2. After the purchase is completed, you will be redirected to the instance list. After the status of the instance becomes **Running**, it can be used normally.

## Relevant Documentation
[Connecting to Instance](https://intl.cloud.tencent.com/document/product/1100/40928)
