## Overview

This document explains how to start using Kafka APIs after you purchase the CKafka service. After setting up a CKafka environment on an CVM instance, you need to download and decompress the Kafka installation file and perform simple testing on Kafka APIs.

## Directions

### Step 1. Install a JDK

#### 1. Check Java installation

Open a terminal window and run this command:

```
java -version
```

If the Java version number is output, Java installation is successful. If Java has not been installed, please [download and install the JDK](http://kafka.apache.org/downloads).


#### 2. Set up the Java environment

Set the `JAVA_HOME` environment variable and point it to the Java installation directory on your machine. 
For example, if you use Java JDK 1.8.0_20, the outputs on different operating systems are as follows:

| OS | Output                                                         |
| -------- | ------------------------------------------------------------ |
| Windows  | Set the environment variable JAVA_HOME to <br/>C:\Program Files\Java\jdkjdk1.8.0_20 |
| Linux    | export JAVA_HOME=/usr/local/java-current                     |
| Mac OSX  | export JAVA_HOME=/Library/Java/Home                          |

 Add the Java compiler path to the system path:

| OS | Output                                                         |
| -------- | ------------------------------------------------------------ |
| Windows  | Add `;C:\Program Files\Java\jdk1.8.0_20\bin` to the end of the system variable `PATH`. |
| Linux    | export PATH=$PATH:$JAVA_HOME/bin/                            |
| Mac OSX  | not required                                                 |

 Use the `java -version` command to check your Java installation.

### Step 2. Download the Kafka installation file

Download and decompress the [Kafka installation file](http://kafka.apache.org/downloads).
Currently, CKafka is fully compatible with Kafka 0.9, 0.10, 1.1, and 2.4. We recommend that you download one of these versions. This document uses kafka_2.12-1.1.1 as an example.

### Step 3. Test Kafka APIs

Go to the `./bin` directory and produce and consume a message with CLI commands.

1. Open a terminal window to start the consumer.
   ```bash
   bash kafka-console-consumer.sh --bootstrap-server XXXX:port --topic XXXX --consumer.config ../config/consumer.properties
   ```
   >?
   >- Replace `XXXX:port` with the domain name and port for VPC access, which can be obtained in the **Access Mode** section on the **Instance Details** page in the console.
   >  ![](https://main.qcloudimg.com/raw/88b29cffdf22e3a0309916ea715057a1.png)
   >- topic: replace `XXXX` with the topic name, which can be obtained on the **Topic Management** page in the console.

2. Open another terminal window to start the producer.
   ``` bash
   bash kafka-console-producer.sh --broker-list XXXX:port --topic XXXX --producer.config ../config/producer.properties
   ```
   >?
   >- Replace `XXXX:port` with the domain name and port for VPC access, which can be obtained in the **Access Mode** section on the **Instance Details** page in the console.
   >  ![](https://main.qcloudimg.com/raw/88b29cffdf22e3a0309916ea715057a1.png)
   >- topic: replace `XXXX` with the topic name, which can be obtained on the **Topic Management** page in the console.

   Enter the content of the message, press Enter, and you can see that the consumer received the message almost at the same time.

   **Producing a message:**
   ![](https://main.qcloudimg.com/raw/c25bdccd293ea4382064b57eec08a2fe.png)

   **Consuming a message:**
   ![](https://main.qcloudimg.com/raw/22860d730e70cfbe9eb5fcbca215d5a5.png)

3. In the message querying page of the CKafka console, query the message sent.
   ![](https://main.qcloudimg.com/raw/80db39a21f7eb35de16f37b1c8670650.png)
    The details of the message are as follows:
   ![](https://main.qcloudimg.com/raw/06cdc6450beefae7f6cc6f3d704390a0.png)
