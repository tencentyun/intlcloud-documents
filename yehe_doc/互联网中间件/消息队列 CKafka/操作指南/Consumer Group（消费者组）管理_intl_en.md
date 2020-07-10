## Querying Consumer Group
On the consumer group page, you can view information of consumer groups in the current CKafka instance, including status, protocol type, balancing algorithm, and operations. You can reset the offset for a topic subscribed to by a consumer group and consume message history again.
![](https://main.qcloudimg.com/raw/eaeeac6122be7335ba6d632aa940f5c4.png)
- On the consumer group list page, click **View Consumer Details** in the "Operation" column to view the information of consumers in the consumer group and the relationship between a consumer and the topic subscribed to by this consumer.
- On the consumer group list page, click the small triangle on the left of the consumer group name to display information of the topic subscribed to by this consumer group, including topic name, number of partitions, submitted offset position, maximum offset position, and number of unconsumed messages. Click **View Partition Details** in the "Operation" column to view offset consumption at the partition level.

>?As the offset information is maintained on the consumer side, the offset position is subject to the way the consumer submits the offset. It is displayed asynchronously and does not necessarily represent real-time consumption conditions.

## Setting Offset 
In scenarios such as offline data processing, sometimes it is necessary to reset the offset to consume message history. In this case, you can enable re-consumption by setting the offset.
1. In the consumer group list, click **Offset Settings**.
2. In the Offset Settings window, select the topic for which to reset the offset (if no topic is selected, the offset will be reset for all topics by default).
3. Specify the offset (in the following four ways):
 - Move the offset to the specified position
 - Move the offset forward or backward by several entries
 - Start the consumption at the latest or initial position
 - Reset the consumption position by point in time
![](https://main.qcloudimg.com/raw/cd3bc2bfb415909c6e666e5978ecc665.png)

>!
- Offset value should be between the minimum offset and the maximum offset. If it is configured to be smaller than the minimum offset, the consumption will start from the minimum offset; if it is larger than the maximum offset, the consumption will start from the maximum offset.
- Make sure there are no consumers in a consumer group before resetting the group.



## Consumer Group Status Description
The consumer group list page includes Dead, Empty, Preparing Rebalance, AwaitingSync, and Stable states. Most common ones are Empty, Stable, and Dead. The transformation of the consumer group's state machine is as shown below:
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
- Number of partitions has increased.
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

