## Consumption Process of Consumer Groups

When you use consumer groups to consume data, the server manages the consumption tasks of all consumers in each consumer group, and automatically balances consumption tasks according to the relationship between topic partitions and consumer counts. At the same time, it also records the consumption progress of each topic partition to avoid repeat consumption. The process by which a consumer group consumes data is as follows:

1. Create a consumer group.
2. Every consumer regularly sends heartbeats to the server.
3. The consumer group automatically assigns topic partitions to consumers according to the load of the topic partitions.
4. Consumers obtain partition cursors and consume data according to their assigned partition lists.
5. Consumers update partition consumption progress periodically to the consumption group for it to assign tasks the next time.
6. Repeat steps 2 - steps 6 until consumption ends.



## Load Balancing Consumption

A consumer group adjusts the consumption tasks for each consumer based on the number of active consumers and topic partitions to maintain consumption balance. At the same time, every consumer saves the consumption progress of each topic partition in order to continue the consumption after a failover and avoid repeat consumption.

#### Example 1: change of topic partitions

For example, a log topic has two consumers. Consumer A consumes partitions 1 and 2, and consumer B consumes partitions 3 and 4. When partition 5 is added after a splitting operation, the consumer group automatically assigns partition 5 to consumer B, as shown in the following figure.
![1561034489523](https://main.qcloudimg.com/raw/96e552cfe73f842a2212b218f9c3fa10.png)



#### Example 2: change of consumers

For example, a log topic has two consumers. Consumer A consumes partitions 1, 2, and 3, and consumer B consumes partitions 4, 5, and 6. In order for the consumption rate to keep up with the production rate, consumer C is added. The consumer group assigns partitions 3 and 4 to consumer C for balance, as shown in the following figure.
![1561035193214](https://main.qcloudimg.com/raw/9fa176361f303f4f28d5c7667957d9ee.png)



## Order Consumption

When the order field of a consumption group is set to true, the consumption group will consume partitions in chronological order. For example, a log topic has three partitions. After partition 3 is split into two new partitions, the consumer group first consumes data in partition 3 and then consumes data in the two new partitions derived from partition 3 in parallel, as shown in the following figure.
![1561036291236](https://main.qcloudimg.com/raw/501a5daa40ad3c69cc4f166352713ae2.png)
