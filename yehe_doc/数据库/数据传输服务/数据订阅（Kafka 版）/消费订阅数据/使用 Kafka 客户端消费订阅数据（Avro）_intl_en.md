## Overview

In data subscription (Kafka Edition), you can consume the subscribed data through Kafka 0.11 or later available at [DOWNLOAD](http://kafka.apache.org/downloads). This document provides client consumption demos for Java, Go, and Python for you to quickly test the process of data consumption and understand the method of data parsing.

When configuring the subscription task, you can select different formats of subscribed data, including ProtoBuf, Avro, and JSON. ProtoBuf and Avro adopt the binary format with a higher consumption efficiency, while JSON adopts the easier-to-use lightweight text format. The reference demo varies by the selected data format.

This document provides a demo of the Avro format. The demo already contains the Avro protocol file, so you don't need to download it separately.

> ?Currently, data consumption over the Avro protocol is supported only for MySQL and TDSQL-C for MySQL.

## Notes

- **The demo only prints out the consumed data but does not contain the usage instructions of such data. You need to write your own data processing logic based on the demo.** You can also use Kafka clients in other languages to consume and parse data.
- Currently, data subscription to Kafka for consumption can be implemented over the Tencent Cloud private network but not the public network. In addition, the subscribed database instance and the data consumer must be in the same region.
- The Kafka built in DTS has a certain upper limit for processing individual messages. When a single row of data in the source database exceeds 10 MB, this row may be discarded.
- The delivery semantics of subscription to Kafka messages in DTS is to deliver a message at least once; therefore, the consumed data may be duplicated in special cases. For example, if the subscription task is restarted, the source binlog will be pulled before the interruption offset after the restart, resulting in repeated delivery of messages. Operations in the console such as modifying subscribed objects and restoring abnormal tasks may cause duplicate messages. If your business is sensitive to duplicate data, you need to add deduplication logic based on the business data in the consumption demo.


## Downloading a consumption demo
| Demo Language | TencentDB for MySQL and TDSQL-C for MySQL |
| ------------- | ------------------------------------------------------------ |
| Go            | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-avro-go.zip) |
| Java          | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-avro-java.zip) |
| Python 3       | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-avro-python.zip) |


## Instructions for the Java demo
Compilation environment: Maven or Gradle and JDK 8. You can choose a desired package management tool. The following takes Maven as an example.
Runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance). Install JRE 8.
Directions:
1. Create a data subscription task (new version).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download the Java demo and decompress it.
4. Access the decompressed directory. Maven model and pom.xml files are placed in the directory for your use as needed.
Package the project with Maven by running `mvn clean package`.
5. Run the demo.
After packaging the project with Maven, go to the target folder `target` and run `java -jar consumerDemo-avro-1.0-SNAPSHOT.jar --brokers xxx --topic xxx --group xxx --user xxx --password xxx --trans2sql=true`.
 - `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660).
 - `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535).
 - `trans2sql` indicates whether to enable conversion to SQL statement. In Java code, if this parameter is carried, the conversion will be enabled.
> ?If `trans2sql` is carried, `javax.xml.bind.DatatypeConverter.printHexBinary()` will be used to convert byte values to hex values. You should use JDK 1.8 or later to avoid incompatibility. If you don't need SQL conversion, comment this parameter out.
6. Observe consumption.
![](https://main.qcloudimg.com/raw/fffa3de2a6e38b3752512183e1ffe785.png)

## Instructions for the Go demo
Compiling environment: Go 1.12 or later, with the Go module environment configured.
Runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance).
Directions:
1. Create a data subscription task (new version).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download the Go demo and decompress it.
4. Access the decompressed directory and run `go build -o subscribe ./main/main.go` to generate the executable file `subscribe`.
5. Run `./subscribe --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=true`.
 - `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660).
 - `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535).
 - `trans2sql` indicates whether to enable conversion to SQL statement.
6. Observe consumption.
![](https://main.qcloudimg.com/raw/c94d9cfe2a62e903a6593e22ce2c60bf.png)

## Instructions for the Python 3 demo
Compilation and runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance). Install Python 3 and pip3 (for dependency package installation).
Use `pip3` to install the dependency package:
```
pip install flag
pip install kafka-python
pip install avro
```
Directions:
1. Create a data subscription task (new version).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download the Python 3 demo and decompress it.
4. Run `python main.py --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=1`.
 - `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660).
 - `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535).
 - `trans2sql` indicates whether to enable conversion to SQL statement.
5. Observe consumption.
![](https://main.qcloudimg.com/raw/6055041985904335b43d7df8f4e75561.png)

## [Key demo logic description](id:dgxljjj)
Files in the demo are as described below, with the Java demo as an example.
- `consumerDemo-avro-java\src\main\resources\avro-tools-1.8.2.jar` is a tool used to generate Avro protocol code.
- `consumerDemo-avro-java\src\main\java\com\tencent\subscribe\avro` is the directory where the Avro tool generates code.
- `consumerDemo-avro-java\src\main\resources\Record.avsc` is the protocol definition file.

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
| readerTimestamp          | The time for the backend to processing the current data record in milliseconds.                       |
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

