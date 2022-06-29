## Parameter Differences Between TDMQ for CMQ and CMQ

The usage and syntax of the data flow (messaging) SDK of TDMQ for CMQ remain unchanged, but some parameters and features are different from those of CMQ.  Given these differences, TDMQ for CMQ has pertinent parameters configured specially to ensure that the original production and consumption logic will stay the same after migration. However, we recommend you configure new queues and topics based on the logic of TDMQ for CMQ.

### Message lifecycle
TDMQ for CMQ adopts the message lifecycle model commonly used in the industry, where time to live (TTL) and retention are used together to avoid high message queue load caused by excessive heap of messages. When the utilization of the capacity for heaped messages reaches 100%, writes will be impossible.

Compared with CMQ, TDMQ for CMQ has a new configuration item of maximum message unacknowledged time ranging from 30 seconds to 12 hours. If the consumer client fails to acknowledge a received message within this time period, the server will automatically acknowledge the message.

Unacknowledged messages will be stored in the message queue and will not be deleted. Acknowledged messages are subject to the message rewindable time and rewindable disk space. If message rewind is not enabled, messages will be deleted directly once acknowledged.

TDMQ for CMQ removes the limit on message lifecycle. By default, messages can no longer be heaped in the queue for a long time. If there are special needs, you can enable message rewind and set the rewindable time range. Only messages with message rewind enabled can be stored in the message queue for more than 12 hours. Once enabled, this feature incurs storage fees as detailed in TDMQ for CMQ's billing overview.

>? Queues migrated from CMQ to TDMQ for CMQ will inherit the message lifecycle within the maximum message unacknowledged time to ensure that existing businesses run properly. The period can range from 30 seconds to 12 hours when you adjust it later. Pay attention to the client processing logic when adjusting it.

### Message heap limit

TDMQ for CMQ removes the limit on the number of heaped messages. In theory, an unlimited number of messages can be heaped as long as the storage capacity is sufficient. However, from the perspective of hardware, we allocate a maximum capacity for heaped message of 10 GB to each queue. You can configure CM alarms based on this value.

![](https://qcloudimg.tencent-cloud.cn/raw/3ca2d9c0dc1030373d365e7df9003514.png)

Generally, about 10 million messages with an average size of 1 KB each can be heaped. If you expect that the heap may exceed the upper limit after migration, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=947&source=14&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CMQ&step=1) for assistance.

### Message size
TDMQ for CMQ no longer supports setting the maximum message size. In order not to affect the business migration from CMQ, the original maximum message size of 1,024 KB is set for all new queues.

>? You cannot set the message size for queues migrated from CMQ. If you need to add a limit, create new queues in TDMQ for CMQ.


### Long polling wait time for message receipt

The meaning of this parameter remains the same, but its effect is different in TDMQ for CMQ, where we recommend you keep it below 3s.

In TDMQ for CMQ, if the long polling wait time for message receipt is too long, as the underlying layer needs to ensure the semantics of "consumption at least once", the repetition rate of message delivery may increase significantly, causing a severe impact on some downstream services without message deduplication implemented. Therefore, if you want to reduce the probability of message duplication, set this parameter as small as possible (3 seconds is recommended, as basically no repeated delivery will occur under this value).

### Capacity for unacknowledged messages
TDMQ for CMQ has a limit on the capacity for unacknowledged messages, ensuring that the memory usage of the message queue server is controlled for guaranteed stability. If the client fails to acknowledge messages in a timely manner, an excessive number of invisible messages are generated. This metric has a monitoring chart. If it surges, check whether the consumer's acknowledgment and deletion logic works properly. If the capacity is insufficient under the surge, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=947&source=14&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CMQ&step=1) for assistance.

