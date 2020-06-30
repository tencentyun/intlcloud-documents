CMQ supports topic subscription with filtering by tags, which is similar to the "direct_routing" mode of RabbitMQ. The "topic_pattern" mode will be provided in the next iteration. Filtering by tags is a complex process. In this document, we will take different use cases to explain this concept.
![](https://main.qcloudimg.com/raw/171e6538aafb695b153a68ff682fd38f.png)
## Scenario Description
### Scenario 1
There are four subscribers A, B, C, and D. Their message tags are as follows: `apple` for A, `xiaomi` for B, `imac+xiaomi` for C, and none for D.
A producer publishes 100 messages to the topic with tag filters `apple`, `imac`, `iphone`, and `macbook`. The topic then sends messages to A, B, C, and D immediately.

**Scenario analysis**:

| Subscriber | Message Tag | Message Receipt Description |
|:---------:|:---------:|:---------:|
| A | apple | As `apple` can match the `apple` tag filter, the 100 messages can be received properly. |
| B | xiaomi | No messages can be received. |
| C | imac+xiaomi | As `imac` can match the `imac` tag filter, the 100 messages can be received properly. |
| D | - | All messages can be received. |







### Scenario 2
A topic has only four subscribers A, B, C, and D. None of them have configured any message tags.
A producer publishes 100 messages to the topic with tag filters `apple`, `imac`, `iphone`, and `macbook`. The topic then sends messages to A, B, C, and D immediately.

**Scenario analysis**:
Because none of the subscribers A, B, C, and D have tags, messages do not need to be matched after publishing, and all four subscribers can receive the 100 messages.


### Scenario 3
A topic has only one subscriber A whose subscription tag is `xiaomi`.
A producer publishes 100 messages to the topic with tag filters `apple`, `imac`, `iphone`, and `macbook`. The topic then sends messages to A immediately.

**Scenario analysis**:
- Because the subscription tag of subscriber A does not match, A cannot receive the 100 messages. In this case, the 100 messages will be discarded immediately and will not be retained in CMQ.
- Tag filter can only be configured once before the producer publishes to the topic. It is bound to message IDs and cannot be modified.


### Scenario 4
A topic is named `test1`, and the API for publishing to a subscription is called at 12:01 (this operation is named "publishing test1"). After publishing, the topic sends 200 messages to subscribers A, B, and C.
Suppose the result is as follows: Subscriber A fails to receive 100 messages, B fails to receive 30 messages, and C successfully receives all 200 messages.

**Scenario analysis**:
- **Message retention**: among subscribers A, B, and C, suppose a total of 110 messages fail to be sent (100 messages fail to be sent to A, 30 to B, and none to C. Some messages fail to be sent to multiple subscribers). A message will not be immediately unsubscribed from as long as one subscriber is associated with it.
- **Blocking policy**: the topic sends 200 messages to A. If the 101st message fails to be sent, the next 99 messages will be blocked. In this case, 100 messages fail to be sent.
- **Retry policy (backoff retry)**: the `test1` topic will re-send the failed 100 messages to A sequentially once every N seconds. If a message fails to be sent for three consecutive times, it will be discarded; the next message will be sent, which will be discarded again if three retries fail, and so on.
- **Retry policy (exponential decay retry)**: the topic sends 100 messages concurrently to A (sequence not guaranteed). If a message fails to be sent to A, it will be retried. If it fails again, subsequent messages will be blocked.
- **Message lifecycle cannot be extended**: suppose the 110 messages are retained in `test1` topic. Despite the number of retries, message lifecycles remain as 1 day. The point in time when a message is pushed by the producer to the topic will be the start time, and the message will be deleted once the lifecycle expires.
- **Republish**: the producer continuously publishes new messages to the topic, and the API for publishing to a subscription is called again at 12:02. Suppose the topic then sends 210 messages (110 retained messages that fail to be sent plus 100 new messages published in one minute). In this case, as the retry policy for A and B is exponential decay retry, A and B will not "respond", and 210 messages will be retained. C will only receive the 100 new messages.
>ID of each message is used as the key and the value is the associated subscriber, indicating whether the message consumption is successful.





### Scenario 5
A topic named `test2` calls the API for publishing to a subscription at 12:01, and this operation is named "publishing test2". The topic sends 200 messages to subscribers A, B, and C.
Assume that A, B, and C successfully receive all 200 messages.

**Scenario analysis**:
The topic `test2` has only three subscribers A, B, and C. After the messages are successfully consumed by them, the topic will delete all 200 messages immediately.


## Rule Summary
Based on aforementioned scenarios, tag match rules are as follows:

| Subscriber | Whether Subscriber Has Tag | Whether Message Tag Exists | Message Receipt Description |
|---------|---------|---------|---------|
| A | Yes | No | The subscriber does not match and cannot receive messages. |
| B | No | Yes | The published messages do not need to be matched and all subscribers can receive messages. |
| C | Yes | Yes | Messages can be received only when a pair of tags matches. N:M match is supported. For example, if a message has 10 tags and a subscriber has 4 tags, the subscriber can receive messages as long as one pair of tags matches. |
| D | No | No | After messages are sent, all subscribers can receive them. |


