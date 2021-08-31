This document describes the factors that affect the reliability of CKafka from the perspectives of the producer, the service (CKafka), and the consumer, respectively, and provides corresponding solutions.

### What should I do if data is lost on the producer?
#### Causes of data loss
When the producer sends data to CKafka, the data may be lost due to network jitters, and CKafka will not receive the data. This may be caused by following reasons:
- The network load is high or the disk is busy, and the producer does not have a retry mechanism.
- The purchased disk capacity is exceeded. For example, if the disk capacity of an instance is 9,000 GB, and it is not expanded promptly after being used up, data cannot be written to CKafka.
- Sudden or continuously increased peak traffic exceeds the purchased peak throughput. For example, if the peak throughput of the instance is 100 MB/s, but it is not scaled up promptly after the peak throughput is exceeded for a long period of time, data writes to CKafka will become slower. In this case, if the producer has a queuing timeout mechanism in place, data cannot be written to CKafka.

#### Solution
- Enable the retry mechanism on the producer for important data.
- For disk usage, set up monitors and [alarm policies](https://console.cloud.tencent.com/monitor/policylist/create) as preventive measures when configuring the instance.
When the disk capacity is used up, upgrade the instance timely in the console. Upgrading non-exclusive CKafka instances will not interrupt the service, which also supports expanding the disk capacity alone. You can also shorten the message retention period to reduce disk usage.
- In order to minimize the loss of messages at the producer side, you can fine-tune the size of the buffer using `buffer.memory` and `batch.size` (in bytes). For the buffer, bigger is not always better. If the producer is down for some reason, the more data in the buffer, the more garbage to be recycled, and the slower the recovery. **Pay close attention to the number of messages produced by the producer and average message size** (through the rich set of monitoring metrics available in CKafka).
- Configure ACK for the producer.
When the producer sends data to the leader, the data reliability level can be set using the `request.required.acks` and `min.insync.replicas` parameters.
 - When acks = 1 (default value), the producer's leader in ISR has successfully received a data entry, and the next data entry can be sent. If the leader is down, as the data may have not been synced to its followers, the data will be lost.
 - When acks = 0, the producer sends the next message without waiting for acknowledgment from the broker. In this case, data transfer efficiency is the highest, but data reliability is the lowest.
 - When acks = -1 or all, the producer needs to wait for acknowledgment of message receipt from all the followers in ISR before sending the next message, which leads to highest reliability.
Even if ACK is configured as above, there is no guarantee that data will never be lost. For example, when there is only one leader in ISR (the number of members in ISR may increase or decrease in certain circumstances, and in some cases, only one leader is left), `acks` will be 1. Therefore, you also need to use the `min.insync.replicas` parameter (which can be configured in CKafka Console > Topic Management > Advanced Configuration). It represents the minimum number of replicas in ISR, which is 1 by default and takes effect when and only when acks = -1 or all.

#### Recommended parameter values
These parameter values are for reference only, and actual values depend on the actual conditions of your business.
 - Retry mechanism: `message.send.max.retries=3;retry.backoff.ms=10000;`
 - Guarantee for high reliability: `request.required.acks=-1;min.insync.replicas=2;`
 - Guarantee for high performance: `request.required.acks=0;`
 - Reliability + performance: `request.required.acks=1;`

### What should I do if data is lost on the server (CKafka)?
#### Causes of data loss
- The partition's leader is down before the backup of followers is completed. Even if a new leader is elected, data will be lost because it has not been backed up yet.
- Open-Source Kafka features async storage to disk, that is, data is first stored in PageCache. If the broker breaks, restarts, or fails, the data stored in PageCache will be lost because it has not been stored to the disk yet.
- Stored data may be lost due to disk failure.

#### Solution
- Open-Source Kafka has a multi-replica feature. You are recommended to use replicas to ensure data integrity. Data will be lost only if multiple replicas and multiple brokers fail at the same time, so data reliability is higher than that in the single-replica case. Therefore, CKafka requires at least 2 replicas for a topic and supports configuring 3 replicas.
- More reasonable values are configured for the `log.flush.interval.messages` and `log.flush.interval.ms` parameters in CKafka for data flushing.
- In CKafka, the disk is specially designed to ensure that data reliability will not be compromised even if the disk is partially damaged.

#### Recommended parameter values
A replica which is not in syncing status can be elected as a leader: `unclean.leader.election.enable=false // Disabled`

### What should I do if data is lost on the consumer?
#### Causes of data loss
- The offset is committed before data is consumed. If the consumer is down in the process but the offset has been updated, the consumer will miss a data entry, and the consumer group will have to reset the offset in order to retrieve it.
- The consumption speed differs significantly from the production speed, but the message retention period is too short; therefore, the message will be deleted upon expiration before it is consumed.

#### Solution
- Configure the `auto.commit.enable` parameter appropriately. When it is `true`, commit is performed automatically. You are recommended to use scheduled commit so as to avoid frequent commit offset.
- Monitor the consumer and correctly adjust the data retention period. Monitor the consumption offset and the number of messages that are not consumed, and configure an alarm to prevent messages from being deleted upon expiration due to slow consumption.


