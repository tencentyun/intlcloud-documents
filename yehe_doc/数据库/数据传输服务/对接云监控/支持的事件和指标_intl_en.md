## Overview
DTS can use Cloud Monitor to monitor events and metrics during data migration, sync, and subscription tasks and set alarming rules. Cloud Monitor will send notifications to you as soon as an event is triggered or a metric becomes exceptional, so you can take corresponding measures.  

> ?Currently, event and metric monitoring is supported only for data migration, sync, and subscription from a MySQL database to another.

## Supported Events
DTS supports default alarm configuration for some critical events, which means it will automatically monitor events when a task is started without having you to configure options and will notify you of triggered events.

| **Event Scenario** | **Event**     | **Alarmed by Default** | **Description**                                             |
| ------------ | ---------------- | ---------------- | ---------------------------------------------------- |
| Data migration     | Data migration task interruption | Yes         | The alarm will be triggered if a data migration task is interrupted or exceptional. |
| Data sync     | Data sync task interruption | Yes         | The alarm will be triggered if a data sync task is interrupted or exceptional. |
| Data subscription     | Data subscription task interruption | Yes         | The alarm will be triggered if a data subscription task is interrupted or exceptional. |

## Metrics Supported by Data Migration

> ?Currently, real-time monitoring metric data can be obtained only during incremental migration.

| **Metric**  | **Unit** | **Description**            |
| ------------------ | ------- | ---------------------------------- |
| RPS read from source database | Count/s | Number of rows of data in the source database read by DTS per second |
| RPS written to target database  | Count/s | Number of rows of data migrated to the target database by DTS per second |
| Data migration time lag | s    | Time difference between the target and source databases. <br>Calculation method: the current time of the target database minus the time recorded in the latest binlog event of the source database running on the target database. If the times of the source and target databases are out of sync, this value may be inaccurate. <br>Calculation of the data migration time lag depends on the incremental binlogs of the source database. Therefore, if there are no DDL or DML operations performed on the source database for a long time, the value of this metric will gradually increase and thus cannot reflect the actual migration time lag (if the value is `-1`, it indicates that the existing data has been migrated, but there is no refresh of the incremental data). In this case, you can run an SQL statement on the source database to refresh the metric so as to get the correct metric value. |
| Data migration data lag | MB/s | Data size difference between the source and target databases. <br>Calculation method: the file offset of the latest binlog event of the source database minus the file offset of the latest binlog event of the source database running in the target database. If the two offsets are in different binlog files, this value will be estimated.<br/>If there are no DDL or DML operations performed on the source database for a long time, the value of this metric will gradually increase and thus cannot reflect the actual migration data lag (if the value is `-1`, it indicates that the existing data has been migrated, but there is no refresh of the incremental data). |

## Metrics Supported by Data Sync

> ?Currently, real-time monitoring metric data can be obtained only during incremental sync.

| **Metric**  | **Unit** | **Description**            |
| ------------------ | ------- | ---------------------------------- |
| RPS read from source database | Count/s | Number of rows of data in the source database read by DTS per second |
| RPS written to target database  | Count/s | Number of rows of data migrated to the target database by DTS per second |
| Data sync time lag | s    | Time difference between the target and source databases. <br>Calculation method: the current time of the target database minus the time recorded in the latest binlog event of the source database running on the target database. If the times of the source and target databases are out of sync, this value may be inaccurate. <br>Calculation of the data sync time lag depends on the incremental binlogs of the source database. Therefore, if there are no DDL or DML operations performed on the source database for a long time, the value of this metric will gradually increase and thus cannot reflect the actual sync time lag (if the value is `-1`, it indicates that the existing data has been migrated, but there is no refresh of the incremental data). In this case, you can run an SQL statement on the source database to refresh the metric so as to get the correct metric value. |
| Data sync data lag | MB/s | Data size difference between the source and target databases. <br>Calculation method: the file offset of the latest binlog event of the source database minus the file offset of the latest binlog event of the source database running in the target database. If the two offsets are in different binlog files, this value will be estimated.<br/>If there are no DDL or DML operations on the source database for a long time, this metric will gradually increase and thus cannot reflect the actual sync data lag (if the value is `-1`, it indicates that the existing data has been synced, but there is no refresh of the incremental data). |

## Metrics Supported by Data Subscription (Kafka Edition)

| **Metric**  | **Unit** | **Description**            |
| --------------- | -------- | ------------------------------------------------------------ |
| Binlog parsing lag | Count    | Difference between the number of GTIDs in the binlog events already parsed by the data subscription service and the number of GTIDs in the latest binlog events generated by the source database. |
| Number of transactions parsed per second  | Count/s  | Number of transactions read and parsed from the source database binlog by DTS per second.                     |

## Metrics Supported by Data Subscription

| **Metric**  | **Unit** | **Description**            |
| ------------------ | -------- | ------------------------------------------------------------ |
| Data parsing GTID lag      | Count    | Difference between the number of GTIDs in the binlog being parsed by the subscription service and the number of GTIDs in the latest binlog generated by the source database. |
| SDK ack time lag       | s       | Every time the SDK consumes a message, it will return an ack message to the server. This metric is the time difference between the SDK message production and consumption, i.e., difference between the time point when the last response message from the SDK is generated in the SDK and the machine time on the subscription server. |
| Number of transactions per second         | Count/s  | Number of transactions processed by the consumer per second.                                     |
| Pending ack queue utilization   | %        | For messages consumed by the client, an ack message will be sent to the server, which will be added to the pending ack queue. This metric indicates the proportion of the messages pending ack by the server in the messages cached on the client. <br>If the pending ack queue is full, this metric value will be 100%, indicating that `AckAsComsumed` fails to be called for a message on the client due to a program exception. |
| Internal parsing queue utilization | %        | Before consuming messages, the client will parse them and place them in the internal parsing queue. This metric indicates the utilization of the parsing queue. |
| Message queue utilization     | %        | When the client is running, it downloads messages from the subscribed server and caches them in the message queue. This metric indicates the utilization of the message queue. |
