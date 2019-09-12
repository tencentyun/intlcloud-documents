## Querying Consumer Groups
On the consumer group page, you can view the information of consumer groups in the current CKafka instance, including the status, protocol type, equalization algorithm, and operations. You can reset the offset for a topic subscribed to by a consumer group for consuming historical messages again.
![](https://main.qcloudimg.com/raw/cd3bc2bfb415909c6e666e5978ecc665.png)
- On the consumer group list page, click **View Consumer Details** in the Action column to view the information of consumers in the consumer group and the correspondence between a specific consumer and a topic subscribed to.
- On the consumer group list page, click the small triangle to the left of a consumer group name to display the information of the topic subscribed to by it, including the topic name, number of partitions, submitted offset position, maximum offset position, and number of unconsumed messages. Click **View Partition Details** in the Action column to view the offset consumption at the partition level.

>? As the offset information is maintained on the consumer side, the offset position is subject to the way the consumer submits the offset. It is displayed asynchronously and does not necessarily represent the real-time consumption conditions.

## Setting Offset 
In scenarios such as offline data processing, it is sometimes necessary to reset the offset for consuming previous messages. In this case, you can enable re-consumption by setting the offset.
1. In the consumer group list, click **Offset Settings**.
2. In the Offset Settings window, select the topic for which to reset the offset (if no topic is selected, the offset will be reset for all topics by default).
3. Specify the offset (in the following four ways):
 - Move the offset to the specified position
 - Move the offset forward or backward by several entries
 - Start the consumption at the latest or initial position
 - Reset the consumption position by time point
![](https://main.qcloudimg.com/raw/eaeeac6122be7335ba6d632aa940f5c4.png)

>!
- The offset value should be between the minimum offset and the maximum offset. If it is configured to be smaller than the minimum offset, the consumption will start from the minimum offset, and if it is greater than the maximum offset, the consumption will start from the maximum offset.
- You should make sure that there are no consumers in a consumer group first before you can reset the group.



## Consumer Group State Descriptions
The states of a consumer group on the consumer group list page mainly include Dead, Empty, PreparingRebalance, AwaitingSync, and Stable. Empty, Stable, and Dead are the most common ones. The state machine transformation of a consumer group is as shown below:
![](https://main.qcloudimg.com/raw/f35cb27ac35bef4628df17427e46c912.jpg)
- Dead: There are no members in the consumer group and the metadata has been removed.
- Empty: There are currently no members in the consumer group. If all offsets in the group have expired, the group will go into Dead state. Generally, a newly created group is in Empty state by default.
As required by the open-source Kafka v0.10.x, **a consumer group will be automatically deleted** if there are no members in it for more than 7 days.
- Stable: Each consumer in the consumer group has joined and is in stable state.

## Rebalance State Details
### Cause of Rebalance
According to the consumer group's state machine, when the consumer group is in Empty, AwaitSync, or Stable state, the group may perform rebalance. Rebalance may occur in the following situations:
- A consumer subscribes to a topic.
- A consumer is closed.
- A consumer is considered to be in Dead state by the group coordinator.
If a consumer does not send a heartbeat to the group coordinator within the period of `session.timeout.ms`, the consumer will be considered to be in Dead state and rebalance will be initiated. For more information, see [CKafka Common Parameter Configuration Guide](https://intl.cloud.tencent.com/document/product/597/31588).
- The number of partitions is increased.
- A topic that does not exist is subscribed to.
If a topic that has not been created yet is subscribed to, rebalance will occur when the topic is created. Similarly, if a topic that has already been subscribed to is deleted, rebalance will also occur.
- The application crashes.

### Rebalance Process Analysis
Taking the mechanism of Kafka v0.10 as an example, the rebalance process is analyzed as follows:
1. When any consumer wants to join a consumer group, it will send a JoinGroup request to the group coordinator. The first consumer that joins a group will become the group leader.
2. The leader will receive a list of all consumers in the group from the coordinator and will be responsible for assigning partitions to the consumers in the group. Partition assignment can be implemented through the PartitionAssignor API.
3. After the assignment is done, the leader will send the assignment result to the coordinator that will then send the result to all consumers.
Therefore, each consumer can view only the partition assigned to it. The leader is the only consumer that can get the information of consumers in the consumer group and their partitions.

The above process will be executed once each time rebalance occurs.

