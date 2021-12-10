## Apache Pulsar Architecture

Apache Pulsar is a messaging system built on the publish-subscribe pattern, which consists of broker, Apache BookKeeper, producer, consumer, and other components.

![](https://qcloudimg.tencent-cloud.cn/raw/b538fed55e55478345e6b7721d909e0c.svg)

- Producer: message producer, which is responsible for publishing messages to topics.
- Consumer: message consumer, which is responsible for subscribing to messages from topics.
- Broker: stateless service layer, which is responsible for receiving and transferring messages, balancing cluster load, and performing other tasks. It does not store metadata persistently, so it can be connected and disconnected quickly.
- Apache BookKeeper: stateful persistence layer, which consists of a set of Bookie storage nodes and can store messages persistently.

Apache Pulsar adopts the computing-storage separation architecture, where the computing logic related to message publishing and subscription is implemented in brokers, and data is stored on the bookie nodes in an Apache BookKeeper cluster.

## Topic and Partition

Topic is a category name where messages are stored and published. Producers write messages to topics, and consumers read the messages from these topics.

Pulsar topics are divided into partitioned topic and non-partitioned topic, with the latter referring to a topic with 1 partition. In fact, topic is a virtual concept in Pulsar, and a 3-partition topic actually refers to three partitioned topics, and messages sent to a 3-partition topic will be sent to these three partitioned topics.
For example, if a producer sends a message to a 3-partition topic named `my-topic`, the message is actually sent to the 3 partitioned topics `my-topic-partition-0`, `my-topic-partition-1`, and `my-topic-partition-2` evenly or according to a rule (if a key is specified).

When partitioned topics persistently store data, partition is a logical concept, and the actual storage unit is segment.

As shown below, data in the `Topic1-Part2` partition consists of N segments, each of which is evenly distributed and stored on multiple bookie nodes in the Apache BookKeeper cluster and has 3 replicas.

![](https://main.qcloudimg.com/raw/66aeaa4a39be02e3c61245694ec6b07c.svg)

## Physical Partition and Logical Partition

Logical partitions and physical partitions are compared as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/18fdf7369f8471797e3863bdd21e19d2.svg)

**Physical partition:** computing and storage are coupled, fault tolerance requires copying physical partitions, and capacity expansion requires migrating physical partitions to implement load balancing.

**Logical partition**: physical segment where the computing layer is isolated from the storage layer. With this structure, Apache Pulsar has the following strengths:

- Brokers and bookies are independent of each other, making it easier to implement separate capacity expansion and fault tolerance.
- Brokers are stateless, so that they can be connected and disconnected quickly, making them more suitable for cloud native scenarios.
- Partitioned storage is not limited by the storage capacity of a single node.
- Partitioned data is evenly distributed. In this way, the excessive amount of data in a single partition will not cause the entire cluster to overflow.
- During storage capacity expansion, new nodes can be quickly added to share the storage load.
