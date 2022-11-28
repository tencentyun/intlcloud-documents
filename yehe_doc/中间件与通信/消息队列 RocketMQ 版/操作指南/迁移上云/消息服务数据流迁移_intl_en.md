## Overview

In a [metadata migration task](https://www.tencentcloud.com/document/product/1113/51219), you can sync the metadata of a self-built RocketMQ cluster to TDMQ for RocketMQ. After the sync, you need to modify the access information of the producer and consumer clusters in order to migrate them from the self-built cluster to TDMQ for RocketMQ for message sending and receiving.

>?Currently, the message migration service migrates only message production and consumption linkages but not message data in the old RocketMQ cluster. It applies only to exclusive clusters as the destination and will be supported for virtual clusters after the beta test ends.



## Migration Directions

This document describes the **double-read double-write** and **batch release** schemes of the message migration service. During migration, the producer and consumer clusters can produce or consume messages in the old RocketMQ and new TDMQ for RocketMQ clusters in parallel. Data will not be heaped because of the migration, so the business can transition smoothly.

![](https://qcloudimg.tencent-cloud.cn/raw/d4d922b8a9f62dd6612443e0aac063c6.png)        

The detailed directions are as follows:

1. Create a TDMQ for RocketMQ cluster, migrate the metadata, and get the required client information in the console, such as the access point of the new cluster, `AccessKey`, and `SecretKey`.
2. Modify the access information of certain nodes in the consumer cluster to connect corresponding consumers to the new TDMQ for RocketMQ cluster. They will consume messages in the new cluster, while the rest will continue to consume messages in the old cluster.
3. Modify the access information of certain nodes in the producer cluster to connect corresponding producers to the new TDMQ for RocketMQ cluster. They will send messages to the new cluster, while the rest will continue to send messages to the old cluster. To avoid message repetition or loss, implement the idempotency logic for message consumption in advance.
4. Connect the remaining producers to the new TDMQ for RocketMQ cluster. Then, all messages will be sent to the new cluster.
5. Check whether there are heaped messages that are not consumed in the old RocketMQ cluster, and if not, connect the remaining consumers to the new TDMQ for RocketMQ cluster. At this point, the migration is completed.



> !
>
> - If you don't follow the above steps strictly, for example, if you switch producers first and then consumers, message loss may occur.
> - Before switching the remaining consumers, make sure that all messages in the old RocketMQ cluster have been consumed; otherwise, some messages may not be consumed. You can view the number of heaped messages in the old cluster to check whether consumption has completed.



### Migration process diagram

![](https://qcloudimg.tencent-cloud.cn/raw/077675eecb90f3f379833441f7967401.png)        


## Possible Issues

### Sequence

Message sequence cannot be guaranteed due to cluster switch.

### Message repetition

Message repetition occurs only in extreme cases. For example, if a consumer consumes a message but doesn't send an acknowledgment to the server (the old RocketMQ cluster), the message will be put into the retry queue, causing repeated consumption. Implementing the idempotency logic can avoid this issue.

### Consumption delay

During the read switch, partitions are reallocated with rebalancing between the queue and consumer client. This may cause a short consumption delay, but you don't need to handle it because it won’t persist after the switch.
