## Overview

This document explains how to start using Kafka APIs after you purchase the CKafka service. After setting up a CKafka environment on an CVM instance, you need to download and decompress the Kafka installation file and perform simple testing on Kafka APIs.

## Directions

### Step 1. Install a JDK.

#### 1. Check Java installation.

Open a terminal window and run this command:
```
java -version
```
If the output of the command is a Java version number, then Java is already installed in your system. If you have not installed Java yet, download and install a [Java Development Kit (JDK)](http://kafka.apache.org/downloads)


#### 2. Set up the Java environment.

Set the `JAVA_HOME` environment variable and point it to the Java installation directory on your machine. 
For example, if you use Java JDK 1.8.0_20, the outputs on different operating systems are as follows:

| OS | Output                                                         |
| -------- | ------------------------------------------------------------ |
| Windows  | Set the environment variable `JAVA_HOME` to <br/>C:\Program Files\Java\jdkjdk1.8.0_20 |
| Linux    | export JAVA_HOME=/usr/local/java-current                     |
| macOS  | export JAVA_HOME=/Library/Java/Home                          |

 Add the Java compiler path to the system path:

| OS | Output                                                         |
| -------- | ------------------------------------------------------------ |
| Windows  | Add `;C:\Program Files\Java\jdk1.8.0_20\bin` to the end of the system variable `PATH`. |
| Linux    | export PATH=$PATH:$JAVA_HOME/bin/                            |
| macOS  | not required                                                 |

 Use the `java -version` command to check your Java installation.

### Step 2. Download the Kafka installation file.

Download and decompress the [Kafka installation file](http://kafka.apache.org/downloads).
Currently, CKafka is fully compatible with Kafka 0.9, 0.10, 1.1, and 2.4. We recommend that you download one of these versions. This document uses kafka_2.12-1.1.1 as an example.

### Step 3. Test Kafka APIs.

1. Configure an ACL policy locally.
   1. In the `./config` directory of the installation file, add the following content at the end of `producer.properties` and `consumer.properties`.
      ```properties
      security.protocol=SASL_PLAINTEXT 
      sasl.mechanism=PLAIN
      ```
   2. Create a file named `ckafka_client_jaas.conf`, and add the following content.
      ```properties
      KafkaClient {
          org.apache.kafka.common.security.plain.PlainLoginModule required
          username="yourinstance#yourusername"
          password="yourpassword";
      };
      ```
      >?  `username` is in the format of "instance ID#entered username", and `password` is the password set. 

   3. In the `./bin` directory of the installation file, add the statement of the full path of the JAAS file at the beginning of `kafka-console-producer.sh` and `kafka-console-consumer.sh`.
      ```bash
      export KAFKA_OPTS="-Djava.security.auth.login.config=****/config/ckafka_client_jaas.conf"
      ```

2. Go to the `./bin` directory, and produce and consume a message via CLI commands.
   1. Open a terminal window to start a consumer.
      ```bash
      bash kafka-console-consumer.sh --bootstrap-server XXXX:port --topic test --consumer.config ../config/consumer.properties
      ```
      >? Replace `XXXX:port` with the domain name and port for public network access.
      >![](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png)

   2. Open another terminal window to start a producer.
      ``` bash
      bash kafka-console-producer.sh --broker-list XXXX:port --topic test --producer.config ../config/producer.properties
      ```
      >? Replace `XXXX:port` with the domain name and port for public network access.
      >![](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png)

      Enter the content of the message and press Enter.

      **Producing a message:**
      ![](https://main.qcloudimg.com/raw/c25bdccd293ea4382064b57eec08a2fe.png)

      **Consuming a message:**
      ![](https://main.qcloudimg.com/raw/22860d730e70cfbe9eb5fcbca215d5a5.png)

3. In the message querying page of the CKafka console, query the message sent.
   ![](https://main.qcloudimg.com/raw/80db39a21f7eb35de16f37b1c8670650.png)
	 The details of the message are as follows:
   ![](https://main.qcloudimg.com/raw/06cdc6450beefae7f6cc6f3d704390a0.png)
