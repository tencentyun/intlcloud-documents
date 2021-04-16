## Broker Configuration Parameter Description

The following are the configurations of a CKafka Broker for your reference:
```
# Maximum message length in bytes.
message.max.bytes=1000012

# Whether to allow automatic creation of topics. The default value is false. Currently, topics can be created in the console or through the Tencent Cloud API. 
auto.create.topics.enable=false

# Whether to allow topic deletion by calling the API.
delete.topic.enable=true

# The maximum request length allowed for a Broker is 16 MB. 
socket.request.max.bytes=16777216

# Each IP can establish up to 5,000 connections with a Broker.
max.connections.per.ip=5000

# Offset retention period. The default value is 7 days.
offsets.retention.minutes=10080

# Everyone is allowed to access when there is no ACL configuration.
allow.everyone.if.no.acl.found=true

# The log segment size is 1 GB.
log.segment.bytes=1073741824

# The log rolling check interval is 5 minutes. If the retention period is set to less than 5 minutes, it may still take 5 minutes to clear logs.
log.retention.check.interval.ms=300000
```
>?For configurations not listed here, see the [open-source Kafka default configurations](http://kafka.apache.org/0102/documentation.html#brokerconfigs).

## Topic Configuration Parameter Description
#### 1. Number of partitions

From the producer's point of view, writes to different partitions are completely in parallel; from the consumer's point of view, the number of concurrencies depends entirely on the number of partitions (if there are more consumers than partitions, there will definitely be idle consumers). It is important to select an appropriate number of partitions to fully play the performance of the CKafka instance.
The number of partitions should be determined based on the throughput of production and consumption, ideally through the following formula:
>?**Num = max(T/PT, T/CT) = T/min(PT, CT)**

Num represents the number of partitions, T the target throughput, PT the maximum production throughput by the producer to a single partition, and CT the maximum consumption throughput by the consumer from a single partition. The number of partitions is equal to T/PT or T/CT, whichever is larger.

In practice, the actual PT is determined by batch size, compression algorithm, acknowledgement mechanism, number of replicas, and so on, while the actual CT is subject to business logic, which varies according to the actual conditions.

**We recommend that the number of partitions be greater than or equal to that of consumers to achieve maximum concurrency. For example, if there are 5 consumers, there should be 5 or more partitions.** However, having too many partitions will lower production throughput and increase time consumed by elections and thus need to be avoided. See the following for reference:
- A single partition can implement sequential writes of messages.
- A single partition can only be consumed by a single consumer process in the same consumer group.
- A single consumer process can consume multiple partitions simultaneously, so partition limits the concurrency of consumers.
- The more partitions there are, the longer it takes to elect a leader upon failure.
- Offset can be down to the partition level. The more partitions there are, the more time the offset query consumes.
- The number of partitions can be dynamically increased but not reduced. However, an increase will result in message rebalance.

#### 2. Number of replicas

At present, the number of replicas must be at least 2 to ensure availability. To ensure high reliability, we recommend maintaining at least 3 replicas.
>!The number of replicas will affect the production/consumption traffic; for example, if there are 3 replicas, the actual traffic will be 3 times the production traffic.

#### 3. Log retention period

The `log.retention.ms` configuration of a topic is set through the retention period of the instance in the console.

#### 4. Other topic-level configurations
```
# Maximum message length at the topic level.
max.message.bytes=1000012

# Messages in the 0.10.2 version are in the V1 format.
message.format.version=0.10.2-IV0

# Replica not in ISR can be selected as a leader; in this case, availability is higher than reliability, and there is a risk of data loss.
unclean.leader.election.enable=true

# Minimum number of replicas for producer requests submitted by ISR. If the number of replicas in synchronization is below this value, the server will no longer accept write requests where request.required.acks is set to -1 or all.
min.insync.replicas=1

```

## Producer Configuration Guide

The following describes common parameter settings for the Producer client. We recommend adjusting them based on your actual business scenarios:

```
# The producer will attempt to bundle and send the messages sent to the same partition by the business to the Broker. The batch.size parameter sets the maximum size of the bundle, which is 16 KB by default. If batch.size is too small, the throughput will drop; if it is too large, too much memory will be used.
batch.size=16384

# The following describes the 3 ACK mechanisms supported by a Kafka producer:
# -1 or all: the Broker responds to the producer and continues to send the next message or next batch of messages only after the leader receives the data and syncs it to followers in all ISRs. This configuration provides the highest data reliability, as messages will never be lost as long as one synced replica survives. Note: this configuration cannot ensure that replicas will be returned after the data is written to all of them. It can be used together with the min.insync.replicas parameter at the topic level.
# 0: the producer continues to send the next message or next batch of messages without waiting for acknowledgement of synchronization completion from the Broker. This configuration provides the highest production performance but lowest data reliability (data loss may occur when the server fails. If the leader is dead but the producer is unaware of that, the Broker cannot receive messages).
# 1: the producer sends the next message or next batch of messages after it receives an acknowledgement that the leader has successfully received the data. This configuration is a balance between production throughput and data reliability (messages may be lost if the leader is dead but has not been replicated yet).

# If users do not configure this, the default value will be 1. Users can customize this according to their business conditions.
acks=1

# Control the maximum time a production request waits in the Broker for replica synchronization to meet conditions set through acks.
timeout.ms=30000

# Configure the memory that the producer uses to cache messages to be sent to the Broker. Users must adjust this according to the total memory size of the process where the producer resides.
buffer.memory=33554432

# If messages are produced faster than they are sent by the sender thread to the Broker, the memory configured by buffer.memory will be used up and thus block the send operation by the producer. This parameter sets the maximum blocking time.
max.block.ms=60000

# Set the time to send the scheduled message, so that more messages can be sent in batches. This parameter is 0 by default, indicating immediate send. When the messages to be sent reach the size set by batch.size, the request will be sent immediately regardless of whether the time set by linger.ms is reached.
linger.ms=0

# Maximum size of the request packet that the producer can send, which defaults to 1 MB. Note: this value cannot exceed the maximum packet size of 16 MB configured for the Broker.
max.request.size=1048576

# Compression format configuration. Currently, version 0.9 and earlier do not support compression, and version 0.10 and later do not support gzip compression.
compression.type=[none, snappy, lz4]

# Timeout period for the client to send a request to the Broker, which cannot be smaller than the value of replica.lag.time.max.ms configured for the Broker. The current value is 10,000 ms.
request.timeout.ms=30000

# Maximum number of unacknowledged requests that the client can send on each connection. If this parameter is greater than 1 and retries is greater than 0, data may be out of order. If strict ordering is necessary, set this value to 1.
max.in.flight.requests.per.connection=5


# Number of retries upon request error. It is recommended that you set the parameter to a value greater than 0 to enable retries and ensure to the greatest extent that messages do not get lost.
retries=0

# Retry interval upon request failure.
retry.backoff.ms=100

```

## Consumer Configuration Guide

The following describes common parameter settings for the Consumer client. We recommend adjusting them based on your actual business scenarios:

```
# Whether to sync the offset to the Broker after a message is consumed, so the latest offset can be obtained from the Broker when the consumer fails.
auto.commit.enable=true

# Interval for the automatic submission of offset when auto.commit.enable=true is configured. We recommend setting this value to at least 1,000.
auto.commit.interval.ms=5000

# Mode to initialize the offset when no offset is configured for the Broker (such as upon initial consumption or when the offset expired for more than 7 days), or mode to reset the offset when error OFFSET_OUT_OF_RANGE occurs.
# earliest: reset to the minimum offset in the partition.
# latest: reset to the maximum offset in the partition. This is the default value.
# none: throw an OffsetOutOfRangeException exception without resetting the offset.
auto.offset.reset=latest

# Identify the consumer group to which the consumer belongs.
group.id=""

# Consumer timeout period when the Kafka consumer groups are used. If the Broker does not receive the heartbeat of the consumer within this period, the consumer will be considered to have failed and the Broker will initiate rebalance. Currently, this value must be configured in the Broker between 6000 (value of group.min.session.timeout.ms) and 300000 (value of group.max.session.timeout.ms).
session.timeout.ms=10000

# Interval at which the consumer sends a heartbeat when the Kafka consumer groups are used. This value must be smaller than the session.timeout.ms value, and is recommended to be smaller than one third of it.
heartbeat.interval.ms=3000

# Maximum interval allowed for calling the poll again when the Kafka consumer groups are used. If poll is not called within this time period, the consumer will be considered to have failed and the Broker will re-initiate rebalance to assign the partitions to other consumers.
max.poll.interval.ms=300000

# Minimum data size returned by a fetch request. The default value is 1 B, indicating that the request can be returned as soon as possible. Increasing this value will increase throughput and latency.
fetch.min.bytes=1

# Maximum data size returned by a fetch request. The default value is 50 MB.
fetch.max.bytes=52428800

# Fetch request wait time.
fetch.max.wait.ms=500

# Maximum data size returned by each partition in a fetch request. The default value is 1 MB.
max.partition.fetch.bytes=1048576

# Number of records returned in one poll call.
max.poll.records=500

# Client request timeout period. If no response is received after this time elapses, the request will time out and fail.
request.timeout.ms=305000
 
```
