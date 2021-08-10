As an extension of Spark Core, Spark Streaming is used for high-throughput and fault-tolerant processing of continuous data. Currently supported external input sources include Kafka, Flume, HDFS/S3, Kinesis, Twitter, and TCP socket.
![Alt text](https://mc.qcloudimg.com/static/img/b95ad071d2273bde7b9d8b64894c7ce6/111.png)

Spark Streaming abstracts continuous data into a Discretized Stream (DStream), which consists of a series of continuous resilient distributed datasets (RDDs). Each RDD contains data generated at a certain time interval. Processing DStream with functions is actually processing these RDDs.
![Alt text](https://mc.qcloudimg.com/static/img/f6f2869bc18bffc9a8e4e807276dd5a6/222.png)

When Spark Streaming is used as data input for Kafka, the following stable and experimental Kafka versions are supported:

| Kafka Version              | spark-streaming-kafka-0.8 | spark-streaming-kafka-0.10 |
| :------------------------- | :------------------------ | :------------------------- |
| Broker Version             | 0.8.2.1 or higher         | 0.10.0 or higher           |
| API Maturity               | Deprecated                | Stable                     |
| Language Support           | Scala, Java, and Python       | Scala and Java                |
| Receiver DStream           | Yes                       | No                         |
| Direct DStream             | Yes                       | Yes                        |
| SSL / TLS Support          | No                        | Yes                        |
| Offset Commit API          | No                        | Yes                        |
| Dynamic Topic Subscription | No                        | Yes                        |


Currently, CKafka is compatible with version above 0.9. The Kafka dependency of v0.10.2.1 is used in this practice scenario.

In addition, Spark Streaming in EMR also supports direct connection to CKafka. For more information, please see [Integrating Spark Streaming with Ckafka](https://intl.cloud.tencent.com/document/product/1026/31134).

## Directions

### Step 1. Get the CKafka instance access address

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Select **Instance List** on the left sidebar and click the **ID** of an instance to enter the instance basic information page.
3. On the instance basic information page, get the instance access address in the **Access Mode** module, which is the `bootstrap-server` required by production and consumption.
  ![](https://main.qcloudimg.com/raw/ba52c2bbce2f6eb15d43e451aab9cbc9.png)

### Step 2. Create a topic

1. On the instance basic information page, select the **Topic Management** tab on the top.
2. On the topic management page, click **Create** to create a topic named `test`. This topic is used as an example below to describe how to produce and consume messages.
   ![](https://main.qcloudimg.com/raw/80c5ed36c46bf709efc041cc21850632.png)



### Step 3. Prepare the CVM environment

**CentOS 6.8**

| Package  | Version |
| :------- | :-------------- |
| sbt    |   0.13.16 |
| Hadoop | 2.7.3 |
| Spark | 2.1.0 |
| Protobuf | 2.5.0 |
| SSH | Installed on CentOS by default |
|   Java   |  1.8  |

For specific installation steps, please see [Configuring environment](#Configuring-environment).

### Step 4. Connect to CKafka

<dx-tabs>
::: Producing\sMessages\sto\sCKafka\s

The Kafka dependency of v0.10.2.1 is used here.

1. Add dependencies to `build.sbt`:

```scala
name := "Producer Example"
version := "1.0"
scalaVersion := "2.11.8"
libraryDependencies += "org.apache.kafka" % "kafka-clients" % "0.10.2.1"
```

2. Configure `producer_example.scala`:
   <dx-codeblock>
   :::  scala
   import java.util.Properties
   import org.apache.kafka.clients.producer._
   object ProducerExample extends App {
    val  props = new Properties()
    props.put("bootstrap.servers", "172.16.16.12:9092") // Private IP and port in the instance information

    props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer")
    props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer")

    val producer = new KafkaProducer[String, String](props)
    val TOPIC="test"  // Specify the topic to produce to
    for(i<- 1 to 50){
           val record = new ProducerRecord(TOPIC, "key", s"hello $i") // Produce a message whose `key` is "key" and `value` is "hello i"
           producer.send(record)
    }
    val record = new ProducerRecord(TOPIC, "key", "the end "+new java.util.Date)
    producer.send(record)
    producer.close() // Disconnect at the end
   }
   :::
   </dx-codeblock>


For more information on how to use `ProducerRecord`, please see [ProducerRecord](https://kafka.apache.org/0100/javadoc/org/apache/kafka/clients/producer/ProducerRecord.html).

:::

::: Consuming\sMessages\sfrom\sCKafka\s

<span id="build.sbt"></span>

#### DirectStream

1. Add dependencies to `build.sbt`:

```scala
name := "Consumer Example"
version := "1.0"
scalaVersion := "2.11.8"
libraryDependencies += "org.apache.spark" %% "spark-core" % "2.1.0"
libraryDependencies += "org.apache.spark" %% "spark-streaming" % "2.1.0"
libraryDependencies += "org.apache.spark" %% "spark-streaming-kafka-0-10" % "2.1.0"
```

2. Configure `DirectStream_example.scala`:

```scala
import org.apache.kafka.clients.consumer.ConsumerRecord
import org.apache.kafka.common.serialization.StringDeserializer
import org.apache.kafka.common.TopicPartition
import org.apache.spark.streaming.kafka010._
import org.apache.spark.streaming.kafka010.LocationStrategies.PreferConsistent
import org.apache.spark.streaming.kafka010.ConsumerStrategies.Subscribe
import org.apache.spark.streaming.kafka010.KafkaUtils
import org.apache.spark.streaming.kafka010.OffsetRange
import org.apache.spark.streaming.{Seconds, StreamingContext}
import org.apache.spark.SparkConf
import org.apache.spark.SparkContext
import collection.JavaConversions._
import Array._
object Kafka {
    def main(args: Array[String]) {
        val kafkaParams = Map[String, Object](
            "bootstrap.servers" -> "172.16.16.12:9092",
            "key.deserializer" -> classOf[StringDeserializer],
            "value.deserializer" -> classOf[StringDeserializer],
            "group.id" -> "spark_stream_test1",
            "auto.offset.reset" -> "earliest",
            "enable.auto.commit" -> "false"
        )

        val sparkConf = new SparkConf()
        sparkConf.setMaster("local")
        sparkConf.setAppName("Kafka")
        val ssc = new StreamingContext(sparkConf, Seconds(5))
        val topics = Array("spark_test")

        val offsets : Map[TopicPartition, Long] = Map()

        for (i <- 0 until 3){
            val tp = new TopicPartition("spark_test", i)
            offsets.updated(tp , 0L)
        }
        val stream = KafkaUtils.createDirectStream[String, String](
            ssc,
            PreferConsistent,
            Subscribe[String, String](topics, kafkaParams)
        )
        println("directStream")
        stream.foreachRDD{ rdd=>
	        // Output the obtained message
            rdd.foreach{iter =>
                val i = iter.value
                println(s"${i}")
            }
            // Get the offset
            val offsetRanges = rdd.asInstanceOf[HasOffsetRanges].offsetRanges
            rdd.foreachPartition { iter =>
                val o: OffsetRange = offsetRanges(TaskContext.get.partitionId)
                println(s"${o.topic} ${o.partition} ${o.fromOffset} ${o.untilOffset}")
            }
        }

        // Start the computation
        ssc.start()
        ssc.awaitTermination()
    }
}
```


#### RDD

1. Configure `build.sbt` in the way as detailed [here](#build.sbt).
2. Configure `RDD_example`:

```scala
import org.apache.kafka.clients.consumer.ConsumerRecord
import org.apache.kafka.common.serialization.StringDeserializer
import org.apache.spark.streaming.kafka010._
import org.apache.spark.streaming.kafka010.LocationStrategies.PreferConsistent
import org.apache.spark.streaming.kafka010.ConsumerStrategies.Subscribe
import org.apache.spark.streaming.kafka010.KafkaUtils
import org.apache.spark.streaming.kafka010.OffsetRange
import org.apache.spark.streaming.{Seconds, StreamingContext}
import org.apache.spark.SparkConf
import org.apache.spark.SparkContext
import collection.JavaConversions._
import Array._
object Kafka {
    def main(args: Array[String]) {
        val kafkaParams = Map[String, Object](
            "bootstrap.servers" -> "172.16.16.12:9092",
            "key.deserializer" -> classOf[StringDeserializer],
            "value.deserializer" -> classOf[StringDeserializer],
            "group.id" -> "spark_stream",
            "auto.offset.reset" -> "earliest",
            "enable.auto.commit" -> (false: java.lang.Boolean)
        )
        val sc = new SparkContext("local", "Kafka", new SparkConf())
        val java_kafkaParams : java.util.Map[String, Object] = kafkaParams
        // Pull messages in the corresponding offset range from the partition in order. The request will be blocked if no messages can be pulled, until the specified waiting time elapses or the number of produced new messages reaches the number for messages to be pulled
        val offsetRanges = Array[OffsetRange](
            OffsetRange("spark_test", 0, 0, 5),
            OffsetRange("spark_test", 1, 0, 5),
            OffsetRange("spark_test", 2, 0, 5)
        )
        val range = KafkaUtils.createRDD[String, String](
            sc,
            java_kafkaParams,
            offsetRanges,
            PreferConsistent
        )
        range.foreach(rdd=>println(rdd.value))
        sc.stop()
    }
}
```

For more information on how to use `kafkaParams`, please see [kafkaParams](http://kafka.apache.org/documentation.html#newconsumerconfigs).

:::

</dx-tabs>

### Configuring environment[](id:Configuring-environment)

#### Installing sbt

1. Download the sbt package from [sbt's official website](http://www.scala-sbt.org/download.html).
2. After decompression, create an `sbt_run.sh` script with the following content in the sbt directory and add executable permissions:
```bash
#!/bin/bash
SBT_OPTS="-Xms512M -Xmx1536M -Xss1M -XX:+CMSClassUnloadingEnabled -XX:MaxPermSize=256M"
java $SBT_OPTS -jar `dirname $0`/bin/sbt-launch.jar "$@"
```
 ```bash
chmod u+x ./sbt_run.sh
 ```
 
3. Run the following command:
```bash
./sbt-run.sh sbt-version
```

The display of sbt version indicates a successful installation.

#### Installing Protobuf

1. Download an appropriate version of [Protobuf](https://github.com/google/protobuf/releases).
2. Decompress and enter the directory.
```bash
./configure
make && make install
```
 You should install gcc-g++ in advance, and the root permission may be required during installation.

3. Log in again and enter the following on the command line:
```bash
protoc --version
```

4. The display of Protobuf version indicates a successful installation.

#### Installing Hadoop

1. Download the required version at [Hadoop's official website](http://hadoop.apache.org/releases.html).
2. Add a Hadoop user.
```bash
useradd -m hadoop -s /bin/bash
```

3. Grant admin permissions.
```bash
visudo
```

4. Add the following in a new line under `root ALL=(ALL) ALL`:
   `hadoop ALL=(ALL) ALL`
   Save and exit.
5. Use Hadoop for operations.
```bash
su hadoop
```

6. Configure SSH password-free login.
```bash
cd ~/.ssh/                     # If there is no such directory, please run `ssh localhost` first
ssh-keygen -t rsa              # There will be prompts. Simply press Enter
cat id_rsa.pub >> authorized_keys  # Add authorization
chmod 600 ./authorized_keys    # Modify file permission
```

7. Install Java.
```bash
sudo yum install java-1.8.0-openjdk java-1.8.0-openjdk-devel
```

8. Configure `${JAVA_HOME}`.
```bash
vim /etc/profile
```
 Add the following at the end:
```vim
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.121-0.b13.el6_8.x86_64/jre
export PATH=$PATH:$JAVA_HOME
```
 Modify the corresponding path based on the installation information.

9. Decompress Hadoop and enter the directory.
```bash
./bin/hadoop version
```
 The display of version information indicates a successful installation.

10. Configure the pseudo-distributed mode (so that you can build different forms of clusters as needed).
```bash
vim /etc/profile
```
 Add the following at the end:
```vim
export HADOOP_HOME=/usr/local/hadoop
export PATH=$HADOOP_HOME/bin:$PATH
```
 Modify the corresponding path based on the installation information.

11. Modify `/etc/hadoop/core-site.xml`.
<dx-codeblock>
:::  xml
<configuration>    
	<property>       
		<name>hadoop.tmp.dir</name>       
		<value>file:/usr/local/hadoop/tmp</value>
		<description>Abase for other temporary directories.</description>
	</property>    
	<property>        
		<name>fs.defaultFS</name>
		<value>hdfs://localhost:9000</value> 
	</property>
</configuration>
:::
</dx-codeblock>


12. Modify `/etc/hadoop/hdfs-site.xml`.
<dx-codeblock>
:::  xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/usr/local/hadoop/tmp/dfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/usr/local/hadoop/tmp/dfs/data</value>
    </property>
</configuration>
:::
</dx-codeblock>


13. Change `JAVA_HOME` in `/etc/hadoop/hadoop-env.sh` to the Java path.
```vim
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.121-0.b13.el6_8.x86_64/jre
```

14. Format the NameNode.
```bash
./bin/hdfs namenode -format
```
 The display of `Exitting with status 0` indicates a success.

15. Start Hadoop.
```bash
./sbin/start-dfs.sh
```
`NameNode`, `DataNode`, and `SecondaryNameNode` processes will exist upon successful startup.

#### Installing Spark

Download the required version at [Spark's official website](http://spark.apache.org/downloads.html).
As Hadoop has already been installed, select *Pre-build with user-provided Apache Hadoop* here.
>?This example also uses the `hadoop` user for operations.

1. Decompress and enter the directory.
2. Modify the configuration file.
```bash
cp ./conf/spark-env.sh.template ./conf/spark-env.sh
vim ./conf/spark-env.sh
```
 Add the following in the first line:
```vim
export SPARK_DIST_CLASSPATH=$(/usr/local/hadoop/bin/hadoop classpath)
```
 Modify the path based on the Hadoop installation information.

3. Run the example.
```bash
bin/run-example SparkPi
```

 The display of an approximate value of `π` output by the program indicates a successful installation.

