### What should I do if a lot of messages heap up?

#### Error description

An alarm is displayed for message heap.

#### Possible causes

The client doesn't consume messages or consumes messages slowly.

#### Solution

- No consumption on the client

  You can check the consumption speed of partitions to confirm whether there is consumption as shown below:

  ![](https://main.qcloudimg.com/raw/e48ab4cc7aa70d8e205f5cc220580341.jpg)

- Slow consumption on the client

  Please see [Slow Message Consumption](https://cloud.tencent.com/document/product/597/60501).

#### Recommended settings

Open-Source Kafka supports setting a timestamp field and type in a message. Currently, two timestamp types are supported: `CreateTime` and `LogAppendTime`.

- `CreateTime` indicates the local time on the client. As client time may vary from server time, please check whether the entered time is correct. If it differs too much from the current Beijing time, the CKafka service will not be able to expire and delete data promptly based on the normal message retention period, which may cause exceptional message heap.
- `LogAppendTime` indicates the time when a message is produced to the CKafka service, which is the CKafka server time and thus recommended.



#### Server stress testing

If you have questions about the server performance, you can run the following stress test commands to check whether there is a problem on the server:

- Sample command for production testing:
```
bin/kafka-producer-perf-test.sh   
--topic test 
--num-records 123 
--record-size 1000  
--producer-props bootstrap.servers= ckafka vip : port 
--throughput 20000   
```

- Sample command for consumption testing:
```
bin/kafka-consumer-perf-test.sh   
--topic test 
--new-consumer  
--fetch-size 10000 
--messages 1000  
--broker-list bootstrap.servers=ckafka vip : port
```

For more information, please see [Conducting Production and Consumption Stress Testing on CKafka](https://cloud.tencent.com/document/product/597/19527).
