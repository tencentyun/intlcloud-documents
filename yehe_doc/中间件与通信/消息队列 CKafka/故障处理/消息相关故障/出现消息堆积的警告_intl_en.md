

## Issue Description

A warning is displayed for message heap.

## Possible Causes

- The client has not consumed messages.
- The client’s consumption speed is slow.

## Solutions

- **The client has not consumed messages**
  You can check the consumption speed of partitions to confirm whether there is consumption as shown below:
  ![](https://main.qcloudimg.com/raw/e48ab4cc7aa70d8e205f5cc220580341.jpg)

- **The client’s consumption speed is slow**
  For more information, see [Slow Message Consumption](https://intl.cloud.tencent.com/document/product/597/42147).

## Recommended Settings

Open-Source Kafka supports setting a timestamp field and type in a message. Currently, two timestamp types are supported: `CreateTime` and `LogAppendTime`.

- `CreateTime` indicates the local time on the client. As client time may vary from server time, check whether the entered time is correct. If it differs too much from the current Beijing time, the CKafka service will not be able to delete data promptly upon expiration based on the normal message retention period, which may cause exceptional message heap.
- `LogAppendTime` indicates the time when a message is produced to the CKafka service, which is the CKafka server time and thus recommended.



## Server Stress Testing

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

For more information, see [Conducting Production and Consumption Stress Testing on CKafka](https://intl.cloud.tencent.com/document/product/597/42257).
