
### How do I set a reasonable number of consumers?

The relationship between consumer group and consumer is as follows:
- A consumer can subscribe to multiple topics at the same time.
- A topic can contain one or multiple partitions.
- A partition can be consumed only by one consumer at a time.

Therefore, the maximum number of consumers in a consumer group is the total number of partitions in all topics.

Consumer refers to a consumer object in programming. There can be multiple consumers on a server. This is because a thread contains a consumer, and if multiple threads are initiated, there will be multiple consumers as shown below:
```java
Properties props = new Properties();
props.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, bootstrap);
KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
consumer.subscribe(Arrays.asList(topic));
while (true) {
            ConsumerRecords<String, String> records = consumer.poll(100);
}
```
You can configure the initial number of consumers based on the client resources and configure heap alarms for consumer groups. If messages are heaped, you can add more consumers. For more information on how to configure an alarm, see [Configuring Alarm](https://intl.cloud.tencent.com/document/product/597/40976). The configuration page is as shown below:
![](https://main.qcloudimg.com/raw/8c10d954b79dc191a9ce173e3063f605.png)


