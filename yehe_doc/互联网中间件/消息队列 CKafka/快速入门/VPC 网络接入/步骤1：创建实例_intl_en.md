## Overview
This document describes how to create an instance and deploy a VPC via the CKafka console.


## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- You have [created a VPC](https://intl.cloud.tencent.com/document/product/215/31805).

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Select **Instance List** on the left sidebar, click **Create** to go to the instance purchase page, and enter the purchase information as needed.
   - Billing Mode: monthly subscription.
   - Specs Type: select the Standard or Pro Edition based on your business needs.
   - Kafka Version: select a Kafka version based on your business needs. For more information, please see [Suggestions for CKafka Edition Selection](https://cloud.tencent.com/document/product/597/57243).
   - Region: select a region close to the resource for client deployment.
   - AZ:
     - Standard Edition: it does not support multi-AZ deployment.
     - Pro Edition: if the current region supports multi-AZ deployment, you can select up to 2 AZs for deployment. For more information on how multi-AZ deployment works, please see [Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/597/40243).
   - Product Specs: select an appropriate model based on the peak bandwidth and disk capacity.
   - Message Retention: select a value between 24 and 2160 hours.
     When the disk capacity is insufficient (i.e., the disk utilization reaches 90%), old messages will be deleted in advance to ensure the service availability.
3. Select the VPC where the CVM instance resides.
   If you need to access other VPCs, you can modify routing access rules as instructed in [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555).
4. Click **Buy Now**. The created instance will be displayed in the instance list in about 3–5 minutes.
