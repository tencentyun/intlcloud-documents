## Overview

This document describes how to use the **Specification Calculator** in the CKafka console to find the appropriate CKafka instance specification for your self-built Kafka cluster that needs to be migrated to the cloud.

## Directions
1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the left sidebar, select **Cloud Migration**, select the region you want to migrate to, and click **Specification Calculator**.
3. Enter the specification of your self-built Kafka cluster on the specification calculator page.
	 ![](https://main.qcloudimg.com/raw/5bdcd2570f30c12f5bf3c47f628f27bd.png)


   | Parameter         | Description                                                         |
   | ------------ | ------------------------------------------------------------ |
   | Kafka Version | Select the version of your self-built Kafka cluster. For more information on CKafka version selection, please see [Suggestions for CKafka Version Selection](https://intl.cloud.tencent.com/document/product/597/40964). |
   | Business Peak Bandwidth | Business peak bandwidth = max (production peak bandwidth * number of replicas, consumption peak bandwidth). |
   | Disk | Estimate according to the current peak value of actual disk usage. |
   | Partitions | Total number of partitions of the topic to be migrated. Note that the number of replicas should be considered. For example, if one topic replica has 5 partitions, then two replicas have 10 partitions in total. CKafka does not support single-replica topics. |
   | Multi-AZ Deployment | Select whether to deploy in multiple AZs according to your business needs. For more information, please see [Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/597/40243). |
   | Data Compression | CKafka does not support the Gzip compression format. For more information, please see [Data Compression](https://intl.cloud.tencent.com/document/product/597/34004). |

4. Click **Next** to get the recommended CKafka instance specification.
5. Click **Buy This Configuration** to redirect to the instance purchase page.
6. Confirm the purchase information, click **Buy Now**, wait 5–10 minutes, and you can see that the instance is created on the instance list page.
	 ![](https://main.qcloudimg.com/raw/693bfe8e26d0bf9ad9ce72537a16cb5d.png)

