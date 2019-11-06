## Operation Scenarios
This task guides you through how to use the Kafka API after purchasing the CKafka service. After building a CKafka environment on an CVM instance, you need to download and decompress the Kafka toolkit and perform simple testing on the Kafka API.

## Prerequisites
- You have already [registered a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).
- You have already [purchased an CVM instance](https://buy.cloud.tencent.com/cvm).

## Directions
### 1. Install the JDK environment
You need to log in to the CVM purchase page to [purchase a CVM instance](https://buy.cloud.tencent.com/cvm) first. The instance is configured as follows for this test:
- OS: CentOS 6.8 64-bit 
- CPU: 1 core 
- Memory: 2 GB 
- Public network bandwidth: 1 Mbps 

After the purchase, install the JDK to the CVM instance by following the steps below:

**1.1 Download the JDK**
The JDK can be obtained with the `wget` command. If you need a different version, go to the official website to download one.
You are recommended to use a JDK version above 1.7. The version used in this example is JDK 1.7.0_79.

**1.2 Move it to a folder and decompress it**
```
mkdir /usr/local/jdk
mv jdk-7u79-linux-x64.tar.gz /usr/local/jdk/
cd /usr/local/jdk/
tar -xzvf jdk-7u79-linux-x64.tar.gz
```
**1.3 Configure the environment variable**
```
vim /etc/profile
```
Add the following environment variable configuration to the end of the file:
```
export JAVA_HOME=/usr/local/jdk/jdk1.7.0_79 (extracted JDK folder)  
export JRE_HOME=/usr/local/jdk/jdk1.7.0_79/jre
export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH  
export CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JRE_HOME/lib
```
Run `wq` to save and exit. Then, run `source /etc/profile` to make the file take effect immediately.

**1.4 Verify**
Verify whether the environment has been installed successfully by running the following command (or the `javac` command) and checking whether the version numbers are the same:
```
cd  $JAVA_HOME/bin
./java  -version
```
> ? `$JAVA_HOME` is the home directory of the installed JDK.

If the following codes appear, the JDK has been installed successfully.
![](https://mc.qcloudimg.com/static/img/859143ff8986b24e80b3a9c3b31bd511/4.png)

### 2. Download the Kafka toolkit
>!
> - The `$ip $port` variable mentioned below refers to the access IP and port of CKafka.
> - A CKafka instance offers up to 6 access points (i.e., $ip $port) which can satisfy the access requests from clients in different network environments. When performing a test, you only need to select the access point corresponding to the specific network environment. For example, if your CVM instance runs in VPC, you can just select the CKafka access point ($ip $port) for VPC. For more information on access points, see the instance details page.

Download the Kafka installation package [here](http://kafka.apache.org/downloads) and decompress it.
Currently, CKafka is 100% compatible with Kafka 0.9 and 0.10. You are recommended to download the installation package on an appropriate version (preferably v0.10.2).

```
tar -C /opt -xzvf kafka_2.10-0.10.2.0.tgz    // Decompressed to the corresponding directory
```

Kafka is ready for use immediately after decompression with no environment configuration required.
You can test whether the CVM instance is connected to the CKafka instance by running the `telnet` command.
```
telnet $ip $port
```
![](https://mc.qcloudimg.com/static/img/c30a8d0e2fe57c109d3f7f1fa55b107f/5.png)

### 3. Test the Kafka API

**Send a message:**
```
./kafka-console-producer.sh --broker-list $ip:$port --topic topicName
This is a message
This is another message
```
Here, the IP in the broker-list is the VIP of the CKafka instance, and topicName is the topic name in the CKafka instance.

**Receive a message (CKafka hides the ZooKeeper cluster by default):**
```
./kafka-console-consumer.sh --bootstrap-server $ip:$port --from-beginning --new-consumer --topic topicName
This is a message
This is another message
```
In the above command, as no consumer group is specified to consume messages, the system will randomly generate a group to consume messages, and the upper limit on group quantity may be reached quickly. Therefore, you are recommended to **specify a group** to receive messages. First, you need to configure the specified group name in `consumer.properties`, as shown below:
![](https://main.qcloudimg.com/raw/7ec8a2311776ac360ba0f4c18703fd8b.jpg)

Then, run the following command to specify the consumer group:
```
./kafka-console-consumer.sh --bootstrap-server $ip:$port --from-beginning --new-consumer --topic topicName --consumer.config ../config/consumer.properties
```
> ?When configuring the `ConsumerConfig` parameter, you are recommended to set `auto.offset.reset` to `earliest` so as to prevent messages from being skipped when a new consumer group does not exist. 
Cause: When you create a consumer which falls into a new group and the `auto.offset.reset` value is `latest`, latest data (i.e., data produced after creating the consumer) will be consumed, while data previously produced will not be consumed.

View the corresponding CKafka monitor:
![](https://main.qcloudimg.com/raw/0f958700c2ce2fa1654269f918660584.png)
