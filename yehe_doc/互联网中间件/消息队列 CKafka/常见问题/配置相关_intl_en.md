### How do I choose an appropriate number of CKafka replicas?
To ensure data reliability, you are recommended to choose two or three replicas for data storage when creating a topic. Currently, CKafka has banned the creation of single-replica topics. If you have a single-replica topic in your account, please migrate it as follows:
1. Create a topic, select the same partition parameter, and select "dual-replica";
2. Produce messages in the new topic while the existing single-replica topic continues to be consumed;
3. Modify the consumer configuration after consumption is completed to subscribe to the new topic for consumption.

### How do I fix production/consumption errors when a new client is connected to CKafka?
- Check whether telnet works. It might be a network issue. Check whether the CKafka instance and the producer are in the same network.
- Check whether the accessed VIP-port is correctly configured.
- Check whether the whitelist is enabled for the topic, and if yes, you need to configure the correct IP for access.

### The CKafka message retention period is configured to 1 minute. Will the heaped messages be deleted immediately after 1 minute?
Not necessarily. Message deletion is related to not only the retention period configuration but also the data size of produced messages.
CKafka's smallest unit for heaped message deletion is partition-level file shard. The current file shard size is 1 GB. If the message heap does not reach the size of one file shard, the messages will not be deleted. If there are 10 partitions, and their total size does not reach 10 GB within 1 minute, then files will not be rolled, and messages will not be deleted.

### Does CKafka support automatic topic creation (auto.create.topic)?
CKafka has not opened up the API for automatic topic creation yet. You are recommended to create topics through the standard [CreateTopic](https://intl.cloud.tencent.com/document/product/597/35347) API.
>
- Topics automatically created through the [CreateTopic](https://intl.cloud.tencent.com/document/product/597/35347) API will also take up the quotas of topics and partitions in your instance. Please pay attention to the quota restrictions.
- Topics automatically created in the instance will inherit the values of partition quantity and replica quantity you configured.
- In order to prevent accidental creation of too many exceptional topics, this API has an upper limit configured.

### What should I do if a lot of CKafka messages heap up?
CKafka uses exactly the same mechanism and principle as open-source Kafka. You can troubleshoot the problem in the following steps:
1. Determine how many consumers in your business are consuming messages;
2. If the consumers' consumption capabilities are poor, simply add more consumers;
3. If the number of consumers has reached the upper limit (≥ your number of partitions), you are recommended to increase the number of topic partitions by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CKafka&step=1) for application.
