In data subscription (Kafka Edition), you can consume the subscribed data through Kafka 0.11 or later available at [DOWNLOAD](http://kafka.apache.org/downloads). This document provides client consumption demos for Java, Go, and Python for you to quickly test the process of data consumption and understand the method of data parsing.

When configuring the subscription task, you can select different formats of subscribed data, including ProtoBuf, Avro, and JSON. ProtoBuf and Avro adopt the binary format with a higher consumption efficiency, while JSON adopts the easier-to-use lightweight text format. The reference demo varies by the selected data format.

This document provides a demo of the JSON format. The demo already contains the JSON protocol file, so you don't need to download it separately.

> ?
>
> Currently, data consumption over the JSON protocol is supported only for MySQL and TDSQL-C for MySQL.

## Notes
- **The demo only prints out the consumed data but does not contain the usage instructions of such data. You need to write your own data processing logic based on the demo.** You can also use Kafka clients in other languages to consume and parse data.
- Currently, data subscription to Kafka for consumption can be implemented over the Tencent Cloud private network but not the public network. In addition, the subscribed database instance and the data consumer must be in the same region.
- The Kafka built in DTS has a certain upper limit for processing individual messages. When a single row of data in the source database exceeds 10 MB, this row may be discarded.
- The delivery semantics of subscription to Kafka messages in DTS is to deliver a message at least once; therefore, the consumed data may be duplicated in special cases. For example, if the subscription task is restarted, the source binlog will be pulled before the interruption offset after the restart, resulting in repeated delivery of messages. Operations in the console such as modifying subscribed objects and restoring abnormal tasks may cause duplicate messages. If your business is sensitive to duplicate data, you need to add deduplication logic based on the business data in the consumption demo.
- If you have used or are familiar with the open-source subscription tool Canal, you can choose to convert the consumed JSON data to a Canal-compatible data format for subsequent processing. The demo already supports this feature, and you can implement it by adding the `trans2canal` parameter in the demo startup parameters. Currently, this feature is supported only in Java.  


## Downloading a Consumption Demo
| Demo Language | TencentDB for MySQL and TDSQL-C for MySQL |
| ------------- | ------------------------------------------------------------ |
| Go            | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-json-go.zip) |
| Java          | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-json-java-1.0.1.zip) |
| Python 3       | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/consumerDemo-json-python.zip) |

## Instructions for the Java Demo
Compilation environment: Maven and JDK 8. You can choose a desired package management tool. The following takes Maven as an example.
Runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance). Install JRE 8.
Directions:
1. Create a data subscription task (NewDTS) as instructed in [Creating MySQL or TDSQL for MySQL Data Subscription](https://intl.cloud.tencent.com/document/product/571/47354).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download the Java demo and decompress it.
4. Access the decompressed directory. Maven model and pom.xml files are placed in the directory for your use as needed.
    Package the project with Maven by running `mvn clean package`.
5. Run the demo.
    After packaging the project with Maven, go to the target folder `target` and run the following code:
    `java -jar consumerDemo-json-1.0-SNAPSHOT.jar --brokers xxx --topic xxx --group xxx --user xxx --password xxx --trans2sql --trans2canal`.
 - `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660).
 - `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535).
 - `trans2sql` indicates whether to enable conversion to SQL statement. In Java code, if this parameter is carried, the conversion will be enabled.
 - `trans2canal` indicates whether to print the data in Canal format. If this parameter is carried, the conversion will be enabled. 
6. Observe consumption.
![](https://main.qcloudimg.com/raw/fffa3de2a6e38b3752512183e1ffe785.png)

## Instructions for the Go Demo
Compiling environment: Go 1.12 or later, with the Go module environment configured.
Runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance).
Directions:
1. Create a data subscription task (NewDTS) as instructed in [Creating MySQL or TDSQL for MySQL Data Subscription](https://intl.cloud.tencent.com/document/product/571/47354).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download the Go demo and decompress it.
4. Access the decompressed directory and run `go build -o subscribe ./main/main.go` to generate the executable file `subscribe`.
5. Run `./subscribe --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=true`.
 - `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660).
 - `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535).
 - `trans2sql` indicates whether to enable conversion to SQL statement.
6. Observe consumption.
![](https://main.qcloudimg.com/raw/c94d9cfe2a62e903a6593e22ce2c60bf.png)

## Instructions for the Python 3 Demo
Compilation and runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region as the subscribed instance). Install Python 3 and pip3 (for dependency package installation).
Use `pip3` to install the dependency package:
```
pip install flag
pip install kafka-python
```
Directions:
1. Create a data subscription task (NewDTS) as instructed in [Creating MySQL or TDSQL for MySQL Data Subscription](https://intl.cloud.tencent.com/document/product/571/47354).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download the Python 3 demo and decompress it.
4. Run `python main.py --brokers=xxx --topic=xxx --group=xxx --user=xxx --password=xxx --trans2sql=1`.
 - `broker` is the private network access address for data subscription to Kafka, and `topic` is the subscription topic, which can be viewed on the **Subscription details** page as instructed in [Viewing Subscription Details](https://intl.cloud.tencent.com/document/product/571/42660).
 - `group`, `user`, and `password` are the name, account, and password of the consumer group, which can be viewed on the **Consumption Management** page as instructed in [Managing Consumer Group](https://intl.cloud.tencent.com/document/product/571/39535).
 - `trans2sql` indicates whether to enable conversion to SQL statement.
5. Observe consumption.
![](https://main.qcloudimg.com/raw/6055041985904335b43d7df8f4e75561.png)

## [Protocol File Description](id:dgxljjj)
The demo for each programming language uses JSON for serialization and contains a `Record` definition file.
In the demo for Java, the path of the definition file is `consumerDemo-json-java\src\main\java\json\FlatRecord.java`.

### Fields in the record

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
| oldColumns               | The column values before DML statement execution, which are output as a string. For binary or geometry data types, a hex value will be output. |
| newColumns               | The column values after DML statement execution, which are output as a string. For binary or geometry data types, a hex value will be output. |
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

### MySQL column attributes in the record
- name: The column name.
- dataTypeNumber: The type of the data recorded in the binlog. For values, see [COM_QUERY Response](https://dev.mysql.com/doc/internals/en/com-query-response.html).
- isKey: Whether the current key is the primary key.
- originalType: The type defined in DDL.

### MySQL data type conversion logic
In the JSON protocol, all MySQL data types are converted to strings.
- String types such as `varchar` are all converted to UTF-8 encoding.
- Numeric types are all converted to strings equal to the value, such as "3.0".
- Time types are output in the format of `yyyy-dd-mm hh:MM:ss.milli`.
- Timestamp types are output as the number of milliseconds.
- Binary types such as `binary` and `blob` are output as strings equal to their hex values, such as "0xfff".


