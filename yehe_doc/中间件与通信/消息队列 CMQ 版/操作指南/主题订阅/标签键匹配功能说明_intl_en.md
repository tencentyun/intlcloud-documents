The topic mode of TDMQ for CMQ supports subscription filtering by tag, which is similar to the "direct_routing" mode of RabbitMQ. The "topic_pattern" mode will be provided in the next iteration. As the usage policies of filter tags are complex, this document uses different scenarios as examples to describe them.

## Scenario Description

### Scenario 1

There are four subscribers A, B, C, and D and the message tags are as follows: `apple` for A, `xiaomi` for B, `imac+xiaomi` for C, and none for D.
A producer publishes 100 messages to the topic with message filter tags `apple`, `imac`, `iphone`, and `macbook`, and the topic is delivered to A, B, C, and D immediately.

**Scenario analysis:**

| Subscriber | Message Tag | Message Receipt Description |
| :----- | :---------- | :----------------------------------------------------------- |
| A | apple | As `apple` can match the `apple` message filter tag, the 100 messages can be received properly. |
| B | xiaomi | No messages can be received. |
| C | imac+xiaomi | As `imac` can match the `imac` message filter tag, the 100 messages can be received properly. |
| D | - | All messages can be received. |

### Scenario 2

A topic has only four subscribers A, B, C, and D, none of which set any message tags.
A producer publishes 100 messages to the topic with message filter tags `apple`, `imac`, `iphone`, and `macbook`, and the topic is delivered to A, B, C, and D immediately.

**Scenario analysis:**
As none of subscribers A, B, C, and D have tags, messages do not need to be matched during delivery, and all of them can receive the 100 messages.

### Scenario 3

A topic has only one subscriber A whose subscription tag is set to `xiaomi`.
A producer publishes 100 messages to the topic with message filter tags `apple`, `imac`, `iphone`, and `macbook`, and the topic is delivered to A immediately.

**Scenario analysis:**

- As the subscription tag of subscriber A does not match, A cannot receive the 100 messages. In this case, the 100 messages will be discarded immediately and will not be retained in TDMQ for CMQ.
- When the producer publishes to the topic, message filter tags can be set once only before publishing. They will be bound to message IDs and cannot be modified.

### Scenario 4

A topic is named `test1`, and the subscription publishing API is called at 12:01 (this operation is named "publishing test1"). After the publishing, the topic is delivered to subscribers A, B, and C so as to deliver 200 messages to them.
Suppose the result is as follows: A fails to receive 100 messages, B fails to receive 30 messages, and C successfully receives all the 200 messages.

**Scenario analysis:**

- **Message retention:** among subscribers A, B, and C, suppose the total number of messages failed to be delivered is 110 (100 ones fail to be delivered to A, 30 to B, and none to C, and the failed ones may be repeated). As long as any subscriber is associated with a message, the message will not be unsubscribed from immediately.

- **Blocking policy:** taking A as an example, the topic delivers 200 messages to A, and if the 101st message fails to be delivered, the delivery of subsequent 99 messages will be blocked. In this case, 100 messages will fail to be delivered.

- **Retry policy (backoff retry):** the `test1` topic will deliver the messages again to A once every N seconds. Specifically, the failed 100 messages will be delivered to A again starting from the first one in sequence. If a message fails to be delivered for three consecutive times, it will be directly discarded, and the next message will be delivered, which may also be discarded after three failures, and so on.

- **Retry policy (decay exponential retry):** taking A as an example, the topic delivers 100 messages concurrently to A (the sequence cannot be guaranteed). When a message fails to be delivered to A, the very message will be retried. If it fails again, subsequent messages will be blocked.

- **Inextensible message lifecycle:** suppose the 110 messages are retained in the `test1` topic. No matter how many times they are retried for delivery, their lifecycle still remains 1 day. The time point when a message is pushed by the producer to the topic will be the lifecycle start time point, and the message will be deleted once the lifecycle expires.

- **Repush**: the producer continuously produces new messages to the topic, and the subscription publishing API is called again at 12:02. Suppose the topic now has 210 messages (110 retained messages that fail to be delivered plus 100 messages that are produced in one minute) and delivers them again. In this case, as the retry policy for A and B is exponential decay retry, A and B cannot "respond", and the 210 messages will continue to be retained. C will receive only the 100 new messages.

  
>?Each message ID is used as the key, and the value is the associated subscribers, indicating whether consumption of each subscriber is successful.

### Scenario 5

A topic named `test2` calls the subscription publishing API at 12:01, and this operation is named "publishing test2", which delivers 200 messages to subscribers A, B, and C.
Assume that A, B, and C successfully receive all the 200 messages.

**Scenario analysis:**
If the topic `test2` has only three subscribers A, B, and C, and the 200 messages are successfully consumed, it will immediately delete all these messages.

## Rule Summary

You can summarize the following tag match rules from the aforementioned scenarios:

| Subscriber | Whether Subscriber Has Tag | Whether Message Tag Exists | Message Receipt Description |
| :----- | :------------- | :----------- | :----------------------------------------------------------- |
| A | Yes | No | The subscriber does not match and cannot receive messages. |
| B | No | Yes | The delivered messages do not need to be matched and all subscribers can receive messages. |
| C | Yes | Yes | Messages can be received only when the tags match. N:M match is supported; for example, if a message has 10 tags, and a subscriber has 4 tags, the subscriber can receive the message as long as there is one matching tag. |
| D | No | No | After a message is delivered, all subscribers can receive it. |
