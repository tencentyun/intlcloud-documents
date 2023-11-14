## Overview

In data subscription (Kafka Edition), you can consume the subscribed data through Kafka 0.11 or later available at [DOWNLOAD](http://kafka.apache.org/downloads). This document provides client consumption demos for Java, Go, and Python for you to quickly test the process of data consumption and understand the method of data parsing.

When configuring the subscription task, you can select different formats of subscribed data, including Protobuf, Avro, and JSON. Protobuf and Avro adopt the binary format with a higher consumption efficiency, while JSON adopts the easier-to-use lightweight text format. The reference demo varies by the selected data format.

This document provides a demo of the Protobuf format. The demo already contains the Protobuf protocol file, so you don't need to download it separately. If you [download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe.proto) it on your own, use Protobuf 3.X for code generation to ensure that data structures are compatible.

## Notes

- **The demo only prints out the consumed data but does not contain the usage instructions of such data. You need to write your own data processing logic based on the demo.** You can also use Kafka clients in other languages to consume and parse data.
- Currently, data subscription to Kafka for consumption can be implemented over the Tencent Cloud private network but not the public network. In addition, the subscribed database instance and the data consumer must be in the same region.
- The delivery semantics of subscription to Kafka messages in DTS is to deliver a message at least once; therefore, the consumed data may be duplicated in special cases. For example, if the subscription task is restarted, the source binlog will be pulled before the interruption offset after the restart, resulting in repeated delivery of messages. Operations in the console such as modifying subscribed objects and restoring abnormal tasks may cause duplicate messages. If your business is sensitive to duplicate data, you need to add deduplication logic based on the business data in the consumption demo.


## Downloading a Consumption Demo
| Demo Language | TencentDB for MySQL, TencentDB for MariaDB, and TDSQL-C for MySQL           | TDSQL for MySQL                                | TDSQL for PostgreSQL                             |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Go            | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_go_demo_1.2.0.zip) | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_go_demo_1.0.3.zip) | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_postgresql_subscribe_kafka_go_demo_1.0.0.zip) |
| Java          | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_java_demo_1.2.0.zip) | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_java_demo_1.0.3.zip) | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_postgresql_subscribe_kafka_java_demo_1.0.0.zip) |
| Python 3       | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_python_demo_1.2.0.zip) | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_python_demo_1.0.3.zip) | [Download](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_postgresql_subscribe_kafka_python_demo_1.0.0.zip) |


## Instructions for the Java Demo
Compilation environment: Maven or Gradle and JDK 8.
Runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance). Install JRE 8.
Directions:
1. Create a data subscription task (NewDTS) as instructed in [Creating MySQL or TDSQL for MySQL Data Subscription](https://www.tencentcloud.com/document/product/571/47354).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download the Java demo and decompress it.
4. Access the decompressed directory. Maven model, pom.xml, and Gradle configuration files are placed in the directory for your use as needed.
  - Package the project with Maven by running `mvn clean package`.
  - Package the project with Gradle by running `gradle fatJar` (with all dependencies contained) or `gradle jar`.
5. Run the demo.
 - After packaging the project with Maven, go to the `target` folder and run `java -jar sub_demo-1.0-SNAPSHOT-jar-with-dependencies.jar --brokers=xxx --topic=xxx --group=xxx--user=xxx --password=xxx --trans2sql`.
 - After packaging the project with Gradle, go to the `tbuild/libs` folder and run `java -jar sub_demo-with-dependencies-1.0-SNAPSHOT.jar --brokers=xxx --topic=xxx --group=xxx--user=xxx --password=xxx --trans2sql`.
Here, `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660). `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535). `trans2sql` indicates whether to enable conversion to SQL statement. In Java code, if this parameter is carried, the conversion will be enabled.
6. Observe consumption.
![](https://main.qcloudimg.com/raw/fffa3de2a6e38b3752512183e1ffe785.png)

You can also use IDE for compilation and packaging. After packaging, you can see `sub_demo-1.0-SNAPSHOT-jar-with-dependencies` in the `target` folder in the project root directory, which is an executable JAR package containing all the required dependencies.

## Instructions for the Go Demo
Compiling environment: Go 1.12 or later, with the Go module environment configured.
Runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance).
Directions:
1. Create a data subscription task (NewDTS) as instructed in [Creating MySQL or TDSQL for MySQL Data Subscription](https://www.tencentcloud.com/document/product/571/47354).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download the Go demo and decompress it.
4. Access the decompressed directory and run `go build -o subscribe ./main` to generate the executable file `subscribe`.
5. Run `./subscribe --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=true`.
  Here, `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660). `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535). `trans2sql` indicates whether to enable conversion to SQL statement.
6. Observe consumption.
  ![](https://main.qcloudimg.com/raw/c94d9cfe2a62e903a6593e22ce2c60bf.png)

## Instructions for the Python 3 Demo
Compilation and runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance). Install Python 3 and pip3 (for dependency package installation).
Use `pip3` to install the dependency package:
```
pip install flag
pip install kafka-python
pip install protobuf
```
Directions:
1. Create a data subscription task (NewDTS) as instructed in [Creating MySQL or TDSQL for MySQL Data Subscription](https://www.tencentcloud.com/document/product/571/47354).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download the Python 3 demo and decompress it.
4. Run `python main.py --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=1`.
Here, `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660). `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535). `trans2sql` indicates whether to enable conversion to SQL statement.
5. Observe consumption.
![](https://main.qcloudimg.com/raw/6055041985904335b43d7df8f4e75561.png)

## [Key demo logic description](id:dgxljjj)

### Message production logic

This section describes the message production logic to help you better understand the consumption logic.
Protobuf is used for serialization. The demo for each programming language contains the Protobuf definition file, which defines several key data structures: `Envelope` is the structure of eventually sent Kafka messages; `Entry` is the structure of an individual subscription event; and `Entries` is a set of `Entry` structures. Below are their relationships:

![](https://qcloudimg.tencent-cloud.cn/raw/3dcceab6ea08686edf64c0517019d70d.png)

The production process is as follows:

1. Pull binlog messages and encode each binlog event into an `Entry`.
```
message Entry { // An `Entry` is the structure of an individual subscription event. An event is similar to a binlog event in MySQL.
    Header header = 1;  // The event header
    Event event   = 2;  // The event body
}
message Header {
    int32       version        = 1;   // The protocol version of the `Entry`
    SourceType  sourceType     = 2;   // The source database type, such as MySQL and Oracle
    MessageType messageType    = 3;   // The message type, i.e., event type, such as BEGIN, COMMIT, and DML
    uint32 timestamp           = 4;   // The event timestamp in the source binlog
    int64  serverId            = 5;   // The `serverId` of the source database
    string fileName            = 6;   // The filename of the source binlog
    uint64 position            = 7;   // The event offset in the source binlog file
    string gtid                = 8;   // The GTID of the current transaction
    string schemaName          = 9;   // The modified schema
    string tableName           = 10;  // The modified table
    uint64 seqId               = 11;  // The globally incremental serial number
    uint64 eventIndex          = 12;  // If a large event is sharded, the shard number starts from 0. This parameter is meaningless on the current version and is reserved for future use.
    bool   isLast              = 13;  // Whether the current shard is the last shard of a sharded event; if so, the value is `true`. This parameter is meaningless on the current version and is reserved for future use.
    repeated KVPair properties = 15;
}
message Event {
    BeginEvent      beginEvent      = 1;  // The begin event in the binlog
    DMLEvent        dmlEvent        = 2;  // The DML event in the binlog
    CommitEvent     commitEvent     = 3;  // The commit event in the binlog
    DDLEvent        ddlEvent        = 4;  // The DDL event in the binlog
    RollbackEvent   rollbackEvent   = 5;  // The rollback event. This parameter is meaningless on the current version and is reserved for future use.
    HeartbeatEvent  heartbeatEvent  = 6;  // The heartbeat event regularly sent by the source database
    CheckpointEvent checkpointEvent = 7;  // The checkpoint event added to the subscription backend, which is generated automatically once every 10 seconds and is used for Kafka production and consumption offset management.
    repeated KVPair properties      = 15;
}
```
2. Multiple `Entry` structures are merged to reduce the number of messages, and the structure of binlog events becomes `Entries` after the merge. The `Entries.items` field refers to the `Entry` sequence list. A reasonable number of `Entry` structures are merged so that the size is smaller than that of a single Kafka message. If a single binlog event has exceeded the size limit, `Entry` structures will not be merged anymore, so there will be only one `Entry` in the `Entries` structure.
```
message Entries {
        repeated Entry items = 1; // `Entry` list
}
```
3. Encode `Entries` with Protobuf to generate a binary sequence.
4. Put the binary sequence in the `data` field of an `Envelope`. If a single binlog event is oversize, the binary sequence may exceed the size limit of a single Kafka message. In this case, you can separate the binary sequence into multiple segments and put each segment in an `Envelope`.
`Envelope.total` and `Envelope.index` record the total number of `Envelope` structures and the serial number of the current `Envelope` structure (starting from 0) respectively.
```
message Envelope {
        int32  version                  = 1; // The protocol version, which determines how the data content is decoded.
        uint32 total                    = 2;
        uint32 index                    = 3;
        bytes  data                     = 4; // Here, `version` is 1, indicating that the data is `Entries` serialized in the ProtoBuf format.
        repeated KVPair properties      = 15;
}
```
5. Encode one or multiple `Envelope` structures generated in the previous step in sequence and publish the `Envelope` structures to Kafka partitions. Multiple `Envelope` structures in the same `Entries` are published to the same partition in sequence.

### Message consumption logic

The following simply describes the consumption logic. Directions for demos in three languages are the same.

1. Create a Kafka consumer.
2. Start the consumption.
3. Consume original messages in sequence and find the corresponding `partitionMsgConsumer` object of a message partition. The object will process these messages.
4. The `partitionMsgConsumer` object deserializes messages into the `Envelope` structure.
```
	// Convert the value of the Kafka message to an `Envelope`.
	envelope := subscribe.Envelope{}
	err := proto.Unmarshal(msg.Value, &envelope)
```
5. The `partitionMsgConsumer` object continuously consumes one or multiple messages according to the `index` and `total` recorded in the `Envelope` until `Envelope.index` equals to `Envelope.total-1` (which indicates that a complete `Entries` is received. See the consumption and production logic mentioned above).
6. Combine the `data` fields of multiple consecutive `Envelope` structures received together in sequence. Decode the combined binary sequences into `Entries` with Protobuf.
```
	if envelope.Index == 0 {
		pmc.completeMsg = envelope
	} else {
        // Splice the split binary sequences of `Entries`
		pmc.completeMsg.Data = append(pmc.completeMsg.Data, envelope.Data...)
	}
	if envelope.Index < envelope.Total-1 {
		return nil
	}
	// Deserialize `Envelope.Data` to `Entries`
	entries := subscribe.Entries{}
	err = proto.Unmarshal(pmc.completeMsg.Data, &entries)

```
7. Process `Entries.items` in sequence, and print the original `Entry` structure or convert it into a SQL statement.
8. When a checkpoint message (a special message written to Kafka by the subscription backend once every 10 seconds) is consumed, submit the Kafka message offset from the consumer. 

## Database Field Mapping and Storage

This section describes the mappings between database field types and data types defined in the Protobuf protocol.
A field value in the source database such as MySQL is stored in the following data structure in the Protobuf protocol:

```
message Data {
     DataType     dataType = 1;
     string       charset  = 2;  // The encoding (string) type of DataType_STRING, with the value stored in `bv`
     string       sv       = 3;  // The string value of DataType_INT8/16/32/64/UINT8/16/32/64/Float32/64/DataType_DECIMAL
     bytes        bv       = 4;  // The value of DataType_STRING/DataType_BYTES
}
```
The field `DataType` refers to the type of stored fields.
```
enum DataType {
     NIL     = 0; // The value is NULL
     INT8    = 1;
     INT16   = 2;
     INT32   = 3;
     INT64   = 4;
     UINT8   = 5;
     UINT16  = 6;
     UINT32  = 7;
     UINT64  = 8;
     FLOAT32 = 9;
     FLOAT64 = 10;
     BYTES   = 11;
     DECIMAL = 12;
     STRING  = 13;
     NA      = 14; // The value does not exist (N/A).
}
```
The `bv` field stores the binary representation of STRING and BYTES; the `sv` field stores the string representation of INT8/16/32/64/UINT8/16/32/64/DECIMAL; the `charset` field stores the encoding type of STRING.

Mapping between MySQL/TDSQL original type and `DataType` is as shown below (the `MYSQL_TYPE_INT8/16/24/32/64` modified by `UNSIGNED` is respectively mapped to `UINT8/16/32/32/64`):

> ?
> - DATE, TIME, and DATETIME types don't support time zone.
> - The TIMESTAMP type supports time zone. For fields of this type, the system will convert the current time zone to Universal Time Coordinated (UTC) when storing them and convert UTC back to the current time zone when querying them.
> - The `MYSQL_TYPE_TIMESTAMP` and `MYSQL_TYPE_TIMESTAMP_NEW` fields carry the time zone information, which you can convert on your own when consuming data. For example, the format of the time data output by DTS is a string with time zone, such as `2021-05-17 07:22:42 +00:00`, where `+00:00`indicates the UTC time. You need to take into account the time zone information when parsing and converting the data.

| MySQL/TDSQL Field Type | Protobuf DataType Enumerated Value |
| ------------------------------------------- | ----------------------------- |
| MYSQL_TYPE_NULL                             | NIL                           |
| MYSQL_TYPE_INT8                             | INT8                          |
| MYSQL_TYPE_INT16                            | INT16                         |
| MYSQL_TYPE_INT24                            | INT32                         |
| MYSQL_TYPE_INT32                            | INT32                         |
| MYSQL_TYPE_INT64                            | INT64                         |
| MYSQL_TYPE_BIT                              | INT64                         |
| MYSQL_TYPE_YEAR                             | INT64                         |
| MYSQL_TYPE_FLOAT                            | FLOAT32                       |
| MYSQL_TYPE_DOUBLE                           | FLOAT64                       |
| MYSQL_TYPE_VARCHAR                          | STRING                        |
| MYSQL_TYPE_STRING                           | STRING                        |
| MYSQL_TYPE_VAR_STRING                       | STRING                        |
| MYSQL_TYPE_TIMESTAMP                        | STRING                        |
| MYSQL_TYPE_DATE                             | STRING                        |
| MYSQL_TYPE_TIME                             | STRING                        |
| MYSQL_TYPE_DATETIME                         | STRING                        |
| MYSQL_TYPE_TIMESTAMP_NEW                    | STRING                        |
| MYSQL_TYPE_DATE_NEW                         | STRING                        |
| MYSQL_TYPE_TIME_NEW                         | STRING                         |
| MYSQL_TYPE_DATETIME_NEW                     | STRING                        |
| MYSQL_TYPE_ENUM                             | STRING                        |
| MYSQL_TYPE_SET                              | STRING                        |
| MYSQL_TYPE_DECIMAL                          | DECIMAL                       |
| MYSQL_TYPE_DECIMAL_NEW                      | DECIMAL                       |
| MYSQL_TYPE_JSON                             | BYTES                         |
| MYSQL_TYPE_BLOB                             | BYTES                         |
| MYSQL_TYPE_TINY_BLOB                        | BYTES                         |
| MYSQL_TYPE_MEDIUM_BLOB                      | BYTES                         |
| MYSQL_TYPE_LONG_BLOB                        | BYTES                         |
| MYSQL_TYPE_GEOMETRY                         | BYTES                         |

