## Overview

To enable public network access, you need to add a public route for the instance. This document describes how to create an instance and add a public route for the instance.

## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- You have [purchased a CVM](https://buy.cloud.tencent.com/cvm).
- You have [created a VPC](https://intl.cloud.tencent.com/document/product/215/31805).

## Directions

### Step 1. create an instance

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
   - VPC: select the created VPC.
3. Click **Buy Now**. The instance created is displayed in the instance list in about 3-5 minutes.

### Step 2. Add a public route

1. In the instance list, click the ID of the created instance.
2. On the instance details page, in the **Access Mode** section, click **Add a routing policy** to add a public route.
   ![](https://main.qcloudimg.com/raw/dcb5bb0a6975a847067387d7730efa0d.png)
   Then you get the domain name and port for public network access.
   ![](https://main.qcloudimg.com/raw/71b6caefb12f44280d83b138df614845.png)

