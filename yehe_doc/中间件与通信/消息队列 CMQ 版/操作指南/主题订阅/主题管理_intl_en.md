## Overview

The topic model is similar to the publish/subscribe design pattern. A topic is the unit for sending messages, and subscribers under a topic are equivalent to observers. A topic will actively push published messages to subscribers.

This document describes how to create or delete a topic in TDMQ for CMQ.

## Directions

### Creating topic

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Topic Subscription** on the left sidebar, select the region, click **Create**, and enter the information as prompted.
![](https://qcloudimg.tencent-cloud.cn/raw/cbe59deb464e839551fe01cad174d18b.png)


   | Attribute | Description |
   |---------|---------|
   | Topic Name | <li>Enter the topic name, which cannot be modified once the topic is created. </li><li>The name can contain up to 64 letters, digits, hyphens, and underscores and is case-sensitive. To avoid confusion, topics with the same name in the same letter case as an existing topic cannot be created.</li> |
   | <nobr>Message Retention</nobr> | It is enabled by default. Messages that are produced by a producer but have not triggered push to subscribers or failed to be received by subscribers will be retained in the topic temporarily. </li><li>In the topic list, you can view the approximate total number of currently retained messages. </li>|
  
	
### Deleting topic

In the **[topic](https://console.cloud.tencent.com/tdmq/cmq-topic)** list, click **Delete** in the **Operation** column of the target topic to delete it. Messages cannot be pushed once the topic is deleted.
