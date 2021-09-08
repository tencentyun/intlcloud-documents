## Overview
Apache Flink is a framework and distributed processing engine for stateful computations over unbounded and bounded data streams. Flink has been designed to run in all common cluster environments, perform computations at in-memory speed and at any scale.

![](https://main.qcloudimg.com/raw/380cf6c9a57a9e645b12f94f1bcaf94c.png)

Apache Flink excels at processing unbounded and bounded data sets. Precise control of time and state enable Flink’s runtime to run any kind of application on unbounded streams. Bounded streams are internally processed by algorithms and data structures that are specifically designed for fixed sized data sets, yielding excellent performance.

Apache Flink requires real-time data from various sources (such as Apache Kafka or Kinesis) in order to execute applications. Flink provides special Kafka Connectors for reading and writing data from/to Kafka topics, which offers exactly-once processing semantics.

## Directions

### Step 1. Get the CKafka instance access address

1. Log in to the [CKafka Console](https://console.cloud.tencent.com/ckafka).
2. Select **Instance List** on the left sidebar and click the **ID** of the target instance to enter its basic information page.
3. On the instance’s basic information page, get the instance access address in the **Access Mode** module, which is the `bootstrap-server` required by production and consumption.
    ![](https://main.qcloudimg.com/raw/7fcec9cfd92d8c0a4284fbd6b76aaaa5.png)

### Step 2. Create a topic

1. On the instance’s basic information page, select the **Topic Management** tab on the top.
2. On the topic management page, click **Create** to create a topic named `test`. This topic is used as an example below to describe how to consume messages.
    ![](https://main.qcloudimg.com/raw/d1fc3abed304203b83c0a8e94e7cc6a7.png)

### Step 3. Add Maven dependencies

Configure `pom.xml` as follows:
<dx-codeblock>
:::  java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.example</groupId>
    <artifactId>Test-CKafka</artifactId>
    <version>1.0-SNAPSHOT</version>
    <dependencies>
        <dependency>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka-clients</artifactId>
            <version>0.10.2.2</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>1.7.25</version>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-java</artifactId>
            <version>1.6.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-streaming-java_2.11</artifactId>
            <version>1.6.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.flink</groupId>
            <artifactId>flink-connector-kafka_2.11</artifactId>
            <version>1.7.0</version>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
:::
</dx-codeblock>


### Step 4. Consume CKafka messages

You can click on the following page to view the two methods of message consumption and view consumption results in the console or printed logs.
<dx-tabs>
:::  Consume via VPC
<dx-codeblock>
:::  java
import org.apache.flink.api.common.serialization.SimpleStringSchema;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.streaming.connectors.kafka.FlinkKafkaConsumer;
import java.util.Properties;

public class CKafkaConsumerDemo {
		public static void main(String args[]) throws Exception {
				StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
				Properties properties = new Properties();
				//Domain name address for public network access, i.e., public routing address, can be obtained in the access mode module of the instance details page.
				properties.setProperty("bootstrap.servers", "IP:PORT");
				//Consumer ID.
				properties.setProperty("group.id", "testConsumerGroup");
				DataStream<String> stream = env
								.addSource(new FlinkKafkaConsumer<>("topicName", new SimpleStringSchema(), properties));
				stream.print();
				env.execute();
		}
}
:::
</dx-codeblock>
:::
::: Consume via public domain name
<dx-codeblock>
:::  java
import org.apache.flink.api.common.serialization.SimpleStringSchema;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.streaming.connectors.kafka.FlinkKafkaConsumer;
import java.util.Properties;

public class CKafkaConsumerDemo {
		public static void main(String args[]) throws Exception {
				StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
				Properties properties = new Properties();
				//Domain name address for public network access, i.e., public routing address, can be obtained in the access mode area of the instance details page.
				properties.setProperty("bootstrap.servers", "IP:PORT");
				//Consumer ID.
				properties.setProperty("group.id", "testConsumerGroup");
				properties.setProperty("security.protocol", "SASL_PLAINTEXT");
				properties.setProperty("sasl.mechanism", "PLAIN");
				//User name and password. Note: the user name is not the one on the console, but concatenated as the “instanceId#username” instead.
				properties.setProperty("sasl.jaas.config", 
															 "org.apache.kafka.common.security.plain.PlainLoginModule required\nusername=\"yourinstanceId#yourusername\"\npassword=\"yourpassword\";");
				properties.setProperty("sasl.kerberos.service.name","kafka");
				DataStream<String> stream = env
								.addSource(new FlinkKafkaConsumer<>("topicName", new SimpleStringSchema(), properties));
				stream.print();
				env.execute();
		}
}
:::
</dx-codeblock>

:::
</dx-tabs>



