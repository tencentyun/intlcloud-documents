## Overview

This document describes how to create instances and topics in the CKafka console.

## Directions

### Creating an instance

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** in the left navigation pane and click **Create** to enter the instance purchase page.
3. On the purchase page, set the purchasing parameters.
	 ![](https://main.qcloudimg.com/raw/2a104de4c0aa47c3488982cff53c80c5.png)
  - Billing Mode: pay as you go
   
  - Region: select a region close to the resources of the client that is to deploy CKafka.
  - AZ: select an AZ based on your actual conditions.
    - The standard edition does not support cross-AZ deployment.
  - Product Specification: select a model based on your peak bandwidth and disk capacity
  - Message Retention: enter a period in minutes, which can range from 1 minute to 90 days
  >?After a message retention period is set, messages will be deleted if the period is reached. CKafka does not delete messages immediately upon expiration, but in batches by segment. The current segment size of CKafka is 1 GB, and a segment will not be deleted until its size reaches 1 GB. If the retention period is set to 1 minute, but the data size of a segment does not grow to 1 GB in 1 minute, then the retention period parameter will not take effect. We recommend that you increase the period depending on the speed of your data accumulation.
  - VPC: if you need to access other VPCs, you can modify the routing access rules as instructed in [Adding a Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555).
  - Purchase Duration: you can set to have your plan renewed automatically by month.
4. Click **Buy Now** to complete the creation.
 ![](https://main.qcloudimg.com/raw/50a3e41cb33313b32b5950b947f42c8f.png)


### Creating a topic

1. Click **Instance List** in the left navigation pane and click the **ID/Name** of your instance to enter the instance details page.
2. On the instance details page, select **Topic Management**, and click **Create**.
3. In the *Create Topic* window, set the number of partitions and replicas and other parameters.
![](https://main.qcloudimg.com/raw/c1b15cf8342af0078adc2517d6d017f4.png)
  - Name: the topic name, which cannot be changed once entered and can contain only letters, digits, “_”, “-” and “.”.
  - Partition Count: partition is the actual unit of storage. A topic can contain one or multiple partitions. CKafka allocates resources by partition.
  - Replica Count: the number of partition replicas, which ensure the availability of partitions. For the sake of data reliability, CKafka does not support single-replica topics currently. 2 replicas are created by default.
    Replicas are counted into the number of partitions too. For example, if you create 1 topic with 6 partitions, and 2 replicas, then there will be a total of 1 x 6 x 2=12 partitions.
  - Allowlist: if the allowlist is enabled, the topic can be accessed only from IP addresses in the allowlist, which ensures data security. You can enable allowlist in either the **Create Topic** or **Edit Topic** window.
4. Click **Submit** to complete the creation.
![](https://main.qcloudimg.com/raw/bbbdcab40f72d74991daf36322fce38b.png)
