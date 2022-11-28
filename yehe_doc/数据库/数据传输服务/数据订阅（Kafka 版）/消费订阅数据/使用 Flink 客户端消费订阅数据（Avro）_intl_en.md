## Overview

In data subscription (Kafka edition), subscribed data in Avro format can be consumed by using a Flink client (only the DataStream API type). This document provides a demo for data consumption with flink-dts-connector.

> ?Currently, data consumption over the Avro protocol is supported only for TencentDB for MySQL and TDSQL-C for MySQL.

## Prerequisites

1. You have created a data consumption task.
2. You have created a consumer group as instructed in [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. You have installed [Flink](https://flink.apache.org/downloads.html), and it can execute tasks normally.

## Notes

- **The demo only prints out the consumed data but does not contain the usage instructions of such data. You need to write your own data processing logic based on the demo.** You can also use Kafka clients in other languages to consume and parse data.
- Currently, data subscription to Kafka for consumption can be implemented over the Tencent Cloud private network but not the public network. In addition, the subscribed database instance and the data consumer must be in the same region.
- The Kafka built in DTS has a certain upper limit for processing individual messages. When a single row of data in the source database exceeds 10 MB, this row may be discarded.
- The delivery semantics of subscription to Kafka messages in DTS is to deliver a message at least once; therefore, the consumed data may be duplicated in special cases. For example, if the subscription task is restarted, the source binlog will be pulled before the interruption offset after the restart, resulting in repeated delivery of messages. Operations in the console such as modifying subscribed objects and restoring abnormal tasks may cause duplicate messages. If your business is sensitive to duplicate data, you need to add deduplication logic based on the business data in the consumption demo.

## Downloading a consumption demo

| Demo Language | TencentDB for MySQL and TDSQL-C for MySQL |
| ------------- | ------------------------------------------------------------ |
| Java | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-avro-flink.zip) |


## Instructions for the Java Flink demo
Compilation environment: Maven or Gradle and JDK 8. You can choose a desired package management tool. The following takes Maven as an example.
Runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance). Install JRE 8.
Directions:

1. Download the Java Flink demo and decompress it.
2. Access the decompressed directory. Maven model and pom.xml files are placed in the directory for your use as needed. 
`java -jar avro-tools-1.8.2.jar compile -string schema Record.avsc`: Code generation path.    
3. Modify the Flink version in the `pom.xml` file. The version in the following code must be the same as the Flink version you use.   
```
<dependency>
             <groupId>org.apache.flink</groupId>
             <artifactId>flink-connector-kafka_${scala.binary.version}</artifactId>
             <version>1.13.6</version>
</dependency>
<dependency>
             <groupId>org.apache.flink</groupId>
             <artifactId>flink-streaming-java_${scala.binary.version}</artifactId>
             <version>1.13.6</version>
             <scope>provided</scope>
</dependency>
<dependency>
             <groupId>org.apache.flink</groupId>
             <artifactId>flink-avro</artifactId>
             <version>1.13.6</version>
</dependency>
```
4. Go to the directory where the pom file is located and package it with Maven or IEDA
   Package with Maven by running `mvn clean package`.
5. For scenarios where the Flink client type is DataStream API, use Flink client commands to submit the task and start consumption.
`./bin/flink run consumerDemo-avro-flink-1.0-SNAPSHOT.jar --brokers xxx --topic xxx --group xxx --user xxx --password xxx —trans2sql`.
 - `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660).
 - `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535).
 - `trans2sql` indicates whether to enable conversion to SQL statement. In Java code, if this parameter is carried, the conversion will be enabled.
6. Observe consumption.
   View running tasks.
   ![](https://qcloudimg.tencent-cloud.cn/raw/dfcd7f2b7170394bd821847104f9ab00.png)   
   View task details.
   ![](https://qcloudimg.tencent-cloud.cn/raw/030783f22dc4997310fae8a18e7d6ebe.png)

## [Key demo logic description](id:dgxljjj)
Files in the demo are as described below:
- `consumerDemo-avro-flink\src\main\resources\avro-tools-1.8.2.jar`: The tool used to generate Avro protocol code.
- `consumerDemo-avro-flink\src\main\java\com\tencent\subscribe\avro`: The directory where the Avro tool generates code.
- `consumerDemo-avro-flink\src\main\resources\Record.avsc`: The protocol definition file.

14 structures (called schemas in Avro) are defined in `Record.avsc`. The main data structure is record, which is used to represent a data record in binlog. The record structure is as follows. Other data structures can be viewed in `Record.avsc`.
```
 {
    "namespace": "com.tencent.subscribe.avro",    // The last schema in `Record.avsc`, with `name` displayed as `Record`.
    "type": "record",    
    "name": "Record",     // `name` is displayed as `Record`, indicating the format of the data consumed from Kafka.
    "fields": [
      {
        "name": "id",     // `id` indicates a globally incremental ID. More record values are explained as follows:
        "type": "long",
        "doc": "unique id of this record in the whole stream"
      },
      {
        "name": "version",  // `version` indicates the protocol version.
        "type": "int",
        "doc": "protocol version"  
      },
      {
        "name": "messageType",   // Message type
        "aliases": [
          "operation"
        ],
        "type": {
          "namespace": "com.tencent.subscribe.avro",
          "name": "MessageType",
          "type": "enum",
          "symbols": [
            "INSERT",
            "UPDATE",
            "DELETE",
            "DDL",
            "BEGIN",
            "COMMIT",
            "HEARTBEAT",
            "CHECKPOINT",
            "ROLLBACK"
          ]
        }
      },  
      {
       ……
      },     
 }    
```

Fields in a record are as explained below:

| Field in Record | Description |
| ------------------------ | ------------------------------------------------------------ |
| id                       | The globally incremental ID.                                                 |
| version                  | The protocol version.                                                   |
| messageType              | The message type.                                                  |
| fileName                 | The binlog filename.                                              |
| position                 | The binlog offset.                                             |
| safePosition             | The binlog offset where the transaction started.                                     |
| timestamp                | The timestamp in the binlog.                                         |
| gtid                     | The transaction GTID.                                                  |
| transactionId            | The transaction ID.                                                    |
| serverId                 | The source database's `serverId`.                                              |
| threadId                 | The source database's thread ID.                                                |
| sourceType               | The source database type.                                           |
| sourceVersion            | The source database version, which is equivalent to `select version();`.                      |
| schemaName               | The database name.                                                       |
| tableName                | The table name.                                                     |
| objectName | The value of database name.table name. |
| columns                  | The column metadata.                                                   |
| oldColumns               | The column value before DML.                                               |
| newColumns               | The column value after DML.                                               |
| sql                      | The SQL statement.                                                   |
| executionTime            | The DDL execution duration.                                                |
| heartbeatTimestamp       | The timestamp of the heartbeat message, which is valid only in the heartbeat event.                  |
| syncedGtid               | The collection of parsed GTIDs.                                           |
| fakeGtid                 | Whether the current GTID is forged.                                        |
| pkNames                  | The primary key field. Only DML statements may have this value.                                  |
| readerTimestamp          | The time for the backend to process the current data record in milliseconds.                       |
| tags                     | Some additional fields.                                             |
| tags.lowerCaseTableNames | The case sensitivity of table names.                                             |
| total                    | The total number of message segments if the message is segmented. This field is invalid on the current version (version=1) and is reserved for extension.  |
| index                    | The total number of message segments if the message is segmented. This field is invalid on the current version (version=1) and is reserved for extension.  |

The field describing column attributes in a record is `Field`, including the following four attributes:

- name: The column name.
- dataTypeNumber: The type of the data recorded in the binlog. For values, see [COM_QUERY Response](https://dev.mysql.com/doc/internals/en/com-query-response.html).
- isKey: Whether the current key is the primary key.
- originalType: The type defined in DDL.

## Database field mappings

The following lists the mappings between database (such as MySQL) field types and data types defined in the Avro protocol. 

| Type in MySQL | Corresponding Type in Avro |
| ------------------------ | ------------------------------------------------------ |
| MYSQL_TYPE_NULL          | EmptyObject                                            |
| MYSQL_TYPE_INT8          | Integer                                                |
| MYSQL_TYPE_INT16         | Integer                                                |
| MYSQL_TYPE_INT24         | Integer                                                |
| MYSQL_TYPE_INT32         | Integer                                                |
| MYSQL_TYPE_INT64         | Integer                                                |
| MYSQL_TYPE_BIT           | Integer                                                |
| MYSQL_TYPE_YEAR          | DateTime                                               |
| MYSQL_TYPE_FLOAT         | Float                                                  |
| MYSQL_TYPE_DOUBLE        | Float                                                  |
| MYSQL_TYPE_VARCHAR       | Character                                              |
| MYSQL_TYPE_STRING        | Character. If the original type is binary, this type will correspond to BinaryObject.    |
| MYSQL_TYPE_VAR_STRING    | Character. If the original type is varbinary, this type will correspond to BinaryObject. |
| MYSQL_TYPE_TIMESTAMP     | Timestamp                                              |
| MYSQL_TYPE_DATE          | DateTime                                               |
| MYSQL_TYPE_TIME          | DateTime                                               |
| MYSQL_TYPE_DATETIME      | DateTime                                               |
| MYSQL_TYPE_TIMESTAMP_NEW | Timestamp                                              |
| MYSQL_TYPE_DATE_NEW      | DateTime                                               |
| MYSQL_TYPE_TIME_NEW      | DateTime                                               |
| MYSQL_TYPE_DATETIME_NEW  | DateTime                                               |
| MYSQL_TYPE_ENUM          | TextObject                                             |
| MYSQL_TYPE_SET           | TextObject                                             |
| MYSQL_TYPE_DECIMAL       | Decimal                                                |
| MYSQL_TYPE_DECIMAL_NEW   | Decimal                                                |
| MYSQL_TYPE_JSON          | TextObject                                             |
| MYSQL_TYPE_BLOB          | BinaryObject                                           |
| MYSQL_TYPE_TINY_BLOB     | BinaryObject                                           |
| MYSQL_TYPE_MEDIUM_BLOB   | BinaryObject                                           |
| MYSQL_TYPE_LONG_BLOB     | BinaryObject                                           |
| MYSQL_TYPE_GEOMETRY      | BinaryObject                                           |

