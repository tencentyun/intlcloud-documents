
Data Subscription Kafka Edition enables you to directly consume subscribed data through Kafka client version 0.11 and later versions. This document provides two client consumption demos in Java, Go and Python languages.

## Downloading Consumption Demo (for TencentDB for MySQL & TencentDB for MariaDB)
Refer to the following table to download the consumption demo code of the client of Data Subscription Kafka Edition:

| Demo Language | Download Address |
| ------------- | ------------------------------------------------------------ |
| Go | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_go_demo_1.1.1.zip) |
| Java | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_java_demo_1.1.1.zip) |
| Python3 | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe_kafka_python_demo_1.1.1.zip) |

## Downloading Consumption Demo (for TDSQL for MySQL)
Refer to the following table to download the consumption demo code of the client of Data Subscription Kafka Edition:

| Demo Language | Download Address |
| ------------- | ------------------------------------------------------------ |
| Go | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_go_demo_1.0.0.zip) |
| Java | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_java_demo_1.0.1.zip) |
| Python | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/tdsql_subscribe_kafka_python_demo_1.0.1.zip) |

## Downloading Protobuf Proto File
| Proto File | Download Address |
| ------------- | ------------------------------------------------------------ |
| Protobuf | [Address](https://subscribesdk-1254408587.cos.ap-beijing.myqcloud.com/subscribe.proto) |


## Configuration Parameters
| Parameter | Description |
| ---------- | --------------------------- |
| brokerlist | The private network access address of Data Subscription Kafka Edition |
| topic | The subscription topic of the data subscription channel |
| group | Consumer group name |
| user | Consumer group account name |
| password | Consumer group password |
| trans2sql  | Whether to convert into SQL statements |


## [Key Demo Logic Description](id:dgxljjj)
### Production logic
We will simply describe the message production logic to help you better understand the consumption logic.
Protobuf is used for serialization. Demos in all languages contain Protobuf definition files which define a few key structures: `envelope` is the structure of the Kafka messages that are finally sent; `entry` is a single subscription event structure; `entries` is the collection of multiple entries.

The production process is as follows:
1. Pull binlog messages and encode each binlog event into an entry structure.
![](https://main.qcloudimg.com/raw/5e956452e68b1fed8c2a32c0207dc887.png)
2. Multiple entries are merged to reduce the number of messages, and the structure of binlog events becomes `entries` after the merge. The field `Entries.items` refers to the entry sequence list. A reasonable number of entries are merged so that the size is smaller than that of a single Kafka message. If a single binlog event has exceeded the size limit, entries will not be merged anymore, so there is only one entry in the `entries` structure.
![](https://main.qcloudimg.com/raw/79f305c3d844b580940636cd228b2299.png)
3. Encode entries with Protobuf to generate a binary sequence.
4. Put the binary sequence in the `data` field of an envelope. If a single binlog event is oversize, the binary sequence may exceed the size limit of a single Kafka message. In this case, we can separate the binary sequence into multiple segments and put each segment in an envelope.
`Envelope.index` and `Evelope.total` are used to record the serial number (starting from 0) of the current envelope and the total number of segments, respectively.
![](https://main.qcloudimg.com/raw/15fbcfc17bdb217de520cb662f2ce52b.png)
5. Encode one or multiple envelopes generated in the previous step in sequence and publish them to Kafka partitions. Multiple envelopes based on the same entries are published to the same partition in sequence.

### Consumption logic
We will simply describe the consumption logic. Directions for demos in three languages are the same.
1. Create a Kafka consumer.
2. Start the consumption.
3. Consume original messages in sequence and find the corresponding `partitionMsgConsumer` object of a message partition. The object will process these messages.
4. The `partitionMsgConsumer` object deserializes messages into the `envelope` structure.
![](https://main.qcloudimg.com/raw/15fbcfc17bdb217de520cb662f2ce52b.png)
5. The `partitionMsgConsumer` object continuously consumes one or multiple messages according to the `index` and `total` recorded in the envelope until `Envlope.index` equals to `Envelope.total-1` (this indicates that a complete `entries` is received. See the consumption and production logic mentioned above).
6. Combine the `data` fields of multiple consecutive envelopes received together in sequence. Decode the combined binary sequences into entries with Protobuf.
![](https://main.qcloudimg.com/raw/a5368cd3c3ef9ec800a25d97ce5c13e0.png)
7. Process `Entries.items` in sequence, and print the original `entry` structure or convert it into an SQL statement.
![](https://main.qcloudimg.com/raw/5e956452e68b1fed8c2a32c0207dc887.png)

## Instructions for Java Demo
Compiling environment: the package management tool Maven or Gradle, and JDK8.
Runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region of the subscribed instance). Install JRE8.
Directions:
1. Create a new edition of data subscription channel. For more information, see [Data Subscription Kafka Edition](https://intl.cloud.tencent.com/document/product/571/39531).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download Java Demo and decompress it.
4. Access the decompressed directory. Maven model files, pom.xml files and Gradle related configuration files are placed in the directory so that users can use them as needed.
  - Package Java demo projects with Maven: use the command `mvn clean package`.
  - Package Java demo projects with Gradle: you can either package these projects with the command `gradle fatJar` and contain all dependencies in the package, or package them with the command `gradle jar`.
5. Run: after using Maven to package Java demo projects, enter the target folder `target` and run `java -jar sub_demo-1.0-SNAPSHOT-jar-with-dependencies.jar --brokers=xxx --topic=xxx --group=xxx--user=xxx --password=xxx --trans2sql`.
After using Gradle to package Java demo projects, enter the folder `build/libs` and run `java -jar sub_demo-with-dependencies-1.0-SNAPSHOT.jar --brokers=xxx --topic=xxx --group=xxx--user=xxx --password=xxx --trans2sql`.
6. Observe consumption.
![](https://main.qcloudimg.com/raw/fffa3de2a6e38b3752512183e1ffe785.png)

You can also use IDE (integrated development environment) for compiling and packaging. Here we take the software IntelliJ IDEA as an example:
1. Open this software and click ** Open**.
![](https://main.qcloudimg.com/raw/9d199900b36a43840825dc52dfa2c567.png)
2. Find the decompressed directory of Demo in the pop-up dialog box, find the `pom.xml` file in the directory as shown in the figure below, and click **Open**.
![](https://main.qcloudimg.com/raw/1747158bf764aa898468bfa2bdb22054.png)
3. In the pop-up dialog box, click **Open as Project**.
![](https://main.qcloudimg.com/raw/6b169744f3529f362fb81bb86becf593.png)
4. In the pop-up window, double-click “package” under “Lifecycle” in the Maven management window on the right, and package.
![](https://main.qcloudimg.com/raw/63d85885b88dce1d65483abea6b9d3d3.png)
After the packaging, the `sub_demo-1.0-SNAPSHOT-jar-with-dependencies` under the `target` folder in the root directory is a runnable jar package which contains the dependencies it requires.
Directions for packaging with Gradle are similar.

## Instructions for Golang Demo
Compiling environment: Golang 1.12 and later versions. The Go Module environment has been configured.
Runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region of the subscribed instance).
Directions:
1. Create a new edition of data subscription channel. For more information, see [Data Subscription Kafka Edition](https://intl.cloud.tencent.com/document/product/571/39531).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download Golang Demo and decompress it.
4. Access the decompressed directory, run `go build -o subscribe ./main`, and the executable file `subscribe` will be generated.
5. Run `./subscribe --brokers=xxx --topic=xxx --group=xxx --user=xxx \--password=xxx --trans2sql=true`.
6. Observe consumption.
![](https://main.qcloudimg.com/raw/c94d9cfe2a62e903a6593e22ce2c60bf.png)

## Instructions for Python3 Demo
Compilation and runtime environment: Tencent Cloud CVM (which can access the private network address of the Kafka server only if it is in the same region of the subscribed instance). Python3 and pip3 have been installed for dependency package installation.
Use `pip3` to install the dependency package:
```
pip install flag
pip install kafka-python
pip install protobuf
```
Directions:
1. Create a new edition of data subscription channel. For more information, see [Data Subscription Kafka Edition](https://intl.cloud.tencent.com/document/product/571/39531).
2. Create one or multiple consumer groups. For more information, see [Adding Consumer Group](https://intl.cloud.tencent.com/document/product/571/39534).
3. Download Python3 Demo and decompress it.
4. Run `python main.py --brokers=xxx --topic=xxx --group=xxx --user=xxx \--password=xxx --trans2sql=1`.
5. Observe consumption.
![](https://main.qcloudimg.com/raw/6055041985904335b43d7df8f4e75561.png)

## Field Mapping and Storage
Specific MySQL/TDSQL field values in a Protobuf protocol are stored in the data structure shown in the figure below.
![](https://main.qcloudimg.com/raw/2d0af55b06c62f410e715f150391cb62.png)
The field `DataType` refers to the type of stored fields. Valid enumerated values are shown in the figure below.
![](https://main.qcloudimg.com/raw/b9b5b081d2f12f6bfda3c24a7043b8e7.png)
The `bv` field stores the binary representation of STRING and BYTES; the `sv` field stores the string representation of INT8/16/32/64/UINT8/16/32/64/DECIMAL; the `charset` field stores the encoding type of STRING.

Mapping between MySQL/TDSQL original type and `DataType` is shown below (the `MYSQL_TYPE_INT8/16/24/32/64` modifed by `UNSIGNED` is respectively mapped to `UINT8/16/32/32/64`):

| MySQL/TDSQL Field Type | Protobuf DataType Enumerated Value |
| ------------------------------------------- | ----------------------------- |
| MYSQL_TYPE_NULL | NIL |
| MYSQL_TYPE_INT8 | INT8 |
| MYSQL_TYPE_INT16 | INT16 |
| MYSQL_TYPE_INT24 | INT32 |
| MYSQL_TYPE_INT32 | INT32 |
| MYSQL_TYPE_INT64 | INT64 |
| MYSQL_TYPE_BIT | INT64 |
| MYSQL_TYPE_YEAR | INT64 |
| MYSQL_TYPE_FLOAT | FLOAT32 |
| MYSQL_TYPE_DOUBLE | FLOAT64 |
| MYSQL_TYPE_VARCHAR | STRING |
| MYSQL_TYPE_STRING | STRING |
| MYSQL_TYPE_VAR_STRING | STRING |
| MYSQL_TYPE_TIMESTAMP | STRING |
| MYSQL_TYPE_DATE | STRING |
| MYSQL_TYPE_TIME | STRING |
| MYSQL_TYPE_DATETIME | STRING |
| MYSQL_TYPE_TIMESTAMP_NEW | STRING |
| MYSQL_TYPE_DATE_NEW | STRING |
| MYSQL_TYPE_TIME_NEW | STRNG |
| MYSQL_TYPE_DATETIME_NEW | STRING |
| MYSQL_TYPE_ENUM | STRING |
| MYSQL_TYPE_SET | STRING |
| MYSQL_TYPE_DECIMAL | DECIMAL |
| MYSQL_TYPE_DECIMAL_NEW | DECIMAL |
| MYSQL_TYPE_JSON | BYTES |
| MYSQL_TYPE_BLOB | BYTES |
| MYSQL_TYPE_TINY_BLOB | BYTES |
| MYSQL_TYPE_MEDIUM_BLOB | BYTES |
| MYSQL_TYPE_LONG_BLOB | BYTES |
| MYSQL_TYPE_GEOMETRY | BYTES |

