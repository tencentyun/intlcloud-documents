You can choose the most appropriate migration method based on your actual business scenario to migrate your business data to the cloud by following the steps below. This guide is mainly for data migration from CVM to CKafka, which can be done over the private network. If access to data stream over the public network is required, you need to activate public IP access for your CKafka instance first.

## Migrating Data to CKafka with Guaranteed Message Ordering

The premise of guaranteeing message ordering is to strictly limit the data consumption to only one single consumer; therefore, timing of the migration is vital. The migration steps are as follows:

![Alt text](https://main.qcloudimg.com/raw/85c0ee0a869df5fbf294bdfc972f2084.png)

Detailed directions:

1. Create a CKafka instance and create a corresponding topic:
![Alt text](https://main.qcloudimg.com/raw/feb55a130b2e14b3942b34e41f4f8a17.png)

2. Switch the production flow so that the producer produces the data to the CKafka instance.
 Change the IP and topicName in the broker-list to the VIP of the CKafka instance and the topic name in the CKafka instance, respectively:
```
 ./kafka-console-producer.sh --broker-list xxx.xxx.xxx.xxx:9092 --topic topicName
```

3. The original consumer does not need to be configured otherwise and can continue to consume the data in your self-built Kafka cluster. After the consumption is completed, make new consumers consume the data in the CKafka cluster through the following configuration. (To guarantee the message ordering, let only one consumer consume the data.)

 To add a new consumer, you need to configure the IP in --bootstrap-server to the VIP of the CKafka instance:
```
./kafka-console-consumer.sh --bootstrap-server xxx.xxx.xxx.xxx:9092 --from-beginning --new-consumer --topic topicName --consumer.config ../config/consumer.properties
```

4. The new consumer continuously consumes the data in the CKafka cluster and the migration is completed (if the original consumer is a CVM instance, it can continue to consume the data).

>**Note:**
> The above commands are test commands. In actual business operations, you only need to modify the broker address configured for the corresponding application and then restart the application.

## Migrating Data to CKafka Without Guaranteed Message Ordering

In case that data ordering requirement is not high, it is possible to migrate the data while it is consumed by multiple consumers in parallel. The migration steps are as follows:

![Alt text](https://main.qcloudimg.com/raw/02342dc426a1ec0f5378071721923c7a.png)

Detailed directions:

1. Create a CKafka instance and create a corresponding topic:
![Alt text](https://main.qcloudimg.com/raw/feb55a130b2e14b3942b34e41f4f8a17.png)

2. Switch the production flow so that the producer produces the data to the CKafka instance.

 Change the IP and topicName in the broker-list to the VIP of the CKafka instance and the topic name in the CKafka instance, respectively:
```
 ./kafka-console-producer.sh --broker-list xxx.xxx.xxx.xxx:9092 --topic topicName
```

3. The original consumer does not need to be configured otherwise and can continue to consume the data in your self-built Kafka cluster. Meanwhile, new consumers can be added to consume the data in the CKafka cluster. After the data in the original self-built cluster is all consumed, the migration is completed. (This is suitable for scenarios where message ordering is not required.)

 Configure the IP in --bootstrap-server to the VIP of the CKafka instance:
```
./kafka-console-consumer.sh --bootstrap-server xxx.xxx.xxx.xxx:9092 --from-beginning --new-consumer --topic topicName --consumer.config ../config/consumer.properties
```

>**Note:**
> The above commands are test commands. In actual business operations, you only need to modify the broker address configured for the corresponding application and then restart the application.
