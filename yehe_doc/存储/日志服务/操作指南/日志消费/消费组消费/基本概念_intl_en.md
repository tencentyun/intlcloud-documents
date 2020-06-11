## Consumer Group

A consumer group is the basic unit for managing real-time consumption of log topics. Consumer tasks in a consumer group are automatically load balanced without any topic partitioning operations on your part. Besides, consumer groups can save consumption progress and ensure breakpoint restart without repeated data consumption.

A log topic can be consumed by multiple consumer groups independently from one another. A consumer group can contain multiple consumers, between whom no repeated data is consumed.

A consumer group has 2 major attributes as follows:

#### Order
  Real-time consumption may be orderly or concurrent. You can determine which option to configure based on your business needs.
  - Orderly consumption (order = true)
    If `order` is set to `true`, topic partitions are consumed in order. When a topic partition is split, data in the original partition is consumed before that in the two new partitions. When two topic partitions are merged, data in the two original partitions is consumed before that in the new single partition.
  - Concurrent consumption (order = false)
    If `order` is set to `false`, topic partitions are consumed concurrently.

#### Timeout
  The service uses this attribute to determine whether a consumer is active. If a consumer reports a heartbeat beyond the preset time, the service determines the heartbeat times out and the consumer has been kept offline. If a consumer group receives no heartbeat within the preset time, the consumer group will be deleted.



## Consumer

A consumer is the unit that actually consumes data. Each consumer must have a unique name in a consumer group, and can consume data from all partitions of a log topic together with the other consumers in the same group through load balancing. Consumer tasks are automatically assigned to consumers in accordance with the following principles:

- Each consumer can consume multiple topic partitions.
- A topic partition can be consumed only by one consumer at a time.

When the number of consumers changes in a consumer group, consumer tasks are assigned automatically to achieve load balancing, with no work needed on your part.



## Consumer Heartbeat

Each consumer should regularly report a heartbeat to the server so that it can determine whether the consumer is active. Depending on the heartbeats it receives, a consumer group automatically assigns topic partitions to all active consumers through load balancing.



## Consumer Group Cursor

The consumer group cursor indicates the consumption progress of a partition. After each data consumption, the consumer should update the cursor to the consumer group so that it can easily assign consumer tasks through load balancing next time. When getting a partition-based consumer task, the consumer should also get the cursors of the current partitions from the consumer group.



## Diagram

![](https://main.qcloudimg.com/raw/9cec5013900ca9d5a9c32774d5a17804.png)

