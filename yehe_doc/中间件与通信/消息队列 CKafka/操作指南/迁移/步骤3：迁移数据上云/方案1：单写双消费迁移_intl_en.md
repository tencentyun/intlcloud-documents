## Overview

This document describes how to use the single-producer dual-consumer scheme to migrate data from a self-built Kafka cluster to a CKafka cluster.

## Prerequisites    

- You have already [purchased a CKafka instance](https://intl.cloud.tencent.com/document/product/597/41379).
- You have already [migrated the topic to CKafka](https://intl.cloud.tencent.com/document/product/597/41380).

## Directions

If your requirement for message ordering is not high, you can migrate the data while it is consumed by multiple consumers in parallel.

The single-producer dual-consumer scheme is simple, clear, and easy to implement, with no data heap for smooth transition; however, it requires adding a new consumer.

The migration steps are as follows:
![](https://main.qcloudimg.com/raw/7b41c8c1f3740a9b5b6ad45f6b369cc0.png)

1. Keep the old consumer intact, start a new consumer in CKafka, and configure the bootstrap-server of the new CKafka cluster for consumption.
    You need to configure the accessed network of the CKafka instance as the IP in `--bootstrap-server` by copying the information in the **Network** column in the **Access Mode** section on the **Instance Details** page in the console.
  ```bash
./kafka-console-consumer.sh --bootstrap-server xxx.xxx.xxx.xxx:9092 --from-beginning --new-consumer --topic topicName --consumer.config ../config/consumer.properties
  ```

2. Switch the production flow so that the producer produces data to the CKafka instance.
   Change the IP in the `broker-list` to the accessed network of the CKafka instance and `topicName` to the topic name in the CKafka instance:
```bash
 ./kafka-console-producer.sh --broker-list xxx.xxx.xxx.xxx:9092 --topic topicName
```

3. The original consumer does not need to be configured and can continue to consume the data in your self-built Kafka cluster. After such data is all consumed, the migration is completed.

>!The above commands are test commands. In actual business operations, just modify the broker address configured for the corresponding application and then restart the application.
