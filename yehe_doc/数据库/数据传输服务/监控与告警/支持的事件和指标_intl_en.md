## Overview
DTS can use CM to monitor events and metrics during data migration, sync, and subscription tasks and set alarm rules. CM will send notifications to you as soon as an event is triggered or a metric becomes abnormal, so you can take corresponding measures.  

> ?
> - Currently, event alarming is supported for the migration, sync, and subscription links of MySQL, MariaDB, Percona, and TDSQL-C for MySQL.
> - Currently, metric alarming is supported for the migration, sync, and subscription links of MySQL, MariaDB, Percona, TDSQL-C for MySQL, and TDSQL for MySQL.

## Supported events
| **Event**   | **Description**                                                     |
| -------------------------------- | ------------------------------------------------------------ |
| Data migration task interrupted | This alarm will be triggered when a data migration task is interrupted abnormally (excluding manual interruptions). |
| Data synchronization task interrupted | This alarm will be triggered when a data sync task is interrupted abnormally (excluding manual interruptions). |
| Data subscription task interrupted | This alarm will be triggered when a data subscription task is interrupted abnormally (excluding manual interruptions). |
| Cloud API actions (CloudAudit) | This alarm will be triggered when a cloud API action is abnormally interrupted. |
| Console operations (CloudAudit) | This alarm will be triggered when a console operation is abnormally interrupted. |
| Mini program operations (CloudAudit) | This alarm will be triggered when a mini program operation is abnormally interrupted. |

## Metrics supported by data migration

> ?Currently, real-time monitoring metric data can be obtained only during incremental migration.

| **Metric**  | **Unit** | **Description**            |
| ------------------ | ------- | ---------------------------------- |
| RPS read from source instance | Count/s | The number of rows of data in the source instance read by DTS per second. |
| RPS written to target instance | Count/s | The number of rows of data migrated to the target instance by DTS per second. |
| Data migration time lag | s    | The time difference between the source and target instances. <br>Calculation method: The current time of the source instance minus the time recorded in the latest binlog event of the source database running in the target instance. <br/>Calculation of the data migration time lag depends on the incremental binlogs of the source database. Therefore, if there are no DDL or DML operations performed on the source database for a long time, the value of this metric will gradually increase and thus cannot reflect the actual migration time lag (if the value is `-1`, it indicates that the existing data has been migrated, but there is no refresh of the incremental data). In this case, you can run a SQL statement on the source database to refresh the metric so as to get the correct metric value. |
| Data migration data lag | MBytes | The data size difference between the source and target instances. <br>Calculation method: The file offset of the latest binlog event of the source instance minus the file offset of the latest binlog event of the source instance running in the target instance. If the two offsets are in different binlog files, this value will be estimated.<br/>If there are no DDL or DML operations performed on the source database for a long time, the value of this metric will gradually increase and thus cannot reflect the actual migration data lag (if the value is `-1`, it indicates that the existing data has been migrated, but there is no refresh of the incremental data). |

## Metrics supported by data sync

> ?Currently, real-time monitoring metric data can be obtained only during incremental sync.

| **Metric**  | **Unit** | **Description**            |
| ------------------ | ------- | ---------------------------------- |
| RPS read from source instance | Count/s | The number of rows of data in the source instance read by DTS per second. |
| RPS written to target instance | Count/s | The number of rows of data migrated to the target instance by DTS per second. |
| Data sync time lag | s    | The time difference between the source and target instances. <br>Calculation method: The current time of the source instance minus the time recorded in the latest binlog event of the source database running in the target instance. <br/>Calculation of the data sync time lag depends on the incremental binlogs of the source database. Therefore, if there are no DDL or DML operations performed on the source database for a long time, the value of this metric will gradually increase and thus cannot reflect the actual sync time lag (if the value is `-1`, it indicates that the existing data has been migrated, but there is no refresh of the incremental data). In this case, you can run a SQL statement on the source database to refresh the metric so as to get the correct metric value. |
| Data sync data lag | MBytes | The data size difference between the source and target instances. <br>Calculation method: The file offset of the latest binlog event of the source instance minus the file offset of the latest binlog event of the source instance running in the target instance. If the two offsets are in different binlog files, this value will be estimated.<br/>If there are no DDL or DML operations performed on the source database for a long time, the value of this metric will gradually increase and thus cannot reflect the actual sync data lag (if the value is `-1`, it indicates that the existing data has been synced, but there is no refresh of the incremental data). |

## Metrics supported by data subscription (Kafka Edition)

| **Metric**  | **Unit** | **Description**            |
| ------------------------- | -------- | ------------------------------------------------------------ |
| Binlog parsing lag | Count    | The difference between the number of GTIDs in the binlog events already parsed by the data subscription service and the number of GTIDs in the latest binlog events generated by the source database. <br>If there are no DDL or DML operations performed on the source database for a long time, the value of this metric will gradually increase and thus cannot reflect the actual subscription data lag. If the value is `-1`, it indicates that there is no refresh of the data. <dx-alert infotype="explain" title="Note">This metric is for MySQL, MariaDB, Perocna, TDSQL for MySQL, and TDSQL-C for MySQL only.</dx-alert> |
| LSN gap between subscription service and source database | MBytes   | The LSN gap between the parsed log offset of the data subscription service and the latest log offset generated by the source database. <dx-alert infotype="explain" title="Note">This metric is for TDSQL for PostgreSQL only.</dx-alert> |
| Transactions parsed per second  | Count/s  | The number of transactions read and parsed from the source database binlog by DTS per second.                     |

## Metrics supported by data subscription

| **Metric**  | **Unit** | **Description**            |
| ------------------ | -------- | ------------------------------------------------------------ |
| Data parsing GTID lag      | Count    | The difference between the number of GTIDs in the binlog being parsed by the subscription service and the number of GTIDs in the latest binlog generated by the source database. |
| SDK ack time lag       | s       | Every time the SDK consumes a message, it will return an ack message to the server. This metric is the time difference between the SDK message production and consumption, i.e., difference between the time point when the last response message from the SDK is generated in the SDK and the machine time on the subscription server. |
| Transactions per second         | Count/s  | The number of transactions processed by the consumer per second.                                     |
| Pending acknowledgment queue utilization   | %        | For messages consumed by the client, an acknowledgment message will be sent to the server, which will be added to the pending acknowledgment queue. This metric indicates the proportion of the messages pending acknowledgment by the server in the messages cached on the client. <br>If the pending acknowledgment queue is full, this metric value will be 100%, indicating that `AckAsComsumed` fails to be called for a message on the client due to a program exception. |
| Internal parsing queue utilization | %        | Before consuming messages, the client will parse them and place them in the internal parsing queue. This metric indicates the utilization of the parsing queue. |
| Message queue utilization     | %        | When the client is running, it downloads messages from the subscribed server and caches them in the message queue. This metric indicates the utilization of the message queue. |

