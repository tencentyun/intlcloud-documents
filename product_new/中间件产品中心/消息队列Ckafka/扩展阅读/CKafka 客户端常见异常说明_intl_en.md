### Kafka Java Client Exceptions
#### The following are client configuration or services exceptions. For these cases, the client will not automatically retry.

| Exception | Description | Analysis |
| ------ | ------ | ------ |
| UnknownServerException | An unknown error occurred when the server processed the request. | Error will be returned during traffic control in the legacy version. If it occurs in the new version, it may be caused by a server bug. |
| RecordTooLargeException | Message is too large. | Current configuration is message.max.bytes=1000012. |
| InvalidRequiredAcksException | Acks parameter configured for the producer is invalid. | |
| InconsistentGroupProtocolException | Group protocol is inconsistent. | Check whether the same group.id is configured for the consumer and the connector. They cannot join the same group if different protocols are used. |
| InvalidGroupIdException | Consumer group ID is invalid. | Use no more than 128 characters such as [a-zA-Z0-9._-]. |
| InvalidTopicException | Topic is invalid. | When topic auto-creation is enabled, an exception will be returned if the client uses an invalid topic. Check whether the topic name contains invalid characters or exceeds the length limit. |
| InvalidSessionTimeoutException | Session.timeout.ms configured for the consumer is invalid. | Current minimum and maximum values allowed by the server are group.min.session.timeout.ms=6000 and group.max.session.timeout.ms=300000. |
| InvalidCommitOffsetSizeException | Submitted offset information is too large and exceeds the maximum message size, so __consumer_offsets cannot be written. | Current configuration is message.max.bytes=1000012. |
| OffsetMetadataTooLarge | Metadata contained in the request to submit the offset is too large. | Server configuration is offset.metadata.max.bytes=4096. |
| UnsupportedVersionException | Broker does not support requests in this version. | We recommend using a v0.10.2.x client. |

#### The following exceptions may occur briefly during normal program operation, and the client will automatically retry. If an exception persists, it means there is an issue with the service.

| Exception | Description | Analysis |
| ------ | ------ | ------ |
| TimeoutException | Request timeout. | If the initial connection reports a request timeout, check whether the address is correct and run telnet to confirm whether the network works. If this exception occurs only occasionally during program execution, it may be caused by network jitters. |
| CorruptRecordException | Message is invalid. | Possible causes include CRC error or invalid data size. This exception may also occur if the compression method used is **gzip** or **the version is below 0.9**. |
| UnknownTopicOrPartitionException | Topic or partition does not exist. | Go to the console to check whether the corresponding topic has been created. Note: The client produces and consumes through TopicName rather than TopicId. This exception will also occur if the client does not have permission to access the topic. |
| LeaderNotAvailableException | Partition has no leader. | When the topic is just created, the server has not selected the appropriate leader. An error will be returned to the client and the client will automatically retry to get the leader information. **Only the legacy version has this exception, which has been removed from 0.10.2.1.** |
| NotLeaderForPartitionException | Partition leader is unavailable. | As the client caches the metadata of the topic, when the partition leader changes, the production or consumption requests may still be sent to the old leader. An error will be returned to the client and the client will automatically update the metadata. |
| NetworkException | Client connection is closed by the server. | Network exception or the number of connections exceeds the limit. |
| NotEnoughReplicasException | Number of ISR is insufficient. | The number of ISR in the partition when data is written is smaller than the value of min.insync.replicas configured for the topic, which may be caused by ISR jitters. |
| NotEnoughReplicasAfterAppendException | ISR jitters occur after data is written to the local broker, making it unable to satisfy the configuration of min.insync.replicas. | | 

#### The following exceptions will occur if the log is configured as DEBUG and will be automatically processed by the client. 

| Exception | Description | Analysis |
| ------ | ------ | ------ |
| OffsetOutOfRangeException | Offset passed in was out of range for consumer pulled messages. | If an offset reset policy (earliest or latest) is configured for the client, the client will reset the offset according to the policy; otherwise, the user application needs to handle this exception. |
| GroupLoadInProgressException | Coordinator of the consumer group is being loaded. | This may occur briefly when the server is being upgraded. The client will automatically retry. |
| GroupCoordinatorNotAvailableException | Coordinator is not available. | This may occur briefly when the server is being upgraded. The client will automatically retry. |
| NotCoordinatorForGroupException | Current node is not the coordinator of the consumer group, and the coordinator has been migrated to another node. | This may occur briefly when the server is being upgraded. The client will automatically retry. |
| IllegalGenerationException | Generation of the consumer group is invalid. | Possible causes include heartbeat timed out or a new consumer joined the group. The consumer will automatically retry joining the consumer group. |
| RebalanceInProgressException | Consumer group is rebalancing. | Possible causes include heartbeat timed out or a new consumer joined the group. Consumer will automatically retry joining the consumer group. |
