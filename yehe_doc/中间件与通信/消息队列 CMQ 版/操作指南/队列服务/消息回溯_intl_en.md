 TDMQ for CMQ provides a message rewind feature similar to that in Kafka. After your business successfully consumes and deletes a message, you can use this feature to consume the message again.

This document describes the concepts, use cases, and use methods of message rewind in TDMQ for CMQ.

## Feature

![](https://qcloudimg.tencent-cloud.cn/raw/683c8ba135048e68c88d93eb3a2ebb0f.png)
As shown above, the message lifecycle is circled in the blue box. After message rewind is enabled, messages consumed and deleted by consumers will be moved to the **rewindable message** section and retained on the TDMQ for CMQ backend. However, if the message existence exceeds the message lifecycle of the queue (assumed as 1 day), the message will be automatically deleted and cannot be rewound.

### Product logic

- **Enable:** if message rewind is not enabled, after a message is consumed by a consumer and its deletion is confirmed, it will be deleted immediately. When enabling this feature, you need to specify the rewind time range, which must be equal to or shorter than the message lifecycle.

- **Milestone:** according to the policy above, after message rewind is enabled, the number of rewindable messages will keep increasing as consumers continuously consume and delete messages.

- **Disable:** after message rewind is disabled, messages in the rewindable message section will be deleted immediately and cannot be rewound.

- **Queue attribute:** message rewind is an attribute of a queue and can be set when you create the queue or modify its configuration. After specifying a rewind time point, all consumers will consume messages produced after this time point.

- **Billing:** after message rewind is enabled, rewindable messages will incur certain retention fees. The unit price is calculated as part of message retention fees.

- **Specify rewind time point**: when a consumer initiates rewind consumption, the queue name and specific rewind time need to be specified, and messages will be rewound from the maximum time point. The time is a `key`, and reverse consumption is not supported. You can consume from timeA to timeB/timeC but not vice versa as shown below.

- **Specify rewind time range:** it ranges from 0 to 15 days. Only after message rewind is enabled in the console can deleted messages be rewound. You are recommended to always enable this feature for key applications and set the message rewind time range to the same as the message lifecycle.

- **Unable to specify message rewind for retained messages:** if a message is retained and not consumed, you cannot specify a specific position for its consumption.

### Rewindable range

The message rewindable range is sorted by message production time and is irrelevant to the order of deletion.

1. The maximum rewindable time point = current_time - rewind_seconds (retention period of rewindable message)
2. The minimum rewindable time point = min_msg_time (the minimum unconsumed message time of the queue)
3. Maximum rewindable time point ≤ start_consume_time ≤ minimum rewindable time point

## Use Cases

This feature facilitates operations such as reconciliation and business system retry for core finance businesses.

## Use Case

The following is a typical use case of message rewind:

There are two businesses (A and B) in a normal production/consumption scenario. A produces messages and delivers them to a queue, and B consumes messages from the queue. At this point, A and B are decoupled from each other and don't care about each other. A only needs to produce and deliver messages, while B gets messages from the queue, deletes them from the queue, and then consumes them locally.

An exception occurs; for example, although business B tries to consume messages, consumption has been exceptional for a period of time. In this case, the messages have been deleted and cannot be consumed again, which will affect the business; moreover, it is necessary to suspend business B and wait for the development and OPS personnel to fix the exception before making business B online again. In addition, the personnel cannot monitor the status of business B in real time, so the exception may have already lasted some time before it is discovered.

To prevent this, business A should be concerned about the processing of business B, back up the produced messages, and make sure that business B can consume the message normally in the production environment before deleting the backup.

In this case, you can use the **message rewind** feature. After business B is restored, messages can be rewound to the last time point when business B's consumption was normal. Then, the messages obtained by business B will start at the specified time point, so business A doesn't need to care about any exceptions of business B at all. Business B should ensure the consumption idempotency.

### Enabling message rewind

You can directly enable the message rewind feature when creating a queue in the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue).

![](https://qcloudimg.tencent-cloud.cn/raw/69ecb7ca62406731c997e8da0b99d5e3.png)



You can also enable message rewind on the queue details page.

![](https://qcloudimg.tencent-cloud.cn/raw/b080265f5e8da66d67f0dc18e9d511e2.png)

Set the message rewind parameters on the client.

```java
endpoint='' // TDMQ for CMQ domain name
secretId ='' // User ID and key
secretKey = ''
account = Account(endpoint,secretId,secretKey)
queueName = 'QueueTest'
my_queue = account.get_queue(queueName)
queue_meta = QueueMeta()
queue_meta.rewindSeconds = 43200 // Message rewindable time in seconds
my_queue.create(queue_meta)
```

### Using message rewind

```java
my_queue.rewindQueue(1488718862) // Specify the time point for message rewind, which is a Unix timestamp
```

