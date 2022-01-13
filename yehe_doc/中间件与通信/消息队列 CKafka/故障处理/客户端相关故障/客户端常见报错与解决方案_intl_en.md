
## Client Configuration or Service Exceptions
The following describes client configuration or service exceptions. If any of the following exceptions occurs, the client will not automatically retry.

| Exception | Description | Analysis |
| ------ | ------ | ------ |
| UnknownServerException | An unknown error occurred when the server processed the request. | The error will be returned during traffic throttling in the legacy version. If it occurs in the new version, it may be caused by a server bug. |
| RecordTooLargeException | Message is too large. | The current configuration is `message.max.bytes=1000012`. |
| InvalidRequiredAcksException | The `acks` parameter configured for the producer is invalid. | - |
| InconsistentGroupProtocolException | Group protocol is inconsistent with the client protocol. | Check whether the same `group.id` is configured for the consumer and the connector. They cannot join the same group if different protocols are used. |
| InvalidGroupIdException | Consumer group ID is invalid. | Use no more than 128 characters such as a-z, A-Z, 0-9, and ._-. |
| InvalidTopicException | Topic is invalid. | When topic auto-creation is enabled, an exception will be returned if the client uses an invalid topic. Check whether the topic name contains invalid characters or exceeds the length limit. |
| InvalidSessionTimeoutException | `Session.timeout.ms` configured for the consumer is invalid. | Current minimum and maximum values allowed by the server are 6000 (value of `group.min.session.timeout.ms`) and 300000 (value of `group.max.session.timeout.ms`). |
| InvalidCommitOffsetSizeException | Submitted offset information is too large and exceeds the maximum message size, so `__consumer_offsets` cannot be written. | Current configuration is `message.max.bytes=1000012`. |
| OffsetMetadataTooLarge | Metadata contained in the request to submit the offset is too large. | `offset.metadata.max.bytes=4096` is configured for the server. |
| UnsupportedVersionException | Broker does not support requests in this version. | We recommend using a v0.10.2.x client. |

## Brief Exceptions That Occur During Normal Program Operation
The following exceptions may occur briefly during normal program operation, and the client will automatically retry. If an exception persists, the service will run improperly.

| Exception | Description | Analysis |
| ------ | ------ | ------ |
| TimeoutException | Request timeout. | If the initial connection reports a request timeout, check whether the address is correct and run telnet to confirm whether the network works properly. If this exception occurs only occasionally during program execution, it may be caused by network jitters. |
| CorruptRecordException | Message is invalid. | Possible causes include CRC error or invalid data size. This exception may also occur if the compression method used is **gzip** or **the version is below 0.9**. |
| UnknownTopicOrPartitionException | Topic or partition does not exist. | Go to the console to check whether the corresponding topic has been created. Note: the client produces and consumes through `TopicName` rather than `TopicId`. This exception will also occur if the client does not have permission to access the topic. |
| LeaderNotAvailableException | Partition has no leader. | When the topic has just been created yet the server has not selected the appropriate leader, an error will be returned to the client, and the client will automatically retry to get the leader information. **Only the legacy version has this exception, which has been removed from 0.10.2.1.** |
| NotLeaderForPartitionException | Partition leader is unavailable. | As the client caches the metadata of the topic, when the partition leader changes, production or consumption requests may still be sent to the original leader. An error will be returned to the client and the client will automatically update the metadata. |
| NetworkException | Client connection is closed by the server. | Network exception or the number of connections exceeds the limit. |
| NotEnoughReplicasException | Number of ISRs is insufficient. | The number of ISRs in the partition when data is written is smaller than the value of `min.insync.replicas` configured for the topic, which may be caused by ISR jitters. |
| NotEnoughReplicasAfterAppendException | ISR jitters occur after data is written to the local broker, making the configuration of `min.insync.replicas` unsatisfied. | - | 
| BrokerNotAvailableError | Partition leader is not found. | As the client caches the metadata of the topic, when the partition leader changes, the production or consumption requests may still be sent to the original leader. An error will be returned to the client and the client will automatically update the metadata. After the leader changes, new production requests sent to the original leader will be automatically forwarded to the new leader upon this error reporting. Theoretically, the integrity of consumption data written will not be affected. |
| NotLeaderForPartitionError | Partition leader is not found. | As the client caches the metadata of the topic, when the partition leader changes, production or consumption requests may still be sent to the original leader. An error will be returned to the client and the client will automatically update the metadata. After the leader changes, new production requests sent to the original leader will be automatically forwarded to the new leader upon this error reporting. Theoretically, the integrity of consumption data written will not be affected. |

## Exceptions That Occur When Log Level Is Configured as DEBUG
The following exceptions will occur if the log level is configured as DEBUG and will be automatically processed by the client. 

| Exception | Description | Analysis |
| ------ | ------ | ------ |
| OffsetOutOfRangeException | Offset passed in was out of range when consumer pulled messages. | If an offset reset policy (earliest or latest) is configured for the client, the client will reset the offset according to the policy; otherwise, the user application needs to handle this exception. |
| GroupLoadInProgressException | Coordinator of the consumer group is being loaded. | This may occur briefly when the server is being upgraded. The client will automatically retry. |
| GroupCoordinatorNotAvailableException | Coordinator is not available. | This may occur briefly when the server is being upgraded. The client will automatically retry. |
| NotCoordinatorForGroupException | The current node is not the coordinator of the consumer group, and the coordinator has been migrated to another node. | This may occur briefly when the server is being upgraded. The client will automatically retry. |
| IllegalGenerationException | `Generation` of the consumer group is invalid. | Possible causes include heartbeat timing out or a new consumer joining the group. The consumer will automatically retry joining the consumer group. |
| RebalanceInProgressException | Consumer group is rebalancing. | Possible causes include heartbeat timing out or a new consumer joining the group. The consumer will automatically retry joining the consumer group. |


