## Overview

This document explains how to start using Kafka APIs after you purchase the CKafka service. After setting up a CKafka environment on a CVM instance, you need to download and decompress the Kafka installation file and perform simple testing on Kafka APIs.

## Directions

### Step 1. Install a JDK.

#### 1. Check Java installation.

Open a terminal window and run this command:
<dx-codeblock>
:::  shell
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
![](https://main.qcloudimg.com/raw/1233548b38c82e92116eedbba9de534e.png)
Go to the `./bin` directory, and produce and consume a message via CLI commands.

1. Open a terminal window to start a consumer.
<dx-codeblock>
:::  bash
bash kafka-console-consumer.sh --bootstrap-server XXXX:port --topic XXXX --consumer.config ../config/consumer.properties
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
- Replace `XXXX:port` with the domain name and port for VPC access, which can be obtained in the **Access Mode** section on the **Instance Details** page in the console.
  ![](https://main.qcloudimg.com/raw/1233548b38c82e92116eedbba9de534e.png)
- topic: Replace `XXXX` with the topic name, which can be obtained on the **Topic Management** page in the console.
</dx-alert>
2. Open another terminal window to start a producer.
<dx-codeblock>
:::  bash
bash kafka-console-producer.sh --broker-list XXXX:port --topic XXXX --producer.config ../config/producer.properties
:::
</dx-codeblock>
<dx-alert infotype="explain" title="">
- Replace `XXXX:port` with the domain name and port for VPC access, which can be obtained in the **Access Mode** section on the **Instance Details** page in the console.
 ![](https://main.qcloudimg.com/raw/1233548b38c82e92116eedbba9de534e.png)
- topic: Replace `XXXX` with the topic name, which can be obtained on the **Topic Management** page in the console.
</dx-alert>

   Enter the content of the message and press Enter.
<ul><li><b>Producing a message:</b>
   <img src = "https://qcloudimg.tencent-cloud.cn/raw/30f5a8207a552023b2954b1e599c7f88.png"> 

   <li><b>Consuming a message:</b>
   <img src = "https://qcloudimg.tencent-cloud.cn/raw/2a09bee955acd0cd238977ec5bc250e5.png"> 
 
3. In the message querying page of the CKafka console, query the message sent.
   ![](https://main.qcloudimg.com/raw/80db39a21f7eb35de16f37b1c8670650.png)
    The details of the message are as follows:
   ![](https://main.qcloudimg.com/raw/06cdc6450beefae7f6cc6f3d704390a0.png)
