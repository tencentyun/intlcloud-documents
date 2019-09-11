### Kafka Java Client Exceptions
#### The following are exceptions with client configuration or service, and the client will not automatically retry.

| Exception | Description | Analysis |
| ------ | ------ | ------ |
| UnknownServerException | An unknown error occurred when the server processed the request. | This error will be returned during traffic control in a legacy version. If it occurs in a new version, it may be caused by a server bug. |
| RecordTooLargeException | The message is too large. | The current configuration is message.max.bytes=1000012. |
| InvalidRequiredAcksException | The acks parameter configured for the producer is invalid. | |
| InconsistentGroupProtocolException | The protocol of the group is inconsistent. | Check whether the same group.id is configured for both the consumer and connector. They use different protocols and cannot join the same group. |
| InvalidGroupIdException | The consumer group ID is invalid. | It is recommended to use no more than 128 characters in the range of [a-zA-Z0-9._-]. |
| InvalidTopicException | The topic is invalid. | After the "auto-create topic" option is enabled, this exception will be returned if the topic used by the client is invalid. Check whether the topic name contains invalid characters or exceeds the length limit. |
| InvalidSessionTimeoutException | The session.timeout.ms configured for the consumer is invalid. | The current minimum and maximum values allowed by the server are group.min.session.timeout.ms=6000 and group.max.session.timeout.ms=300000, respectively. |
| InvalidCommitOffsetSizeException | The submitted offset information is too large and exceeds the maximum message size, so __consumer_offsets cannot be written. | The current configuration is message.max.bytes=1000012. |
| OffsetMetadataTooLarge | The metadata contained in the request to submit the offset is too large. | The server configuration is offset.metadata.max.bytes=4096. |
| UnsupportedVersionException | The broker does not support requests in this version. | It is recommended to use a v0.10.2.x client. |

#### The following exceptions may occur briefly during normal program operation, and the client will automatically retry. If an exception persists, the service is exceptional.

| Exception | Description | Analysis |
| ------ | ------ | ------ |
| TimeoutException | The request timed out. | If this exception is reported for the initial connection, check whether the address is correct and run telnet to confirm whether the network works. If this exception is thrown occasionally during program execution, it may be caused by network jitter. |
| CorruptRecordException | The message is invalid. | Possible reasons include the CRC check failed and the data size is invalid. In addition, this error will also be caused if the compression method used is **gzip** or **compression** is used in versions 0.9 and below. |
| UnknownTopicOrPartitionException | The topic or partition does not exist. | Go to the console to check whether the corresponding topic has been created. Note: The client produces and consumes through the TopicName instead of the TopicId. In addition, this error will also be caused if the client does not have permission to access the topic. |
| LeaderNotAvailableException | The partition has no leader. | If the topic is just created, the server has not selected the appropriate leader. In this case, this error will be returned to the client, and the client will automatically retry to get the leader information. **This exception is applicable to legacy versions only and has been removed since version 0.10.2.1.** |
| NotLeaderForPartitionException | The leader of the partition is unavailable. | As the client caches the topic's metadata, after the leader of the partition is changed, the production or consumption requests may still be sent to the old leader. In this case, this error will be returned to the client, and the client will automatically update the metadata. |
| NetworkException | The client connection is closed by the server. | The network is exceptional or the number of connections exceeds the limit. |
| NotEnoughReplicasException | The number of ISRs is insufficient. | The number of ISRs in the partition when data is written is smaller than the value of min.insync.replicas configured for the topic, possibly due to ISR jitter. |
| NotEnoughReplicasAfterAppendException | After data is written to the local broker, ISR jitter occurrs, making it unable to satisfy the configuration of min.insync.replicas. | | 

#### The following exceptions will occur if the log is configured as DEBUG and will be automatically processed by the client. 

| Exception | Description | Analysis |
| ------ | ------ | ------ |
| OffsetOutOfRangeException | The offset passed in when the consumer pulled messages was out of range. | If an offset reset policy (earliest or latest) is set for the client, the client will perform an offset reset according to the policy; otherwise, the user program needs to handle this exception. |
| GroupLoadInProgressException | The coordinator of the consumer group is being loaded. | This may occur briefly when the server is upgraded. The client will automatically retry. |
| GroupCoordinatorNotAvailableException | The coordinator is not available. | This may occur briefly when the server is upgraded. The client will automatically retry. |
| NotCoordinatorForGroupException | The current node is not the coordinator of the consumer group, and the coordinator has been migrated to another node. | This may occur briefly when the server is upgraded. The client will automatically retry. |
| IllegalGenerationException | The generation of the consumer group is invalid. | Possible reasons include heartbeat timed out or a new consumer joined. The consumer will automatically retry to join the consumer group. |
| RebalanceInProgressException | The consumer group is performing rebalance. | Possible reasons include heartbeat timed out or a new consumer joined. The consumer will automatically retry to join the consumer group. |
