## Overview

This document describes how to create a topic under an existing instance in the CKafka console.

## Directions


1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the **Instance List** page, click the **ID/Name** of the instance created in [step 1](https://intl.cloud.tencent.com/document/product/597/40044) to enter the **Instance Details** page.
3. On the **Instance Details** page, click **Topic Management** at the top and click **Create**.
4. In the **Edit Topic** window, set the number of partitions and replicas and other parameters.
      ![](https://main.qcloudimg.com/raw/b059e7bddbb29b16b9449e1dbbcf1b4d.png)
  - Name: the topic name, which cannot be changed once entered and can only contain letters, digits, underscores, hyphens, and dots.
  - Partition Count: it is a concept in physical partition, where one topic can contain one or more partitions. CKafka uses partition as an allocation unit.
  - Replica Count: the number of partition replicas is used to ensure the high availability of the partition. To ensure data reliability, creating a single-replica topic is not supported. Two replicas are enabled by default.
    Replicas are also counted into the number of partitions. For example, if you create 1 topic with 6 partitions, and 2 replicas for each partition, then you have a total of 12 partitions (1 x 6 x 2).
  - Allowlist: if the allowlist is enabled, the topic can be accessed only from IP addresses in the allowlist, which ensures data security. You can enable allowlist in either the **Create Topic** or **Edit Topic** window.
5. Click **Submit** to complete topic creation.

