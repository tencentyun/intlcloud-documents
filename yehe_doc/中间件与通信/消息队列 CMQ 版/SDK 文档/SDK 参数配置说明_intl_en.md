TDMQ for CMQ is a distributed message queue service that provides a reliable message-based async communication mechanism. It enables message sending/receiving among different applications deployed in a distributed manner (or different components of the same application) and stores the delivered messages in reliable and valid TDMQ for CMQ queues to prevent message loss. It supports multi-process simultaneous read/write, so that message sending and receiving do not interfere with each other, eliminating the need for the applications or components to keep running.

TDMQ for CMQ provides four SDKs. This document uses the SDK for Python as an example.

## SDK for Python Overview

To facilitate your use, TDMQ for CMQ operations for objects such as users, queues, and topics are divided into the following classes:
- Account: encapsulates account `SecretId` and `SecretKey` so that you can create, delete, and view queues, topics, and subscriptions.
- queue: receives/sends messages and views/sets queue attributes.
- topic: publishes messages, views/sets topic attributes, and views subscribers.
- cmq_client: sets the attributes of the connection between client and server, such as setting whether log write is enabled, connection timeout period, and whether persistent connection is enabled

>!All classes are not thread-safe. If you need to use them in multiple threads, it is recommended that each thread instantiate its own objects.

[SDK download >>](https://intl.cloud.tencent.com/document/product/1111/43020)


## Queue Model

A queue in TDMQ for CMQ is different from that defined in a data structure. Queues in data structures are manipulated in strict compliance with the First In, First Out (FIFO) rule, while TDMQ for CMQ distributed queues do not strictly follow FIFO (a dedicated FIFO product will be released in the future). A TDMQ for CMQ queue is considered as a container featuring high performance, capacity, and reliability, to which produced messages can be delivered, and from which messages can be fetched out for consumption. It has its own attribute settings during initialization as detailed below:

| Attribute | Description |
|---------|---------|
| maxMsgHeapNum | Maximum number of retained messages, i.e., number of messages that can be stored in a queue. It represents the queue storage and retention capacity. |
| pollingWaitSeconds | Long-Polling waiting time for message receipt, which ranges from 0 to 30 seconds. It indicates the default time it takes to receive a message during message consumption.<br>For example, when this attribute is set to 10, if there are no messages during message consumption, the result will be returned after 10 seconds of waiting by default; otherwise, the result will be immediately returned.<br>You can customize the waiting time when receiving messages, which will take precedence over this attribute. | 
| visibilityTimeout | Message visibility timeout period.<br>After a message is obtained by a consumer, there will be an invisibility period, during which other consumers cannot get this message. This value ranges from 1 to 43,200 seconds (12 hours), and the default value is 30. | 
| maxMsgSize | Maximum message size, which ranges from 1,024 to 1,048,576 bytes (i.e., 1–1,024 KB). The default value is 65,536. | 
| msgRetentionSeconds | Message lifecycle, i.e., message retention time period in queue, which ranges from 60 to 1,296,000 seconds (1 minute to 15 days). The default value is 345,600 (4 days). | 
| createTime | Queue creation time. A Unix timestamp accurate down to the second will be returned. | 
| lastModifyTime | Time when the queue attribute is last modified. A Unix timestamp accurate down to the second will be returned. | 
| activeMsgNum | Total number of messages in `Active` state (not being consumed) in queue, which is an approximate value. |  
| inactiveMsgNum | Total number of messages in `Inactive` state (being consumed) in queue, which is an approximate value. | 
| rewindSeconds | Maximum time range during which a message can be rewound in the queue, which ranges from 0 to 43,200 seconds. 0 indicates that message rewind is disabled. | 
| rewindmsgNum | Number of retained messages which have been deleted by the `DelMsg` API but are still within their rewind time range. | 
| minMsgTime | Minimum unconsumed time of message in seconds. | 
| delayMsgNum | Number of delayed messages. | 

[Getting started with the queue model >>](https://intl.cloud.tencent.com/document/product/1111/42991)

## Topic Model

The topic model is similar to the publish/subscribe design pattern. A topic is the unit for sending messages, and subscribers under a topic are equivalent to observers. A topic will actively push published messages to subscribers.   

| Attribute | Description |
|---------|---------|
| msgCount | Number of messages currently retained in topic (number of retained messages) |
| maxMsgSize | Maximum message size, which ranges from 1,024 to 1,048,576 bytes (i.e., 1–1,024 KB). The default value is 65,536. |
| msgRetentionSeconds | Maximum lifecycle of message in topic. After the period specified by this parameter has elapsed since a message is sent to the topic, the message will be deleted no matter whether it has been successfully pushed to the user. This parameter is measured in seconds and defaulted to one day (86,400 seconds), which cannot be modified. |
| createTime | Topic creation time. A Unix timestamp accurate down to the second will be returned. |
| lastModifyTime | Time when the topic attribute is last modified. A Unix timestamp accurate down to the second will be returned. |
| filterType | Filtering policy selected when a subscription is created:<br> If `filterType` is 1, `filterTag` will be used for filtering.<br>If `filterType` is 2, `bindingKey` will be used for filtering. |

