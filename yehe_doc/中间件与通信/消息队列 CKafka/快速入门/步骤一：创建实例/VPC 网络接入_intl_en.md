## Overview
This document describes how to create an instance and deploy a VPC via the CKafka console.


## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- You have [purchased a CVM](https://buy.cloud.tencent.com/cvm).
- You have [created a VPC](https://intl.cloud.tencent.com/document/product/215/31805).

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Choose **Instance List** in the left sidebar, click **Create** to go to the instance purchase page, and enter the purchase information as needed.
   - Billing Mode: monthly subscription
   - Specs Type: select the Standard or Pro edition based on your business needs.
   - Region: select a region close to the resource for client deployment.
   - AZ:
     - Standard Edition: does not support cross-AZ deployment.
     - Pro Edition: if the current region supports multi-AZ deployment, you can select up to 2 AZs for deployment. For more information on cross-AZ deployment, please see [Cross-AZ Deployment](https://intl.cloud.tencent.com/document/product/597/40243).
   - Product Specification: select a model based on the peak bandwidth and disk capacity.
   - Message Retention: the value must range from 24 hours to 2,160 hours.
     When the disk capacity is insufficient (i.e., the disk utilization reaches 90%), old messages will be deleted in advance to ensure the service availability.
3. Select the VPC where the CVM resides.
   To connect to another VPC, modify routing access rules as instructed in [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555).
4. Click **Buy Now**. The instance created is displayed in the instance list in about 3-5 minutes.
