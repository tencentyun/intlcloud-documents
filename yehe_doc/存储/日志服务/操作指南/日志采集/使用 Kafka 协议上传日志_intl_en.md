CLS allows you to upload logs to CLS by using Kafka Producer SDKs or other Kafka related agents.

## Use Cases

Using Kafka as a message pipeline is common in log applications. First, the open source collection client or the producer on the machine directly writes logs to be collected, and then provides them to the downstream, such as Spark and Flink, for consumption through the Kafka message pipeline. CLS has complete upstream and downstream capabilities of the Kafka message pipeline. The following describes the scenarios suitable for you to upload logs using the Kafka protocol. For more Kafka protocol consumption scenarios, please see [Kafka Real-time Consumption](https://intl.cloud.tencent.com/document/product/614/42752).

- **Scenario 1**: You already have a self-built system based on open source collection and you do not want complex secondary modifications. Then you can upload logs to CLS by modifying configuration files.
For example, if you have set up a log system using ELK, now you only need to modify the Filebeat or Logstash configuration file to configure the output destination (see [Filebeat configuration](#filebeat)) to CLS to implement convenient and simple log upload to CLS.
- **Scenario 2**: If you want to use Kafka producers to collect and upload logs, you do not need to install collection agents.
CLS allows you to use various Kafka producer SDKs to collect logs and upload the logs to CLS via the Kafka protocol. For more information, see [SDK call examples](#SDKSample) in this document.


## Use Limits

- Supported Kafka protocol versions: 0.11.0.X, 1.0.X, 1.1.X, 2.0.X, 2.1.X, 2.2.X, 2.3.X, 2.4.X, 2.5.X, 2.6.X, 2.7.X, 2.8.X
- Supported compression modes: Gzip, Snappy, LZ4
- Current authentication mode: SASL_PLAINTEXT


## Configuration Methods

To upload logs via Kafka, you need to set the following parameters:

| Parameter | Description |
|---------|---------|
| LinkType | Currently, SASL_PLAINTEXT is supported. |
| hosts | Address of the initially connected cluster. For more information, see [Service Entries](#hosts). |
| topic | Log topic ID. Example: 76c63473-c496-466b-XXXX-XXXXXXXXXXXX |
| username | Logset ID. Example: 0f8e4b82-8adb-47b1-XXXX-XXXXXXXXXXXX |
| password | Password in the format of `${SecurityId}#${SecurityKey}`. Example: XXXXXXXXXXXXXX#YYYYYYYY |


<span id="hosts"></span>
## Service Entries 

<table>
	<tr><th>Region</th><th>Network Type</th><th>Port Number</th><th>Service Entry</th></tr>
	<tr><td rowspan=2>Guangzhou</td><td>Private network</td><td>9095</td><td>gz-producer.cls.tencentyun.com:<b>9095</b></td></tr>
	<tr><td>Public network</td><td>9096</td><td>gz-producer.cls.tencentcs.com:<b>9096</b></td></tr>
</table>

>! This document uses the Guangzhou region as an example. The private and public domain names are identified by different ports. For other regions, replace the address prefixes. For more information, see [here](https://intl.cloud.tencent.com/document/product/614/18940).
>

## Examples

### Agent call examples

<span id="filebeat"></span>
#### Filebeat configuration

```filebeat
output.kafka:
  enabled: true
  hosts: ["${region}-producer.cls.tencentyun.com:9096"] # TODO: service address. The public network port is 9096, and the private network port is 9095.
  topic: "${topicID}" #  TODO: topic ID
  version: "0.11.0.2"
  compression: "${compress}"   # TODO: configuration compression mode
  username: "${logsetID}"
  password: "${SecurityId}#${SecurityKey}"
```

<span id="SDKSample"></span>
### SDK call examples

#### Golang SDK call example

```golang
import (
    "fmt"
    "github.com/Shopify/sarama"
)

func main() {
    config := sarama.NewConfig()

    config.Net.SASL.Mechanism = "PLAIN"
    config.Net.SASL.Version = int16(1)
    config.Net.SASL.Enable = true
    config.Net.SASL.User = "${logsetID}"                        // TODO: logset ID
    config.Net.SASL.Password = "${SecurityId}#${SecurityKey}"   // TODO: format ${SecurityId}#${SecurityKey}
    config.Producer.Return.Successes = true
    config.Producer.RequiredAcks = ${acks}                      // TODO: select the acks value according to the use case
    config.Version = sarama.V0_11_0_0
    config.Producer.Compression = ${compress}                   // TODO: configuration compression mode

    // TODO: service address. The public network port is 9096, and the private network port is 9095.
    producer, err := sarama.NewSyncProducer([]string{"${region}-producer.cls.tencentyun.com:9096"}, config)
    if err != nil {
        panic(err)
    }

    msg := &sarama.ProducerMessage{
        Topic: "${topicID}", // TODO: topic ID
        Value: sarama.StringEncoder("goland sdk sender demo"),
    }
    // Send the message
    for i := 0; i <= 5; i++ {
        partition, offset, err := producer.SendMessage(msg)
        if err != nil {
            panic(err)
        }
        fmt.Printf("send response; partition:%d, offset:%d\n", partition, offset)
    }

    _ = producer.Close()

}
```

#### Python SDK call example

```python
from kafka import KafkaProducer

if __name__ == '__main__':
    produce = KafkaProducer(
        # TODO: service address. The public network port is 9096, and the private network port is 9095.
        bootstrap_servers=["${region}-producer.cls.tencentyun.com:9096"],
        security_protocol='SASL_PLAINTEXT',
        sasl_mechanism='PLAIN',
        # TODO: logset ID
        sasl_plain_username='${logsetID}',
        # TODO: format ${SecurityId}#${SecurityKey}
        sasl_plain_password='${SecurityId}#${SecurityKey}',
        api_version=(0, 11, 0),
        # TODO: configuration compression mode
        compression_type="${compress_type}",
    )

    for i in range(0, 5):
        # TODO: topic ID of the sent message
        future = produce.send(topic="${topicID}", value=b'python sdk sender demo')
        result = future.get(timeout=10)
        print(result)
```

#### Java SDK call example

Maven dependencies:
```maven
<dependencies>
  <!--https://mvnrepository.com/artifact/org.apache.kafka/kafka-clients-->
  <dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <version>0.11.0.2</version>
  </dependency>
</dependencies>
```

Sample code:
```java
import org.apache.kafka.clients.producer.*;

import java.util.Properties;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.Future;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.TimeoutException;

public class ProducerDemo {
    public static void main(String[] args) throws InterruptedException, ExecutionException, TimeoutException {
        // 0. Set parameters
        Properties props = new Properties();
        // TODO: in use
        props.put("bootstrap.servers", "${region}-producer.cls.tencentyun.com:9096");
        // TODO: Set the following according to the actual business scenario 
        props.put("acks", ${acks});
        props.put("retries", ${retries});
        props.put("batch.size", ${batch.size});
        props.put("linger.ms", ${linger.ms});
        props.put("buffer.memory", ${buffer.memory});
        props.put(ProducerConfig.COMPRESSION_TYPE_CONFIG, "${compress_type}"); // TODO: configuration compression mode
        props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
        props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

        props.put("security.protocol", "SASL_PLAINTEXT");
        props.put("sasl.mechanism", "PLAIN");
        // TODO: The user name is logsetID, and the password is the combination of securityID and securityKEY: securityID#securityKEY.
        props.put("sasl.jaas.config",
                "org.apache.kafka.common.security.plain.PlainLoginModule required username='${logsetID}' password='${SecurityId}#${SecurityKey}';");

        // 1. Create a producer object.
        Producer<String, String> producer = new KafkaProducer<String, String>(props);
        
        // 2. Call the send method.
        Future<RecordMetadata> meta = producer.send(new ProducerRecord<String, String>("${topicID}", ${message}));
        RecordMetadata recordMetadata = meta.get(${timeout}, TimeUnit.MILLISECONDS);
        System.out.println("offset = " + recordMetadata.offset());

        // 3. Close the producer.
        producer.close();
    }
}
```



