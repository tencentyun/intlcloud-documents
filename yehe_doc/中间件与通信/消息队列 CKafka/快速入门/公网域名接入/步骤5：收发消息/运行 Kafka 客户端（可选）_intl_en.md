## Overview

This document explains how to start using Kafka APIs after you purchase the CKafka service. You need to download and decompress the Kafka installation file and perform simple testing on Kafka APIs.

## Directions

### Step 1. Install a JDK.

#### 1. Check Java installation.

Open a terminal window and run this command:
<dx-codeblock>
:::  sh
java -version
:::
</dx-codeblock>

If the Java version number is output, Java installation is successful. If Java has not been installed, [download and install the JDK](https://www.oracle.com/java/technologies/downloads/).


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

Download and decompress the [Kafka installation file](https://archive.apache.org/dist/kafka/1.1.1/kafka_2.11-1.1.1.tgz).


### Step 3. Test Kafka APIs.

1. Configure an ACL policy locally.
   1. In the `./config` directory of the installation file, add the following content at the end of `producer.properties` and `consumer.properties`.
   <dx-codeblock>
   :::  properties
      security.protocol=SASL_PLAINTEXT 
      sasl.mechanism=PLAIN
   :::
   </dx-codeblock>
   2. Create a file named `ckafka_client_jaas.conf`, and add the following content.
   <dx-codeblock>
   :::  properties
      KafkaClient {
                 org.apache.kafka.common.security.plain.PlainLoginModule required
                 username="yourinstance#yourusername"
                 password="yourpassword";
      };
   :::
   </dx-codeblock>
   <dx-alert infotype="explain" title="">
   Set `username` to a value in the format of `instance ID` + `#` + `configured username`, and `password` to a configured password.
   </dx-alert>
   3. In the `./bin` directory of the installation file, add the statement of the full path of the JAAS file at the beginning of `kafka-console-producer.sh` and `kafka-console-consumer.sh`.
   <dx-codeblock>
   :::  bash
      export KAFKA_OPTS="-Djava.security.auth.login.config=****/config/ckafka_client_jaas.conf"
   :::
   </dx-codeblock>
2. Go to the `./bin` directory, and produce and consume a message via CLI commands.
   1. Open a terminal window to start a consumer.
   <dx-codeblock>
   :::  bash
      bash kafka-console-consumer.sh --bootstrap-server XXXX:port --topic XXXX --consumer.config ../config/consumer.properties
   :::
   </dx-codeblock>
   <dx-alert infotype="explain" title="">
- broker-list: Replace `XXXX:port` with the domain name and port for public network access, which can be obtained in the **Access Mode** section on the **Instance Details** page in the console.
  ![](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png)
- topic: Replace `XXXX` with the topic name, which can be obtained on the **Topic Management** page in the console.
</dx-alert>
   2. Open another terminal window to start a producer.
<dx-codeblock>
:::  bash
 bash kafka-console-producer.sh --broker-list XXXX:port --topic XXXX --producer.config ../config/producer.properties
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
- broker-list: Replace `XXXX:port` with the domain name and port for public network access, which can be obtained in the **Access Mode** section on the **Instance Details** page in the console.
  ![](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png)
- topic: Replace `XXXX` with the topic name, which can be obtained on the **Topic Management** page in the console.
</dx-alert>

      Enter the content of the message and press Enter.
<ul><li><b>Producing a message:</b>
      <img src = "https://qcloudimg.tencent-cloud.cn/raw/34e000095c6bd53b191d644593c466a8.png"> 

      <li><b>Consuming a message:</b>
      <img src = "https://qcloudimg.tencent-cloud.cn/raw/14ec265fe6ef5edd5f95c98891245637.png">  

3. In the message querying page of the CKafka console, query the message sent.
   ![](https://main.qcloudimg.com/raw/80db39a21f7eb35de16f37b1c8670650.png)
    The details of the message are as follows:
   ![](https://main.qcloudimg.com/raw/06cdc6450beefae7f6cc6f3d704390a0.png)
