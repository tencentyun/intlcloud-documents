## Overview
This document describes how to create an instance and deploy a VPC in the CKafka console.


## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- You have [created a VPC](https://intl.cloud.tencent.com/document/product/215/31805).

## Directions

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Select **Instance List** on the left sidebar, click **Create** to go to the instance purchase page, and enter the purchase information as needed.
   - Billing Mode: Select **Monthly subscription** or **Pay as you go**.
   - Specs Type: Select the Standard or Pro Edition based on your business needs.
   - Kafka Version: Select a Kafka version based on your business needs. For more information, see [Suggestions for CKafka Version Selection](https://intl.cloud.tencent.com/document/product/597/40964).
   - Region: Select a region close to the resource for client deployment.
   - AZ:
     - Standard Edition: Does not support multi-AZ deployment.
     - Pro Edition: If the current region supports multi-AZ deployment, you can select up to two AZs for deployment. For more information on multi-AZ deployment, see [Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/597/40243).
   - Product Specs: Select an appropriate model based on the peak bandwidth and disk capacity.
   - Message Retention Period: The value range is 1–2160 hours.
     When the disk capacity is insufficient (i.e., the disk utilization reaches 90%), old messages will be deleted in advance to ensure the service availability.
   - Instance Name: When purchasing multiple instances, you can use the features of automatically incrementing the instance suffix number and specifying a pattern string. For detailed directions, see [Naming with Consecutive Numeric Suffixes or Designated Pattern String](https://intl.cloud.tencent.com/document/product/597/41581).
3. Select an appropriate VPC according to your business needs.
   If you want to use other VPCs, follow the steps in [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555) to modify the routing rules.
4. Click **Buy Now**. The created instance will be displayed in the instance list in about 3–5 minutes.
