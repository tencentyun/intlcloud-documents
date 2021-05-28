### What should I do if a lot of messages heap up?
#### Error description
A warning is displayed for message heap.

#### Possible causes
If the instance is configured with an alarming rule in Cloud Monitor, when too many unconsumed messages heap up, an alarm will be generated for the "number of retained messages".

#### Solution
You can log in to the [CKafka console](https://console.cloud.tencent.com/ckafka), find the consumer group where messages heap up, and observe whether there are active consumers in the consumer group:
- If yes, ask the consumers to speed up consumption.
- If not, delete the unused consumer group as appropriate.

#### Recommended settings
Open-Source Kafka supports setting a timestamp field and type in a message. Currently, two timestamp types are supported: `CreateTime` and `LogAppendTime`.

- `CreateTime` indicates the local time on the client. As client time may vary from server time, please check whether the entered time is correct. If it differs too much from the current Beijing time, the CKafka service will not be able to expire and delete data promptly based on the normal message retention period, which may cause exceptional message heap.
- `LogAppendTime` indicates the time when a message is produced to the CKafka service, which is the CKafka server time and thus recommended.
