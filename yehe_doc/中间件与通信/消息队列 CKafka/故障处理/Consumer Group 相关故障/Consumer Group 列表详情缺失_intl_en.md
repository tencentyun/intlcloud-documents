
## Issue Description

The consumer group list in the CKafka Console contains consumer group name, but no consumption details are displayed on the details page; for example, the consumer group CR has no details displayed in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/30ca45b4a1b9850bc86c89ccda38c60a.png)

## Possible Causes

There are two data consumption modes in Kafka: consumer group mode and custom partition consumption mode.

- When consumption is performed in consumer group mode, the client will coordinate consumption through the consumption coordinator, and after data consumption is completed, it will send an offset storage request to the server, which will store information such as the consumed topic, partition progress, and client.
- When consumption is performed in custom partition consumption mode, the client will not automatically submit an offset storage request to the server. In this case, the server will not be able to see information related to consumption.
- After an ACL is set for a topic, you may not be able to view the consumer group details on some instances. In this case, check whether there are any ACLs, and if so, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.


## Solutions

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
