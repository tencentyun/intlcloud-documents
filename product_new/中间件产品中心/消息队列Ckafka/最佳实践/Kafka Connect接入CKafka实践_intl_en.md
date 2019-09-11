Kafka Connect currently supports two execution modes: standalone and distributed.


## Starting Connect in Standalone Mode
Start Connect in standalone mode by running the following command:
```
bin/connect-standalone.sh config/connect-standalone.properties connector1.properties [connector2.properties ...]
```
Accessing CKafka is basically the same as accessing the open-source Kafka, except that you need to change the bootstrap.servers to the IP assigned when the instance is applied for.

## Starting Connect in Distributed Mode
Start Connect in distributed mode by running the following command:
```
bin/connect-distributed.sh config/connect-distributed.properties
```
In this mode, Kafka Connect stores the offsets, configs, and task status information in Kafka topics which are configured in the following fields in connect-distributed:
```
config.storage.topic
offset.storage.topic
status.storage.topic
```
These three topics need to be created manually to ensure that the attributes created meet the requirements of Connect.

- It should be ensured that config.storage.topic has only one partition and multiple replicas and is in compact mode.
- offset.storage.topic should have multiple partitions and multiple replicas and be in compact mode.
- status.storage.topic should have multiple partitions and multiple replicas and be in compact mode.

Configure bootstrap.servers to the IP assigned when the instance is applied for.

Configure group.id to identify the Connect cluster which should be distinguished from the consumer group.

