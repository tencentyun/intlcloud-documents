## Overview

This document describes how to create a topic under an existing instance in the CKafka console.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the **Instance List** page, click the ID of the instance created in [step 1](https://intl.cloud.tencent.com/document/product/597/40043) to go to the instance details page.
3. On the instance details page, click the **Topic Management** tab and click **Create**.
4. In the **Create Topic** dialog box, set parameters as needed.
   ![](https://main.qcloudimg.com/raw/a0a6444b0bb665691a1e4c61ff1114ec.png)
  - Name: topic name, which cannot be changed once entered and can contain only letters, digits, underscores (_), hyphens (-), and dots (.).
  - Partition Count: number of partitions (physical). A topic can contain one or multiple partitions. CKafka allocates resources by partition.
  - Replica Count: number of partition replicas, which ensure the availability of partitions. For data reliability concerns, CKafka does not support single-replica topics currently. Two replicas are created for each partition by default.
    Replicas are also counted into the number of partitions. For example, if you create 1 topic with 6 partitions, and 2 replicas for each partition, then you have a total of 12 partitions (1 x 6 x 2).
  - Allowlist: if the allowlist is enabled, the topic can be accessed only from IP addresses in the allowlist, which ensures data security. You can enable allowlist in either the **Create Topic** or **Edit Topic** window.
4. Click **Submit**.
