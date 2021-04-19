## Consumer Group Status Description

A consumer group can be in Dead, Empty, Preparing Rebalance, AwaitingSync, or Stable state. Most common states are Empty, Stable, and Dead. The transformation of the consumer group's state machine is as shown below:
![](https://main.qcloudimg.com/raw/f35cb27ac35bef4628df17427e46c912.jpg)

- Dead: consumer group does not have any members and metadata has been removed.
- Empty: consumer group currently does not have any members. If all offsets in the group have expired, the group’s state will be Dead. Generally, a newly created group is in Empty state by default.
  As required by the open-source Kafka v0.10.x, **a consumer group will be automatically deleted if it does not have any members for more than 7 days.**
- Stable: every consumer in the consumer group has joined and the state is stable.

## Rebalance State Details

### Cause of rebalance

According to the consumer group's state machine, the group may perform rebalance when the consumer group is in Empty, AwaitingSync, or Stable state. Rebalance may occur in the following scenarios:

- A consumer subscribes to a topic.
- A consumer is closed.
- A consumer is considered to be in Dead state by the group coordinator.
  If a consumer does not send a heartbeat to the group coordinator within the `session.timeout.ms` time period, the consumer will be considered to be in Dead state and rebalance will be initiated. For more information, please see [CKafka Common Parameter Configuration Guide](https://intl.cloud.tencent.com/document/product/597/31588).
- The number of partitions has increased.
- A topic that does not exist is subscribed to.
  If you subscribe to a topic that has not been created yet, rebalance will occur when the topic is created. Similarly, if a topic that has already been subscribed to is deleted, rebalance will also occur.
- Application crashes.

### Rebalance process analysis

Taking the mechanism of Kafka v0.10 as an example, the rebalance process is analyzed as follows:

1. A consumer that wants to join a consumer group will send a JoinGroup request to the group coordinator. The first consumer to join a group will become the group leader.
2. The leader will receive a list of all consumers in the group from the coordinator and will be responsible for assigning partitions to consumers in the group. Partition assignment can be implemented through the PartitionAssignor API.
3. When the assignment is done, the leader will send the assignment result to the coordinator. The coordinator will then send the result to all consumers.
   Each consumer can only view the partition assigned to it. The leader is the only consumer that can get the information of consumers in the consumer group and their partitions.

The above process will be executed once whenever rebalance occurs.
