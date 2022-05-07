## Overview

This document describes how to create a topic in a created instance in the CKafka console.

## Directions


1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the **Instance List** page, click the **ID/Name** of the instance created in [Step 1](https://intl.cloud.tencent.com/document/product/597/40044) to enter the instance details page.
3. On the instance details page, click **Topic Management** at the top and click **Create**.
4. In the **Create Topic** window, set the number of partitions and replicas and other parameters.
![](https://main.qcloudimg.com/raw/b059e7bddbb29b16b9449e1dbbcf1b4d.png)

   - Name: The topic name. It cannot be changed once entered and can contain only letters, digits, underscores, hyphens, and periods.
   - Partition Count: It is a concept in physical partition, where one topic can contain one or more partitions. CKafka uses partition as an allocation unit.
   - Replica Count: The number of partition replicas is used to ensure the high availability of the partition. To ensure data reliability, creating a single-replica topic is not supported. Two replicas are enabled by default.
     Replicas are also counted into the number of partitions. For example, if you create 1 topic with 6 partitions and 2 replicas for each partition, then you have a total of 12 partitions (1 x 6 x 2).
   - **Tag**: Set a resource tag. For more information, see [Tag Overview](https://intl.cloud.tencent.com/document/product/597/41600).
   - Preset ACL Policy: Select the preset ACL policy. For more information on ACL policy, see [Configuring ACL Policy](https://intl.cloud.tencent.com/document/product/597/39084).

5. Click **Submit**.

