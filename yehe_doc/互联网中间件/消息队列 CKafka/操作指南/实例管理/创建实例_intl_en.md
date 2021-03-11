## Overview

This document describes how to create instances in the CKafka console.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** in the left navigation pane and then click **Create** to enter the instance purchase page.
3. On the purchase page, enter the purchase information.
   ![](https://main.qcloudimg.com/raw/053e51b2105b9ac14f4eacdb33130bb2.png)
  - Billing Mode: pay as you go
   
    - The standard edition does not support cross-AZ deployment.
  - Region: select a region close to the resources of the client that is to deploy CKafka.
  - AZ: select an AZ based on your actual conditions.
  - Bandwidth Cap: choose the peak bandwidth based on your actual conditions.
  - Message Retention: 1-2,160 hours
   
  >
  - VPC: if you want to use other VPCs, follow the steps in [Adding a Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555) to modify the routing rules.
   
4. Click **Buy Now** to complete the creation.
   ![](https://main.qcloudimg.com/raw/38933dab24f3e9a16941609518d73c70.png)
