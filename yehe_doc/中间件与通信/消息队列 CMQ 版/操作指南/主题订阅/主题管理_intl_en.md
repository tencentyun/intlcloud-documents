## Overview

The topic model is similar to the publish/subscribe design pattern. A topic is the unit for sending messages, and subscribers under a topic are equivalent to observers. A topic will actively push published messages to subscribers.

This document describes how to create or delete a topic in TDMQ for CMQ.

## Directions

### Creating topic

1. Log in to the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).
2. Select **Topic Subscription** on the left sidebar, select the region, click **Create**, and enter the information as prompted.
   ![](https://qcloudimg.tencent-cloud.cn/raw/cbe59deb464e839551fe01cad174d18b.png)
   - Topic Name: It can contain up to 64 letters, digits, "-", or "_", and must start with a letter. It cannot be modified once created.
   - Message Heap: Messages will be heaped temporarily if the message push is not triggered or the subscriber fails to receive them.
 - Message Filter Type:
     - Tag: TDMQ for CMQ can match message tags for production and subscription, which can be used for message filtering. For detailed rules, see [Tag Key Matching Feature Description](https://intl.cloud.tencent.com/document/product/1111/43003).
     - Routing Matching: The binding key and routing key are used together and are fully compatible with the topic match mode of RabbitMQ. The routing key carried when a message is sent is added by the client, and the binding key carried when a subscription is created is the binding relationship between the topic and the subscriber. For detailed rules, see [Routing Key Matching Feature Description](https://intl.cloud.tencent.com/document/product/1111/43004).
 - Resource Tag: It is optional and can help you easily categorize and manage TDMQ for CMQ resources in many dimensions. For detailed usage, see [Managing Resource with Tag](https://intl.cloud.tencent.com/document/product/1111/43007).
  
	
### Deleting topic

In the **[topic](https://console.cloud.tencent.com/tdmq/cmq-topic)** list, click **Delete** in the **Operation** column of the target topic to delete it. No messages will be pushed to this topic after it is deleted.
