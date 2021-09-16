## Overview

This document describes how to use the single-producer single-consumer scheme to migrate data from a self-built Kafka cluster to a CKafka cluster.

## Prerequisites    

- You have already [purchased a CKafka instance](https://intl.cloud.tencent.com/document/product/597/41379).
- You have already [migrated the topic to CKafka](https://intl.cloud.tencent.com/document/product/597/41380).

## Directions

The prerequisite for guaranteeing message ordering is to strictly limit data consumption to only one consumer. Therefore, timing of the migration is vital.

The single-producer single-consumer scheme is simple, clear, and easy to implement; however, after the production is switched to the new cluster, before the old consumer is switched to the new cluster, there will be a certain amount of data heap in the new cluster.

The migration steps are as follows: ![](https://main.qcloudimg.com/raw/a24b388a3259dfe609e94ed14037c862.png)

1. Switch the production flow so that the producer produces data to the CKafka instance.
   Configure the accessed network of the CKafka instance as the IP in `broker-list` by copying the information in the **Network** column in the **Access Mode** section on the **Instance Details** page in the console, and change the `topicName` to the topic name in the CKafka instance.
```bash
 ./kafka-console-producer.sh --broker-list xxx.xxx.xxx.xxx:9092 --topic topicName
```

2. The original consumer does not need to be configured and can continue to consume the data in your self-built Kafka cluster until all data is consumed.

3. When the consumption by the original consumer is completed, switch to the new CKafka cluster for consumption through the following configuration (let only one consumer consume the data to guarantee message ordering). If you add a new consumer, you need to configure the accessed network of the CKafka instance as the IP in `--bootstrap-server`.
>?If the original consumer is a CVM instance, it can continue to consume the data.
>
```bash
./kafka-console-consumer.sh --bootstrap-server xxx.xxx.xxx.xxx:9092 --from-beginning --new-consumer --topic topicName --consumer.config ../config/consumer.properties
```

4. The consumer continues to consume data in the CKafka cluster after switch, and the migration is completed (if the original consumer is a CVM instance, it can continue to consume the data).

>!The above commands are test commands. In actual business operations, just modify the broker address configured for the corresponding application and then restart the application.
