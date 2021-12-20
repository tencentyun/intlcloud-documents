For duplicate messages, the best solution is to make them reentrant (repeated message consumption has no impact on the business). If this is not possible, deduplication needs to be performed on the consumer side.

## Causes of Message Duplication

![](https://main.qcloudimg.com/raw/a705e5969a503b19fce600ae4b2927be.png)
Messages may be lost due to network exceptions, server failures, or other issues. To prevent message loss and ensure reliable delivery, TDMQ for CMQ adopts a mechanism of dual acknowledgment mechanism for message production and consumption.

**Message production acknowledgment**: normally, the producer sends a message to TDMQ for CMQ and waits for acknowledgment from it, and it stores the message in the disk and returns a success to the producer. However, if the producer request times out or TDMQ for CMQ returns an error, the producer needs to send the message to it again.

**Consumer acknowledgment**: TDMQ for CMQ delivers the message to the consumer and sets it to invisible, and the consumer uses a handle to delete the message during the invisibility period. If the message is not deleted and the invisibility period elapses, it will become visible again.

As the message acknowledgment mechanism of TDMQ for CMQ guarantees at-least-once delivery of every message, repeated production/consumption may occur due to network jitters or producer/consumer exceptions.


## Deduplication Scheme
The first step of deduplication is to identify duplicate messages. A common approach is to insert a deduplication key in the message body when producing a message, which is used to identify duplicate messages at the time of consumption. The deduplication key can be a unique value composed of <producer IP + thread ID + timestamp + incremental value within a time period>.

If there is only one consumer, you can cache the consumed deduplication keys (e.g., KV) and check whether they have already been consumed during each consumption. The key cache can be set to expire based on the maximum validity period of messages. TDMQ for CMQ provides a parameter for the current minimum unconsumed message time (min_msg_time) in the queue. You can use this parameter and the maximum retry period for message production to determine the cache expiration time.
If there are multiple consumers, distributed caching of deduplication keys should be used.

-	Calculate key expiration time based on the maximum message validity period:
current_time + max_retention_time + max_retry_time + max_network_time
(Current time) + (maximum validity period) + (maximum retry period) + (maximum network time)

-	Calculate key expiration time based on the minimum unconsumed time provided by TDMQ for CMQ:
min_msg_time + max_retry_time + max_network_time
(Minimum unconsumed time) + (maximum retry period) + (maximum network time)

 TDMQ for CMQ supports a maximum message validity period of 15 days. You can adjust the validity period within the value range as needed.
 The earliest time of a consumed and acknowledged message in the current TDMQ for CMQ queue, which is the earliest time point as shown in the figure below. All the messages before this time point have already been deleted, while those after it may have not.
![](https://mc.qcloudimg.com/static/img/dbff4055c9fa8a10160ff59a830c016c/image.jpg)



## Examples
**How to avoid duplicate commits:**

- Scenario: A is a producer, B is a consumer, and TDMQ for CMQ is between them. A transferred 10 USD to B and sent a message to TDMQ for CMQ. TDMQ for CMQ successfully received the message but failed to respond to A due to network jitters or A's server failures. A assumed that the sending failed and therefore produced a new message, resulting in duplicate commits.

- Solution: when producing the message, A can add information such as timestamp to generate a unique deduplication key. If A assumes that the delivery failed due to network exceptions and retries, the same deduplication key will be used. At this point, consumer B can deduplicate the message based on the deduplication key.
As implied in this example, message ID in TDMQ for CMQ cannot be used for deduplication, because the two messages have different IDs but the same body.

- Note: before sending a message, producer A should make the deduplication key persistent (such as writing it to the disk to avoid loss due to power failure).

**How to prevent multiple messages with the same body from being filtered out:**

- Scenario: A transferred 10 USD to B with five requests containing the same body committed. If B arbitrarily uses the message body as the decisive criterion for deduplication, those five requests will be mistaken for one.

- Solution: A can add information such as timestamp when producing the messages. In this way, even if the messages have the same body, the generated deduplication keys will be different, which makes it possible to send multiple messages with the same body.
