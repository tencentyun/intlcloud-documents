### How do I choose an appropriate number of CKafka replicas?
To ensure data reliability, you are recommended to choose two or three replicas for data storage when creating a topic. Currently, CKafka has banned the creation of single-replica topics. If you have a single-replica topic in your account, please migrate it as follows:
1. Create a topic, select the same partition parameter, and select "dual-replica";
2. Produce messages in the new topic while the existing single-replica topic continues to be consumed;
3. Modify the consumer configuration after consumption is completed to subscribe to the new topic for consumption.

### How do I fix production/consumption errors when a new client is connected to CKafka?
- Check whether telnet works. It might be a network issue. Check if Kafka and the producer are in the same network.
- Check whether the accessed vip-port is correctly configured.
- Check whether the topic allowlist is enabled. If yes, you need to configure the correct IP for access.

### The CKafka message retention period is configured to 1 minute. Will the heaped messages be deleted immediately after 1 minute?
Not necessarily. Message deletion is related to not only the retention period configuration but also the data size of produced messages.
CKafka's smallest unit for heaped message deletion is partition-level file segment. The current file segment size is 1 GB. If the message heap does not reach the size of one file segment, the messages will not be deleted. If there are 10 partitions, and their total size does not reach 10 GB within 1 minute, then files will not be rolled, and messages will not be deleted.

### Does CKafka support automatic topic creation (auto.create.topic)?
Currently, CKafka supports the open-source API for automatic topic creation. On the [instance list page](https://console.cloud.tencent.com/ckafka/index?rid=1), click an instance ID to enter the instance details page. On the **Basic Info** tab there, view or edit the configuration information, message retention period, and automatic topic creation of the instance.

### What should I do if a lot of CKafka messages heap up?
CKafka uses exactly the same mechanism and principle as open-source Kafka. You can troubleshoot the problem in the following steps:
1. Determine how many consumers in your business are consuming messages.
2. If the consumers' consumption capabilities are poor, simply add more consumers.

### How does CKafka throttle traffic?
To ensure stability of the service, CKafka implement network traffic control strategies on both inputting and outputting messages.
- Throttling occurs when the total traffic of the user’s all replicas exceeds the purchased peak traffic.
- When the producer side is throttled, CKafka will extend the response time of a TCP connection. The delay period depends on how much the instantaneous traffic exceeds the limit. It is similar to the principle of road traffic control. The more traffic flow, the higher the delay value from the delay algorithm, up to 5 minutes.
- When the consumer side is throttled, CKafka will reduce the size of each `fetch.request.max.bytes` request to control the traffic.

### How does throttling affect the production and consumption of messages?
Throttling only affects the message sending and receiving rate but not the content of messages.

### How do I determine whether CKafka has been throttled?
1. In the instance list, you can see the health status of each cluster. If it’s “Warning”, you can hover your mouse over it to view the detailed data. The data displays your peak traffic and the throttling times, by which you can determine whether this instance has been throttled.
2. You can click the **Monitor** tab to view the max traffic value. If **the value of max traffic multiplied by replica quantity is greater than that of the purchased peak bandwidth**, you can determine that at least one throttling has occurred.
