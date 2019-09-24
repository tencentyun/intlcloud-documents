## Broker Configuration Parameter Descriptions.

Below are configurations of a CKafka broker for your reference:
```
# Maximum size of the message in bytes.
message.max.bytes=1000012

# Whether to allow auto creation of topics. Default value is false. Topics can be created in the console or through TencentCloud API. 
auto.create.topics.enable=false

# Whether to allow calling an API to delete a topic.
delete.topic.enable=true

# Maximum request size allowed for a broker is 16 MB. 
socket.request.max.bytes=16777216

# Each IP can establish up to 5,000 connections with a broker.
max.connections.per.ip=5000

# Offset retention period. Default value is 7 days.
offsets.retention.minutes=10080

# Allow anyone to access when there is no ACL configuration.
allow.everyone.if.no.acl.found=true

# Log segment size is 1 GB.
log.segment.bytes=1073741824

# Log rolling check interval is 5 minutes. If the retention period is set to less than 5 minutes, it may still take 5 minutes to clear the log.
log.retention.check.interval.ms=300000
```
>**Note:** For configurations not listed here, see [Kafka Default Configurations](http://kafka.apache.org/0102/documentation.html#brokerconfigs).

## Topic Configuration Parameter Descriptions.
#### 1. Select an appropriate number of partitions

From the producer's point of view, writes to different partitions are completely in parallel; from the consumer's point of view, the number of concurrencies depends entirely on the number of partitions (if there are more consumers than partitions, there will definitely be idle consumers). It is important to select an appropriate number of partitions for the performance of the CKafka instance.
The number of partitions should be determined based on the throughput of production and consumption, ideally through the following formula:
>**Num = max(T/PT, T/CT) = T/min(PT, CT)**

Num represents the number of partitions, T the target throughput, PT the maximum production throughput by the producer to a single partition, and CT the maximum consumption throughput by the consumer from a single partition. The number of partitions should equal to T/PT or T/CT, whichever is larger.

In practice, the actual PT is subject to batch size, compression algorithm, acknowledgment mechanism, number of replicas and so on, while the actual CT is subject to business logic, which needs to be measured in actual scenarios.

**We recommend that the number of partitions be greater than or equal to that of consumers to achieve maximum concurrency. For example, if there are 5 consumers, there should be 5 or more partitions.** However, having too many partitions will lower production throughput and increase time consumed by elections and should thus be avoided. See the following information for reference:
- A single partition can implement sequential writes of messages.
- A single partition can only be consumed by a single consumer process in the same consumer group.
- A single consumer process can consume multiple partitions simultaneously, so partition limits the concurrency of consumers.
- The more partitions there are, the longer it takes to elect a leader upon failure.
- Offset can be down to the partition level. The more partitions there are, the more time-consuming the offset query is.
- The number of partitions can be dynamically increased but not reduced. However, an increase will result in message rebalance.

#### 2. Select an appropriate number of replicas

At present, the number of replicas must be at least 2 to ensure availability. To ensure high reliability, we recommend maintaining at least 3 replicas.
>**Note:** The number of replicas will affect the production/consumption traffic; for example, if there are 3 replicas, the actual traffic will be production traffic * 3.

#### 3. Log retention period

The log.retention.ms configuration of a topic is set through the retention period of the instance in the console.

#### 4. Descriptions of other topic-level configurations
```
# Maximum message size at the topic level.
max.message.bytes=1000012

# Message format is the same in v0.10.2 and v1.
message.format.version=0.10.2-IV0

# Replica not in ISR can be selected as a leader; in this case, availability is higher than reliability, and there is a risk of data loss.
unclean.leader.election.enable=true

# Minimum number of replicas for producer requests submitted by ISR. If the number of replicas in synchronization is below this value, the server will no longer accept write requests where request.required.acks is -1 or all.
min.insync.replicas=1

```

## Producer Configuration Guide.

Below are common producer configuration parameters. We recommend adjusting them based on your actual business scenarios:

```
# The producer will attempt to bundle and send the messages sent to the same partition by the business to the broker. Batch.size sets the maximum size of the bundle, which is 16 KB by default. If batch.size is too small, the throughput will drop; if it is too large, too much memory will be used.
batch.size=16384

# There are three ack mechanisms for a Kafka producer as described below:
# -1 or all: The broker responds to the producer and continues to send the next message or next batch of messages only after the leader receives the data and synchronizes it to followers in all ISRs. This configuration provides the highest data reliability, as messages will never be lost as long as one synced replica survives. Note: This configuration cannot ensure that replicas will be returned after the data is written to all of them. It can be used together with the min.insync.replicas parameter at the topic level.
# 0: The producer continues to send the next message or next batch of messages without waiting for acknowledgment of synchronization completion from the broker. This configuration provides the highest production performance but lowest data reliability (data loss may occur when the server fails. If the leader is dead but the producer is unaware of that, the broker cannot receive messages).
# 1: The producer sends the next message or next batch of messages after it receives an acknowledgment that the leader has successfully received the data. This configuration is a balance between production throughput and data reliability (messages may be lost if the leader is dead but has not been replicated yet).

# If users do not configure this, the default value will be 1. Users can customize this according to their business conditions.
acks=1

# Control the maximum time a production request waits in the broker for replica synchronization to meet conditions set by acks.
timeout.ms=30000

# Configure the memory that the producer uses to cache messages to be sent to the broker. Users should adjust this according to the total memory size of the process where the producer resides.
buffer.memory=33554432

# If messages are produced faster than sent by the sender thread to the broker, the memory configured by buffer.memory will be used up and thus block the send operation by the producer. This parameter sets the maximum blocking time.
max.block.ms=60000

# Maximum number of unacknowledged requests that the client can send on each connection. If this parameter is greater than 1 and retries is greater than 0, data may become out of order. If strict ordering is necessary, we recommend setting this value to 1.
max.in.flight.requests.per.connection=5

# Set the time to send the scheduled message, so more messages can be sent in batches. This parameter is 0 by default, indicating to send immediately. When the messages to be sent reach the size set by batch.size, the request will be sent immediately regardless of whether the time set by linger.ms is reached.
linger.ms=0

# Maximum size of the request packet that the producer can send is 1 MB by default. Note: This value cannot exceed the maximum packet size of 16 MB configured for the broker.
max.request.size=1048576

# Compression format configuration. Currently, version 0.9 and below do not support compression, and versions 0.10 and above do not support gzip compression.
compression.type=[none, snappy, lz4]

# Timeout period for the client to send a request to the broker cannot be smaller than the replica.lag.time.max.ms configured for the broker. Current value is 10,000 ms.
request.timeout.ms=30000

# Number of retries upon request error. We recommend setting the value to be larger than 0 to ensure minimal message loss when retrying.
retries=0

# Time between when a request fails and the next time the request is retried.
retry.backoff.ms=100

```

## Consumer Configuration Guide.

Below are common consumer configuration parameters. We recommend adjusting them based on your actual business scenarios:

```
# Whether to sync the offset to the broker after a message is consumed, so the latest offset can be obtained from the broker when the consumer fails.
auto.commit.enable=true

# Interval for the auto submission of offset when auto.commit.enable=true. We recommend setting this value to at least 1,000.
auto.commit.interval.ms=5000

# How to initialize the offset when there is no offset on the broker (for example, during initial consumption or when the offset expired more than 7 days ago), and how to reset the offset when an OFFSET_OUT_OF_RANGE error is received.
# earliest: reset to the minimum offset in the partition.
# latest: this is the default value, indicating to reset to the maximum offset in the partition.
# none: will throw an OffsetOutOfRangeException exception and not automatically reset the offset.
auto.offset.reset=latest

# Identify the consumer group to which the consumer belongs.
group.id=""

# Consumer timeout period when the Kafka consumer groups mechanism is used. If the broker does not receive the heartbeat of the consumer within this period, the consumer will be considered to have failed and the broker will initiate rebalance. Currently, this value must be configured in the broker between group.min.session.timeout.ms=6000 and group.max.session.timeout.ms=300000.
session.timeout.ms=10000

# Interval at which the consumer sends a heartbeat when the Kafka consumer groups mechanism is used. This value should generally be smaller than one-third of the session.timeout.ms value.
heartbeat.interval.ms=3000

# Maximum interval allowed for calling the poll again when the Kafka consumer groups mechanism is used. If poll is not called again within this time period, the consumer will be considered to have failed and the broker will re-initiate rebalance to assign the partitions to other consumers.
max.poll.interval.ms=300000

# Minimum data size returned by a fetch request. The default value is 1 B, indicating that the request can be returned as soon as possible. Increasing this value will increase throughput and latency.
fetch.min.bytes=1

# Maximum data size returned by a fetch request. The default value is 50 MB.
fetch.max.bytes=52428800

# Fetch request wait time.
fetch.max.wait.ms=500

# Maximum data size returned by each partition in a fetch request. The default value is 10 MB.
max.partition.fetch.bytes=1048576

# Number of records returned in one poll call.
max.poll.records=500

# Client request timeout period. If no response is received after this time elapses, the request will time out and fail.
request.timeout.ms=305000
 
```
