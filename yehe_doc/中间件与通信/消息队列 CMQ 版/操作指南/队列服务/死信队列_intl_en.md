This document describes the basic concept, use cases, and usage of TDMQ for CMQ dead letter queue.

## Feature Overview

A dead letter queue (DLQ) is used to process messages that cannot be consumed normally. If consumption still fails after the maximum number of retries, it indicates that the consumer cannot consume a message under normal circumstances. At this point, TDMQ for CMQ will not immediately discard the message; instead, it will send the message to a special queue of the consumer, i.e., DLQ. You can enable DLQ for both new and existing queues.

## Use Cases

- **Issue location**: for example, if a message is not deleted after being consumed multiple times, this is generally because the message is not consumed properly, and there may be an issue which you should identify. You can set the maximum number of receipts after which the message will be placed in the specified DLQ for subsequent troubleshooting.

- **Priority queue**: for example, O2O customers such as bike sharing operators have high requirements for access latency and real-timeness. In the bike unlocking logic, after TDMQ for CMQ retains 100 million messages, it will process the latest messages first and place old ones in the DLQ for consumption when the consumer is capable of consuming them.
As users may have been lost while old messages are waiting (such as bike unlocking through QR code scan), the value of old messages is low; therefore, we recommend processing the latest messages first.

## Directions

When creating a queue in the [TDMQ for CMQ console](https://console.cloud.tencent.com/tdmq/cmq-queue), you can enable the DLQ feature.

<img src="https://qcloudimg.tencent-cloud.cn/raw/50d82689a33899d3a5d7a2b7ca782956.png" width="500px">

- DLQ Queue Name: specify a queue as the DLQ of the queue.

- Dead Letter Policy: select the method of triggering dead letter messages.
  - Maximum Number of Receipts: maximum number of times a message is allowed to be received before it is sent to the DLQ. The value range is 1–1000 times.
  - Maximum Unconsumed Time: maximum time a message remains unconsumed before it is sent to the DLQ. The value range is 5 minutes–12 hours.

## Use Limits

- A queue can be bound to only one DLQ.
- The bound DLQ must be in the same region and under the same account as the queue. 
- If a DLQ has been bound to a queue, it cannot be deleted directly.
- A queue with transaction message enabled cannot act as a DLQ.
- A queue can be specified as the DLQ of up to 6 queues, but other queues cannot be specified as its DLQ (this helps avoid nesting).
- A source queue (data queue produced to or consumed from by the client) can be unbound from the DLQ. The DLQ can then be deleted if it has no other queues bound to it.
- If an existing regular queue is specified as a DLQ at time point T, and it contains unconsumed messages before time point T, all such messages need to be consumed before the dead letter policy can be triggered.

