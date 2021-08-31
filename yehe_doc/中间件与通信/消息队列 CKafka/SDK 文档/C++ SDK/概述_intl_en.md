[C/C++ SDK](https://github.com/edenhill/librdkafka) can access CKafka via different types of access points to send and receive messages. This document introduces only part of the configuration. For more information on the configuration, see [C/C++ SDK configuration list](https://github.com/edenhill/librdkafka/blob/master/CONFIGURATION.md) and [Configuration Guide for Common Parameters in CKafka](https://intl.cloud.tencent.com/document/product/597/31588).



## Global Configuration

| **Parameter**          | **Default Value** | **Description**                                                     |
| :------------------ | ---------- | ------------------------------------------------------------ |
| api.version.request | true       | Kafka message format version negotiation. You are advised to enable this feature. Kafka supports multiple message formats, and a client needs to query the message format supported by the broker first and then adapt to the version returned by the broker. |
| debug               | none       | Debugging information display. Debugging information is not printed by default. In this document, this parameter is set to `all` (printing all debugging information) to facilitate debugging. Please be careful when setting this parameter during online business deployment. |

## Producer Configuration

| **Parameter**          | **Default Value** | **Description**                                                     |
| :--------------- | ---------- | ------------------------------------------------------------ |
| acks             | -1         | Kafka producer supports 3 ACK mechanisms:<li> -1 or all: the broker responds to the producer and continues to send the next message or next batch of messages only after the leader receives the data and syncs it to followers in all ISRs. This configuration provides the highest data reliability, as messages will never be lost as long as one synced replica survives. Note: this configuration cannot ensure that replicas will be returned after the data is written to all of them. It can be used together with the `min.insync.replicas` parameter at the topic level.</li><li>0: the producer continues to send the next message or next batch of messages without waiting for acknowledgement of synchronization completion from the broker. This configuration provides the highest production performance but lowest data reliability (data loss may occur when the server fails. If the leader is dead but the producer is unaware of that, the broker cannot receive messages).</li><li>1: the producer sends the next message or next batch of messages after it receives an acknowledgement that the leader has successfully received the data. This configuration is a balance between production throughput and data reliability (messages may be lost if the leader is dead but has not been replicated yet).<br>If you do not specify a value, the default value will be 1. You can customize this parameter according to your business requirements.</li> |
| linger.ms        | 5          | Path to obtain the value: [CKafka console](https://console.cloud.tencent.com/ckafka) -> **Basic Info** -> **Access Mode** -> **Public domain name access**. |
| compression.type | none       | Compression format. Currently, version 0.9 and below do not support compression, and versions 0.10 and above do not support Gzip compression. |
| retries          | 2147483647 | Number of retries upon request error. It is recommended that you set the parameter to a value greater than 0 to enable retries and ensure to the greatest extent that messages do not get lost. |
| retry.backoff.ms | 100        | Retry interval upon request failure.                   |

## Consumer Configuration

| **Parameter**          | **Default Value** | **Description**                                                     |
| :---------------------- | ---------- | ------------------------------------------------------------ |
| enable.auto.commit      | true       | Whether to sync the offset to the broker after a message is consumed, so that the latest offset can be obtained from the broker when the consumer fails. |
| auto.commit.interval.ms | 5000       | Interval for the automatic submission of offset when `auto.commit.enable` is set to `true`. We recommend setting this value to at least 1,000. |
| auto.offset.reset       | largest    | How to initialize the offset when there is no offset on the broker (such as upon initial consumption or when the offset expires for more than 7 days), or how to reset the offset when an `OFFSET_OUT_OF_RANGE` error is received. <li>earliest: reset to the minimum offset in the partition. </li><li>latest: reset to the maximum offset in the partition. This is the default value. </li><li>none: throw an `OffsetOutOfRangeException` exception without resetting the offset.</li> |
| session.timeout.ms      | 10000      | Consumer timeout period when Kafka consumer groups are used. If the broker does not receive the heartbeat of the consumer within this period, the consumer will be considered to have failed and the broker will initiate rebalance. Currently, the value must be in the allowable range (6,000-300,000) as configured in the broker configuration by `group.min.session.timeout.ms` and `group.max.session.timeout.ms`. |
| heartbeat.interval.ms   | 3000       | Interval at which the consumer sends a heartbeat when Kafka consumer groups are used. This value must be smaller than the value of `session.timeout.ms` and is recommended to be smaller than one third of the value. |



The C/C++ SDK can access CKafka via different types of access points to send and receive messages.

| Item     | **Default Access Point**         | **SASL Access Point**                                               |
| :------- | ---------------------- | ------------------------------------------------------------ |
| Network     | VPC                    | VPC/Public network                                                     |
| Protocol     | PLAINTEXT              | SASL_PLAINTEXT                                               |
| Port     | 9092                   | Please obtain the SASL access point information in the **Access Mode** area in the **Basic Info** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka).<br>![](https://main.qcloudimg.com/raw/75cea90d71b66617a7830bfe15aa924a.png) |
| SASL mechanism | N/A                 | PLAIN (a simple username/password authentication mechanism)                       |
| Demo     | [PLAINTEXT](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/cppkafkademo)          | [SASL_PLAINTEXT/PLAIN](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/cppkafkademo)                                     |
| Document     | [Using the Default Access Point to Send and Receive Messages](https://intl.cloud.tencent.com/document/product/597/40065) | [Using the SASL Access Point and PLAIN Mechanism to Send and Receive Messages](https://intl.cloud.tencent.com/document/product/597/40066)                             |
