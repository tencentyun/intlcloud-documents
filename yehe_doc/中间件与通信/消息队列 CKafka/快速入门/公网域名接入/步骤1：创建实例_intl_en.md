## Overview

This document describes how to create an instance and deploy a VPC via the CKafka console.

## Prerequisites

- You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- You have [created a VPC](https://intl.cloud.tencent.com/document/product/215/31805).

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Choose **Instance List** in the left sidebar, click **Create** to go to the instance purchase page, and enter the purchase information as needed.
   - Billing Mode: monthly subscription
   - Specs Type: select the Standard or Pro edition based on your business needs.
   - Kafka Version: select a Kafka version based on your business needs. For more information, please see [Suggestions for CKafka Edition Selection](https://intl.cloud.tencent.com/document/product/597/40964).
   - Region: select a region close to the resource for client deployment.
   - AZ:
     - Standard Edition: does not support multi-AZ deployment.
     - Pro Edition: if the current region supports multi-AZ deployment, you can select up to 2 AZs for deployment. For more information on multi-AZ deployment, please see [Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/597/40243).
   - Product Specification: select a model based on the peak bandwidth and disk capacity.
   - Message Retention: select a value between 24 and 2160 hours.
     When the disk capacity is insufficient (i.e., the disk utilization reaches 90%), old messages will be deleted in advance to ensure the service availability.
   - VPC: select the created VPC.
   - Instance name: when purchasing multiple instances, you can batch create instances by its numeric suffix (which is numbered in an ascending order) or its designated pattern string. For specific operations, please see [Naming with Consecutive Numeric Suffixes or Designated Pattern String](https://cloud.tencent.com/document/product/597/59246).
3. Click **Buy Now**. The instance created is displayed in the instance list in about 3-5 minutes.


