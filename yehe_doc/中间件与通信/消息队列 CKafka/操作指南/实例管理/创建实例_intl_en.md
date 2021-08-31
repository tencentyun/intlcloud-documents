## Overview

This document describes how to create instances and topics in the CKafka console.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click **Create** to enter the instance purchase page.
3. On the instance purchase page, set the configuration information for purchase based on your actual needs.
   - Billing Mode: monthly subscription
   - Specs Type: select the Standard or Pro Edition based on your business needs.
   - Kafka Version: select a Kafka version based on your business needs. For more information, please see [Suggestions for CKafka Edition Selection](https://intl.cloud.tencent.com/document/product/597/40964).
   - Region: select a region close to the resource for client deployment.
   - AZ: select an AZ according to your actual needs.
     - Standard Edition: it does not support multi-AZ deployment.
     - Pro Edition: if the current region supports multi-AZ deployment, you can select up to 2 AZs for deployment. For more information on how multi-AZ deployment works, please see [Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/597/40243).
   - Product Specs: select an appropriate model based on the peak bandwidth and disk capacity.
   - Message Retention: select a value between 24 and 2160 hours.
     When the disk capacity is insufficient (i.e., the disk utilization reaches 90%), old messages will be deleted in advance to ensure the service availability.
   - VPC: if you need to access other VPCs, you can modify routing access rules as instructed in [Adding a Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555).
   - Tag: it is optional. For specific usage, please see [Tag Overview](https://cloud.tencent.com/document/product/597/33355).
   - Instance Name: when purchasing multiple instances, you can use the features of automatically incrementing the instance suffix number and specifying a pattern string. For detailed directions, please see [Consecutive Batch Naming or Naming with Pattern String](https://cloud.tencent.com/document/product/597/59246)

4. Click **Buy Now** to complete the instance creation process.
   ![](https://main.qcloudimg.com/raw/d7df4ac342594f0016e57878921ba06d.png)
