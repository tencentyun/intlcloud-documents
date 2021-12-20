## Overview

This document describes how to use MirrorMaker to migrate data from a self-built Kafka cluster to a CKafka cluster.

Kafka MirrorMaker can back up data in a self-built Kafka cluster to a CKafka cluster in the following way:
MirrorMaker can use a consumer to consume messages in the self-built Kafka cluster and then use a producer to transfer the message data to the CKafka cluster. After this, you can transfer the production and consumption configurations of the client to the accessed network of the CKafka cluster so as to complete data migration.

## Prerequisites

- You have already [purchased a CKafka instance](https://intl.cloud.tencent.com/document/product/597/41379).
- You have already [migrated the topic to CKafka](https://intl.cloud.tencent.com/document/product/597/41380).

## Directions

1. [Download MirrorMaker](http://kafka.apache.org/downloads) and decompress it on the local server.
>?This document takes [kafka_2.11-1.1.1.tgz](https://archive.apache.org/dist/kafka/1.1.1/kafka_2.11-1.1.1.tgz) as an example:

2. Configure the `consumer.properties` file.

   ```properties
   # list of brokers used for bootstrapping knowledge about the rest of the cluster
   # format: host1:port1,host2:port2 ...
   bootstrap.servers=localhost:9092
   
   # consumer group id
   group.id=test-consumer-group
   
   partition.assignment.strategy=org.apache.kafka.clients.consumer.RoundRobinAssignor
   # What to do when there is no initial offset in Kafka or if the current
   # offset does not exist any more on the server: latest, earliest, none
   #auto.offset.reset=
   ```


   | Parameter                          | Description                                                         |
   | ----------------------------- | ------------------------------------------------------------ |
   | bootstrap.servers             | List of broker access points of the self-built cluster.                                 |
   | group.id                      | ID of the consumer group used during data migration. It must be different from the names of existing consumer groups in the self-built cluster. |
   | partition.assignment.strategy | Partition assignment policy, such as `partition.assignment.strategy=org.apache.kafka.clients.consumer.RoundRobinAssignor` |

3. Configure the `producer.properties` file.

   ```properties
   # list of brokers used for bootstrapping knowledge about the rest of the cluster
   # format: host1:port1,host2:port2 ...
   bootstrap.servers=localhost:9092
   
   # specify the compression codec for all data generated: none, gzip, snappy, lz4
   compression.type=none
   ```


   | Parameter              | Description                                                         |
   | ----------------- | ------------------------------------------------------------ |
   | bootstrap.servers | Accessed network of the CKafka instance, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![img](https://main.qcloudimg.com/raw/6b12eca18662d26a334d55b743c825ef.png) |
   | compression.type  | Data compression type. CKafka does not support the Gzip compression format.                     |

4. Start MirrorMaker in the `.bin` directory to start migration.

   ```bash
   sh bin/kafka-mirror-maker.sh --consumer.config config/consumer.properties --producer.config config/producer.properties --whitelist topicName
   ```

    <dx-alert infotype="explain" title="">
   `whitelist` is a regular expression, and topics whose names hit it will be migrated.
   </dx-alert>



5. Run `kafka-consumer-groups.sh` in the `bin` directory to view the consumption progress of the self-built cluster.

   ```bash
   bin/kafka-consumer-groups.sh --new-consumer --describe --bootstrap-server self-built cluster access point --group test-consumer-group
   ```

    <dx-alert infotype="explain" title="">
   `group` is the ID of the consumer group used during data migration.
   </dx-alert>

   ![](https://main.qcloudimg.com/raw/7840067dd702a22ebfd2ecb9250dc0d7.png)

## Subsequent Operations

After data migration, transfer the production and consumption configurations of the client to the access point of the CKafka cluster.
