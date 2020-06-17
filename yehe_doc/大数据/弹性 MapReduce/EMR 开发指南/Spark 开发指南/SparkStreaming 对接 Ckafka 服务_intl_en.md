Tencent Cloud Elastic MapReduce (EMR) allows you to realize the following streaming applications with CKafka:
- Log information stream processing
- User behavior record stream processing
- Alarm information collection and processing
- Messaging

## 1. Preparations for Development
- This job is required to access to CKafka, so you need to create a CKafka instance first. For more information, please see [CKafka](https://intl.cloud.tencent.com/product/CKafka).
- Confirm that you have activated Tencent Cloud and created an EMR cluster. When creating the EMR cluster, select the Spark component on the software configuration page.

## 2. Using Kafka Toolkit in EMR Cluster
First, you need to check the private IP and port number of CKafka. Log in to the CKafka Console, select the CKafka instance you want to use, and view its private IP as $kafkaIP in the basic information section, and the port number is generally defaulted to 9092. Create a topic named spark_streaming_test on the topic management page.

Log in to any node (preferably a master one) in the EMR cluster. For more information on how to log in to EMR, please see [Logging in to Linux Instances](https://intl.cloud.tencent.com/document/product/213/5436). Here, you can choose to log in with WebShell. Click "Log in" on the right of the desired CVM instance to enter the login page. The default username is `root`, and the password is the one you set when creating the EMR cluster. Once the correct credentials are entered, you can enter the command line interface.

Run the following command in EMR command-line interface to switch to the Hadoop user and go to the directory `/usr/local/service/spark`:
```
[root@172 ~]# su hadoop
[root@172 root]$ cd / usr/local/service/spark
```

Download the installation package [Kafka's official website](http://kafka.apache.org/downloads). A Kafka client is recommended as it is most compatible with Tencent Cloud CKafka. Then, Decompress the package and move the extracted folder to the `/opt` directory:
```
[hadoop@172 data]$ tar -xzvf kafka_2.10-0.10.2.0.tgz
[hadoop@172 data]$ mv kafka_2.10-0.10.2.0 /opt/
```
Once the package is decompressed, you can use Kafka. Run the `telnet` command to see whether the EMR cluster is connected to the CKafka instance:
```
[hadoop@172 kafka_2.10-0.10.2.0]$ telnet $kafkaIP 9092
Trying $kafkaIP...
Connected to $kafkaIP.
```

$kafkaIP is the private IP address of the CKafka instance you created.
The following example describes how to test the Kafka toolkit. Log in to the EMR cluster in two WebShell terminals, switch to the Hadoop user, and go to the Kafka installation path:
```
[root@172 ~]# su hadoop
[hadoop@172 root]$ cd /opt/kafka_2.10-0.10.2.0/
```
Connect to CKafka on the first terminal and send the following message:
```
[hadoop@172 kafka_2.10-0.10.2.0]$ bin/kafka-console-producer.sh --broker-list $kafkaIP:9092 
--topic spark_streaming_test
hello world
this is a message
```
Connect to CKafka on the other terminal. Now, as a consumer, you are able to access or consume records from a Kafka cluster:
```
[hadoop@172 kafka_2.10-0.10.2.0]$ bin/kafka-console-consumer.sh --bootstrap-server 
$kafkaIP:9092 --from-beginning --new-consumer --topic spark_streaming_test
hello world
this is a message
```

## 3. Connecting Spark Streaming to CKafka
On the consumer side, Spark Streaming is used to continuously pull data from CKafka for word frequency counting, i.e. performing the WordCount job on the streaming data. On the producer side, a program is used to constantly generate data which is continuously delivered to CKafka.
[Download and install Maven](http://maven.apache.org/download.cgi) first and then configure its environment variables. If you are using IDE, please configure Maven-related items in your IDE.

### Creating a Spark Streaming consumer project
Enter the directory for your Maven project, such as `D://mavenWorkplace`, by running the following commands:
```
mvn   archetype:generate   -DgroupId=$yourgroupID   -DartifactId=$yourartifactID 
-DarchetypeArtifactId=maven-archetype-quickstart
```
Here, $yourgroupID is your package name, $yourartifactID is your project name, and maven-archetype-quickstart indicates to create a Maven Java project. Some files need to be downloaded during the process, so please keep the Internet connected.
After successfully creating the project, you will see a folder named $yourartifactID in the `D://mavenWorkplace` directory. The files included in the folder have the following structure:
```
simple
　　　---pom.xml　　　　Core configuration, under the project root directory
　　　---src
　　　　　---main　　　　　　
　　　　　　　---java　　　　  Java source code directory
　　      　---resources　  Java configuration file directory
　　　　---test
　　　　　　---java　　　　  Test source code directory
　　　　　　---resources　  Test configuration directory
```
Among the files above, pay extra attention to the pom.xml file and the Java folder under the main directory. The pom.xml file is primarily used to create dependencies and package configurations; the Java folder is used to store your source code.

First, add the Maven dependencies to the pom.xml file:
```
<dependencies>
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-core_2.11</artifactId>
            <version>2.0.2</version>
        </dependency>
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-streaming_2.11</artifactId>
            <version>2.0.2</version>
        </dependency>
        <dependency>
            <groupId>org.apache.spark</groupId>
            <artifactId>spark-streaming-kafka-0-10_2.11</artifactId>
            <version>2.0.2</version>
        </dependency>
</dependencies>
```
Then, add the packaging and compiling plugins to the pom.xml file:
```
<build>
<plugins>
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
      <source>1.8</source>
      <target>1.8</target>
      <encoding>utf-8</encoding>
    </configuration>
  </plugin>
  <plugin>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
      <descriptorRefs>
      <descriptorRef>jar-with-dependencies</descriptorRef>
      </descriptorRefs>
    </configuration>
    <executions>
      <execution>
        <id>make-assembly</id>
        <phase>package</phase>
        <goals>
          <goal>single</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
</plugins>
</build>
```
>Replace $yourgroupID and $yourartifactID with your real information.

Then, add the sample code by creating a Java Class named KafkaTest.java in the main>Java folder and adding the following code to it:
```
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.spark.SparkConf;
import org.apache.spark.api.java.JavaSparkContext;
import org.apache.spark.streaming.Durations;
import org.apache.spark.streaming.api.java.JavaInputDStream;
import org.apache.spark.streaming.api.java.JavaPairDStream;
import org.apache.spark.streaming.api.java.JavaStreamingContext;
import org.apache.spark.streaming.kafka010.ConsumerStrategies;
import org.apache.spark.streaming.kafka010.KafkaUtils;
import org.apache.spark.streaming.kafka010.LocationStrategies;
import scala.Tuple2;

import java.util.*;
import java.util.concurrent.TimeUnit;

/**
 * Created by tencent on 2018/7/3.
 */
public class KafkaTest {
    public static void main(String[] args) throws InterruptedException {
        String brokers = "$kafkaIP:9092";
        String topics = "spark_streaming_test1";  // Subscribed topics; multiple topics should be separated by ','
        int durationSeconds = 60;  // Interval
        SparkConf conf = new SparkConf().setAppName("spark streaming word count");
        JavaSparkContext sc = new JavaSparkContext(conf);
        JavaStreamingContext ssc = new JavaStreamingContext(sc, Durations.seconds(durationSeconds));
        Collection<String> topicsSet = new HashSet<>(Arrays.asList(topics.split(",")));
        // Kafka-related parameter
        Map<String, Object> kafkaParams = new HashMap<>();
        kafkaParams.put("metadata.broker.list", brokers) ;
        kafkaParams.put("bootstrap.servers", brokers);
        kafkaParams.put("group.id", "group1");
        kafkaParams.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        kafkaParams.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        kafkaParams.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
        // Create a connection
        JavaInputDStream<ConsumerRecord<Object,Object>> lines = KafkaUtils.createDirectStream(
                ssc,
                LocationStrategies.PreferConsistent(),
                ConsumerStrategies.Subscribe(topicsSet, kafkaParams)
        );
        // wordcount logic
        JavaPairDStream<String, Integer> counts = lines
                .flatMap(x -> Arrays.asList(x.value().toString().split(" ")).iterator())
                .mapToPair(x -> new Tuple2<String, Integer>(x, 1))
                .reduceByKey((x, y) -> x + y);
        // Save the result
        counts.dstream().saveAsTextFiles("$hdfsPath","result");
//
        ssc.start();
        ssc.awaitTermination();
        ssc.close();
    }
}
```
Pay attention to the following settings in the code:
- The brokers variable should be set to the private IP of the CKafka instance found in step 2;
- The topics variable should be set to the name of the topic you created, e.g., spark_streaming_test1 here;
- durationSeconds is the interval for the program to consume the data in CKafka, e.g., 60 seconds here;
- $hdfsPath is the path in HDFS to which the result will be output.

Use the local command prompt to enter the project directory and run the following command to compile and package the project:
```
mvn package
```
"Build success" indicates that package is successfully created. You can see the generated .jar package in the target folder under the project directory.
Upload the package file to the EMR cluster with the scp or sftp tool. Be sure to include the dependencies in the .jar package to be uploaded:
```
scp $localfile root@public IP address:$remotefolder
```
Here, $localfile is the path and the name of your local file; root is the CVM instance username. You can look up the public IP address in the node information in the EMR or CVM Console. $remotefolder is the path where you want to store the file in the CVM instance. After the upload is completed, you can check whether the file is in the corresponding folder on the EMR command line.

### Creating a Spark Streaming producer project
Enter the directory for your Maven project, such as `D://mavenWorkplace`, by running the following commands:
```
mvn archetype:generate -DgroupId=$yourgroupID -DartifactId=$yourartifactID 
-DarchetypeArtifactId=maven-archetype-quickstart
```
First, add the Maven dependencies to the pom.xml file:
```
<dependencies>
        <dependency>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka_2.11</artifactId>
            <version>0.10.1.0</version>
        </dependency>
        <dependency>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka-clients</artifactId>
            <version>0.10.1.0</version>
        </dependency>
        <dependency>
            <groupId>org.apache.kafka</groupId>
            <artifactId>kafka-streams</artifactId>
            <version>0.10.1.0</version>
        </dependency>
    </dependencies>
```
Then, add the packaging and compiling plugins to the pom.xml file:
```
<build>
<plugins>
  <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
      <source>1.8</source>
      <target>1.8</target>
      <encoding>utf-8</encoding>
    </configuration>
  </plugin>
  <plugin>
    <artifactId>maven-assembly-plugin</artifactId>
    <configuration>
      <descriptorRefs>
      <descriptorRef>jar-with-dependencies</descriptorRef>
      </descriptorRefs>
    </configuration>
    <executions>
      <execution>
        <id>make-assembly</id>
        <phase>package</phase>
        <goals>
          <goal>single</goal>
        </goals>
      </execution>
    </executions>
  </plugin>
</plugins>
</build>
```
>Replace $yourgroupID and $yourartifactID with your real information.

Then, add the sample code by creating a Java Class named SendData.java in the main>Java folder and adding the following code to it:
```
import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.ProducerRecord;
import java.util.Properties;


/**
 * Created by tencent on 2018/7/4.
 */
public class SendData {
    public static void main(String[] args) {

        Properties props = new Properties();
        props.put("bootstrap.servers", "$kafkaIP:9092");
        props.put("acks", "all");
        props.put("retries", 0);
        props.put("batch.size", 16384);
        props.put("linger.ms", 1);
        props.put("buffer.memory", 33554432);
        props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        // The producer sends a message
        String topic = "spark_streaming_test1";
        org.apache.kafka.clients.producer.Producer<String, String> procuder = new KafkaProducer<String,String>(props);
        while(true){
            int num = (int)((Math.random())*10);
            for (int i = 0; i <= 10; i++) {
                int tmp = (num+i)%10;
                String value = "value_" + tmp;
                ProducerRecord<String, String> msg = new ProducerRecord<String, String>(topic, value);
                procuder.send(msg);
            }

            try {Thread.sleep(1000*10);}
            catch (InterruptedException e) {}
        }
    }
}
```
**Replace $kafkaIP with the private IP address of your CKafka instance.**

This program sends 10 messages from value_0 to value_9 to CKafka every 10 seconds, starting at a random order. For more information on the parameters in the program, please see the consumer program.
Use the local command prompt to enter the project directory and run the following command to compile and package the project:
```
mvn package
```

"Build success" indicates that package is successfully created. You can see the generated .jar package in the target folder under the project directory.
Upload the package file to the EMR cluster with the scp or sftp tool. Be sure to include the dependencies in the .jar package to be uploaded:
```
scp $localfile root@public IP address:$remotefolder
```

### Using a program to consume CKafka data
Use two interfaces to log in to the WebShell of the EMR cluster.
**In the first interface**, log in to a master node of the EMR cluster and switch to the Hadoop user, as shown in section 2. Run the following command to run the demo:
```
[hadoop@172 ~]$ bin/spark-submit --class KafkaTest --master yarn-cluster $consumerpackage 
```
The parameters are as follows:
- --class indicates the entry class to be executed, e.g., KafkaTest in this example
- --master is the master URL of the cluster.
- $consumerpackage is the package name of the packaged consumer program.

After the program is started, it will run continuously in the Yarn cluster. Run the following command to view the status of the program running:
```
[hadoop@172 ~]$ yarn application –list
```
**In the second interface**, log in to the WebShell of EMR and run the producer program, so that Spark Streaming can retrieve the data for consumption.
```
[hadoop@172 spark]$ bin/spark-submit --class SendData $producerpackage
```
Here, $producerpackage is the package name of the packaged producer program. The result of the wordcount job will be output to the specified HDFS folder in a while. You can view in HDFS the result of Spark Streaming's consumption of the CKafka data:
```
[hadoop@172 root]$ hdfs dfs -ls /user
Found 9 items
drwxr-xr-x - hadoop supergroup  0 2018-07-03 16:37 /user/hadoop
drwxr-xr-x - hadoop supergroup  0 2018-06-19 10:10 /user/hive
-rw-r--r-- 3 hadoop supergroup 0 2018-06-29 10:19 /user/pythontest.txt
drwxr-xr-x - hadoop supergroup 0 2018-07-05 20:25 /user/sparkstreamingtest-1530793500000.result

[hadoop@172 root]$ hdfs dfs -cat /user/sparkstreamingtest-1530793500000.result/*
(value_6,16)
(value_7,22)
(value_8,18)
(value_0,18)
(value_9,17)
(value_1,18)
(value_2,17)
(value_3,17)
(value_4,16)
(value_5,17)
```
Finally, exit the KafkaTest program in the Yarn cluster:
```
[hadoop@172 ~]$ yarn application –kill $Application-Id
```
Here, $Application-Id is the ID found by running the `yarn application –list` command.
For more information on Kafka, please see the [official documentation](http://kafka.apache.org/).
