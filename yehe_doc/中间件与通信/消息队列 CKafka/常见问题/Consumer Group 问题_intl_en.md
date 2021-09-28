### What should I do if details are missing in the consumer group list?

#### Error description

The consumer group list in the CKafka console contains consumer group name, but no consumption details are displayed on the details page; for example, the consumer group CR has no details displayed in the figure below:
![](https://main.qcloudimg.com/raw/40abecbbf024dab703c1904c006c04d0.png)

#### Possible causes

There are two data consumption modes in Kafka: consumer group mode and custom partition consumption mode.

- When consumption is performed in consumer group mode, the client will coordinate consumption through the consumption coordinator, and after data consumption is completed, it will send an offset storage request to the server, which will store information such as the consumed topic, partition progress, and client.
- When consumption is performed in custom partition consumption mode, the client will not automatically submit an offset storage request to the server. In this case, the server will not be able to see information related to consumption.
- After an ACL is set for a topic, you may not be able to view the consumer group details on some instances. In this case, please check whether there are any ACLs, and if so, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.


#### Solutions

1. View the consumer groups of the instance.
   ```
   ]$ bin/kafka-consumer-groups.sh --bootstrap-server 9.146.153.249:9092 --list
   CR
   ```
   You should be able to see the names of all current consumer groups.  

2. View the details of a specific consumer group of the instance.
   ```
   ]$ bin/kafka-consumer-groups.sh --bootstrap-server 9.146.153.249:9092 --describe --group CR
   Note: This will not show information about old Zookeeper-based consumers.
   ```
   You will find that there are no details for this consumer group, which means that the consumer client did not use the `consumerGroup` mechanism to consume data, that is, the client did not submit consumption details to the server. As the server did not store the consumption data, no details will be displayed.

3. Check whether the problem is caused by the server.
   Use the native consumer group command to specify the consumer group `test1` for consumption as shown below: 
   ```
   ]$ bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --from-beginning --topic test --group test1
   ```
   You should be able to see the normally displayed consumer group in the console, and you can run the `--describe` command to view the details as shown below:
   ![](https://main.qcloudimg.com/raw/d54eb823fe66da94364849e670f83fba.png)

   



### How do I set a reasonable number of consumers?

The relationship between consumer group and consumer is as follows:
- A consumer can subscribe to multiple topics at the same time.
- A topic can contain one or multiple partitions.
- A partition can be consumed by only one consumer.

Therefore, the maximum number of consumers in a consumer group is the total number of partitions in all topics.

Consumer refers to a consumer object from the perspective of code, and there can be multiple consumers on a server; for example, if multiple threads are initiated, a thread will contain a consumer as shown below:
```java
Properties props = new Properties();
props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrap);
KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
consumer.subscribe(Arrays.asList(topic));
while (true) {
            ConsumerRecords<String, String> records = consumer.poll(100);
}
```
You can configure the initial number of consumers based on the client resources and configure heap alarms for consumer groups. If messages are heaped, you can add more consumers. For more information on how to configure an alarm, please see [Configuring Alarm](https://intl.cloud.tencent.com/document/product/597/40976). The configuration page is as shown below:
![](https://main.qcloudimg.com/raw/d84892ff3a2cf3f37340e213454e3308.png)


### Why is a consumer group constantly in `PreparingRebalance` status?

Rebalance may occur in the following cases:
1. There is a new consumer joining the consumer group.
2. A running consumer stops running and leaves the consumer group. Common causes for this include consumer restart, consumer application crash, and heartbeat timeout of consumer process reporting. For more information, please see [Configuration Guide for Common Parameters in CKafka](https://intl.cloud.tencent.com/document/product/597/31588).
3. The number of partitions changes (partitions are added or removed).

Here, rebalance is inevitable in cases 1 and 3. In normal cases, rebalance can be completed in 30s. If there is a longer rebalance process, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

If the rebalance is caused by heartbeat timeout or excessive interval between two polls, you can adjust the following parameters:
```bash
# Consumer timeout period when the Kafka consumer grouping mechanism is used. If the broker does not receive the heartbeat of the consumer within this period, the consumer will be considered to have failed and the broker will initiate rebalance. Currently, this value must be configured in the broker between `group.min.session.timeout.ms=6000` and `group.max.session.timeout.ms=300000`
session.timeout.ms=10000

# Interval at which the consumer sends a heartbeat when the Kafka consumer grouping mechanism is used. This value must be smaller than `session.timeout.ms` and should generally be below one-third of it
heartbeat.interval.ms=3000

# Maximum interval allowed for calling `poll` again when the Kafka consumer grouping mechanism is used. If `poll` is not called again within this time period, the consumer will be considered to have failed, and the broker will initiate rebalance again to assign the partitions originally assigned to the consumer to other consumers
max.poll.interval.ms=300000
```

If a consumer subscribes to many topics, you can try reducing the topics subscribed to by the group.
