## Overview

To enable public network access, you need to configure an ACL policy for a topic. This document describes how to create a topic and configure an ACL policy for a created instance in the CKafka console.

## Directions

### Step 1. Create a topic

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the **Instance List** page, click the ID of the instance created in [step 1](https://intl.cloud.tencent.com/document/product/597/40044) to go to the instance details page.
3. On the instance details page, click the **Topic Management** tab and click **Create**.
4. In the **Create Topic** dialog box, set parameters as needed.
   ![](https://main.qcloudimg.com/raw/a93a5c2ce385779e632965a4411903da.png)
  - Name: topic name, which cannot be changed once entered and can contain only letters, digits, underscores (_), hyphens (-), and dots (.).
  - Partition Count: number of partitions (physical). A topic can contain one or multiple partitions. CKafka allocates resources by partition.
  - Replica Count: number of partition replicas, which ensure the availability of partitions. For data reliability concerns, CKafka does not support single-replica topics currently. Two replicas are created for each partition by default.
    Replicas are also counted into the number of partitions. For example, if you create 1 topic with 6 partitions, and 2 replicas for each partition, then you have a total of 12 partitions (1 x 6 x 2).
  - Allowlist: if the allowlist is enabled, the topic can be accessed only from IP addresses in the allowlist, which ensures data security. You can enable allowlist in either the **Create Topic** or **Edit Topic** window.
4. Click **Submit**.

### Step 2. Configure an ACL policy

1. On the instance details page, click the **User Management** tab, click **Create**, and set the username and password in the **Add User** dialog box displayed.
   ![img](https://main.qcloudimg.com/raw/5dad7d1f14bebd52b08a366bd356e638.png)
2. On the **ACL Policy Management** tab page, locate the topic created and click **Edit ACL Policy** in the *Operation* column to add read/write permission for the user.
    ![img](https://main.qcloudimg.com/raw/5aae813035f9981c7fa975dea6a4b812.png)
