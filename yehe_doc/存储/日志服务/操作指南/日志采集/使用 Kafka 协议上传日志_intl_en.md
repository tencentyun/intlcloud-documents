CLS allows you to upload logs to CLS by using Kafka Producer SDKs or other Kafka related agents.

## Overview

Using Kafka as a message pipeline is common in log applications. First, the open source collection client or the producer on the machine directly writes logs to be collected, and then provides them to the downstream, such as Spark and Flink, for consumption through the Kafka message pipeline. CLS has complete upstream and downstream capabilities of the Kafka message pipeline. The following describes the scenarios suitable for you to upload logs using the Kafka protocol. For more Kafka protocol consumption scenarios, see [Kafka Real-time Consumption](https://intl.cloud.tencent.com/document/product/614/47570).

- **Scenario 1**: You already have a self-built system based on open source collection and you do not want complex secondary modifications. Then you can upload logs to CLS by modifying configuration files.
For example, if you have set up a log system using ELK, now you only need to modify the Filebeat or Logstash configuration file to configure the output destination (see [Filebeat configuration](#filebeat)) to CLS to implement convenient and simple log upload to CLS.
- **Scenario 2**: If you want to use Kafka producers to collect and upload logs, you do not need to install collection agents.
CLS allows you to use various Kafka producer SDKs to collect logs and upload the logs to CLS via the Kafka protocol. For more information, see [SDK call examples](#SDKSample) in this document.


## Use Limits

- Supported Kafka protocol versions: 0.11.0.X, 1.0.X, 1.1.X, 2.0.X, 2.1.X, 2.2.X, 2.3.X, 2.4.X, 2.5.X, 2.6.X, 2.7.X, 2.8.X
- Supported compression modes: Gzip, Snappy, LZ4
- Current authentication mode: SASL_PLAINTEXT
- Upload over Kafka requires the `RealtimeProducer` permission. For more information, see [Access Policy Templates](https://intl.cloud.tencent.com/document/product/614/45004).


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
#### Filebeat/Winlogbeat configuration

```filebeat
output.kafka:
  enabled: true
  hosts: ["${region}-producer.cls.tencentyun.com:9095"] # TODO: Service address. The public network port is 9096, and the private network port is 9095.
  topic: "${topicID}" #  TODO: Topic ID
  version: "0.11.0.2"
  compression: "${compress}"   # Configure the compression method. Valid values: `gzip`, `snappy`, `lz4`.
  username: "${logsetID}"
  password: "${SecurityId}#${SecurityKey}"
```

<span id="logstash"></span>
#### Logstash example

```logstash
output {
  kafka {
    topic_id => "${topicID}"
    bootstrap_servers => "${region}-producer.cls.tencentyun.com:${port}"
    sasl_mechanism => "PLAIN"
    security_protocol => "SASL_PLAINTEXT"
    compression_type => "${compress}"
    sasl_jaas_config => "org.apache.kafka.common.security.plain.PlainLoginModule required username='${logsetID}' password='${securityID}#${securityKEY}';"
  }
}
```

<span id="SDKSample"></span>
### SDK call examples

#### Golang SDK call example

```golang
import (
    "fmt"
    "github.com/Shopify/sarama"
)

func main(){
    config := sarama.NewConfig()

    config.Net.SASL.Mechanism = "PLAIN"
    config.Net.SASL.Version = int16(1)
    config.Net.SASL.Enable = true
    config.Net.SASL.User = "${logsetID}"                        // TODO: Logset ID
    config.Net.SASL.Password = "${SecurityId}#${SecurityKey}"   // TODO: Format: ${SecurityId}#${SecurityKey}
    config.Producer.Return.Successes = true
    config.Producer.RequiredAcks = ${acks}                      // TODO: Select the acks value according to the use case
    config.Version = sarama.V1_1_0_0
    config.Producer.Compression = ${compress}                   // TODO: Configuration compression mode

    // TODO: Service address. The public network port is 9096, and the private network port is 9095.
    producer, err := sarama.NewSyncProducer([]string{"${region}-producer.cls.tencentyun.com:9095"}, config)
    if err != nil{
        panic(err)
    }

    msg := &sarama.ProducerMessage{
        Topic: "${topicID}", // TODO: Topic ID
        Value: sarama.StringEncoder("goland sdk sender demo"),
    }
    // Send the messages
    for i := 0; i <= 5; i++ {
        partition, offset, err := producer.SendMessage(msg)
        if err != nil{
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
        # TODO: Service address. The public network port is 9096, and the private network port is 9095.
        bootstrap_servers=["${region}-producer.cls.tencentyun.com:9095"],
        security_protocol='SASL_PLAINTEXT',
        sasl_mechanism='PLAIN',
        # TODO: Logset ID
        sasl_plain_username='${logsetID}',
        # TODO: Format: ${SecurityId}#${SecurityKey}
        sasl_plain_password='${SecurityId}#${SecurityKey}',
        api_version=(0, 11, 0),
        # TODO: Configuration compression mode
        compression_type="${compress_type}",
    )

    for i in range(0, 5):
        # TODO: Topic ID of the sent message
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
        // TODO: In use
        props.put("bootstrap.servers", "${region}-producer.cls.tencentyun.com:9095");
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

#### SDK for C call example

```
// https://github.com/edenhill/librdkafka - master
#include <iostream>
#include <librdkafka/rdkafka.h>
#include <string>
#include <unistd.h>

#define BOOTSTRAP_SERVER "${region}-producer.cls.tencentyun.com:${port}"
#define USERNAME "${logsetID}"
#define PASSWORD "${SecurityId}#${SecurityKey}"
#define TOPIC "${topicID}"
#define ACKS "${acks}"
#define COMPRESS_TYPE "${compress_type}"

static void dr_msg_cb(rd_kafka_t *rk, const rd_kafka_message_t *rkmessage, void *opaque) {
    if (rkmessage->err) {
        fprintf(stdout, "%% Message delivery failed : %s\n", rd_kafka_err2str(rkmessage->err));
    } else {
        fprintf(stdout, "%% Message delivery successful %zu:%d\n", rkmessage->len, rkmessage->partition);
    }
}

int main(int argc, char **argv) {
    // 1. Initialize the configuration.
    rd_kafka_conf_t *conf = rd_kafka_conf_new();

    rd_kafka_conf_set_dr_msg_cb(conf, dr_msg_cb);

    char errstr[512];
    if (rd_kafka_conf_set(conf, "bootstrap.servers", BOOTSTRAP_SERVER, errstr, sizeof(errstr)) != RD_KAFKA_CONF_OK) {
        rd_kafka_conf_destroy(conf);
        fprintf(stdout, "%s\n", errstr);
        return -1;
    }

    if (rd_kafka_conf_set(conf, "acks", ACKS, errstr, sizeof(errstr)) != RD_KAFKA_CONF_OK) {
        rd_kafka_conf_destroy(conf);
        fprintf(stdout, "%s\n", errstr);
        return -1;
    }

    if (rd_kafka_conf_set(conf, "compression.codec", COMPRESS_TYPE, errstr, sizeof(errstr)) != RD_KAFKA_CONF_OK) {
        rd_kafka_conf_destroy(conf);
        fprintf(stdout, "%s\n", errstr);
        return -1;
    }

    // Set the authentication method.
    if (rd_kafka_conf_set(conf, "security.protocol", "sasl_plaintext", errstr, sizeof(errstr)) != RD_KAFKA_CONF_OK) {
        rd_kafka_conf_destroy(conf);
        fprintf(stdout, "%s\n", errstr);
        return -1;
    }
    if (rd_kafka_conf_set(conf, "sasl.mechanisms", "PLAIN", errstr, sizeof(errstr)) != RD_KAFKA_CONF_OK) {
        rd_kafka_conf_destroy(conf);
        fprintf(stdout, "%s\n", errstr);
        return -1;
    }
    if (rd_kafka_conf_set(conf, "sasl.username", USERNAME, errstr, sizeof(errstr)) != RD_KAFKA_CONF_OK) {
        rd_kafka_conf_destroy(conf);
        fprintf(stdout, "%s\n", errstr);
        return -1;

    }
    if (rd_kafka_conf_set(conf, "sasl.password", PASSWORD, errstr, sizeof(errstr)) != RD_KAFKA_CONF_OK) {
        rd_kafka_conf_destroy(conf);
        fprintf(stdout, "%s\n", errstr);
        return -1;
    }

    // 2. Create a handler.
    rd_kafka_t *rk = rd_kafka_new(RD_KAFKA_PRODUCER, conf, errstr, sizeof(errstr));
    if (!rk) {
        rd_kafka_conf_destroy(conf);
        fprintf(stdout, "create produce handler failed: %s\n", errstr);
        return -1;
    }

    // 3. Send data.
    std::string value = "test lib kafka ---- ";
    for (int i = 0; i < 100; ++i) {
        retry:
        rd_kafka_resp_err_t err = rd_kafka_producev(
                rk, RD_KAFKA_V_TOPIC(TOPIC),
                RD_KAFKA_V_MSGFLAGS(RD_KAFKA_MSG_F_COPY),
                RD_KAFKA_V_VALUE((void *) value.c_str(), value.size()),
                RD_KAFKA_V_OPAQUE(nullptr), RD_KAFKA_V_END);

        if (err) {
            fprintf(stdout, "Failed to produce to topic : %s, error : %s", TOPIC, rd_kafka_err2str(err));
            if (err == RD_KAFKA_RESP_ERR__QUEUE_FULL) {
                rd_kafka_poll(rk, 1000);
                goto retry;
            }
        } else {
            fprintf(stdout, "send message to topic successful : %s\n", TOPIC);
        }

        rd_kafka_poll(rk, 0);
    }

    std::cout << "message flush final" << std::endl;
    rd_kafka_flush(rk, 10 * 1000);

    if (rd_kafka_outq_len(rk) > 0) {
        fprintf(stdout, "%d message were not deliverer\n", rd_kafka_outq_len(rk));
    }

    rd_kafka_destroy(rk);

    return 0;
}

```

#### SDK for C# call example

```
/*
 * This demo only provides the easiest way of using the feature. The specific production needs to be implemented in combination with the call method.
 * During use, the TODO items in the demo need to be replaced with actual values.
 *
 * Notes:
 *  1. This demo is verified based on Confluent.Kafka 1.8.2.
 *  2. The maximum value of `MessageMaxBytes` cannot exceed 5 MB.
 *  3. This demo adopts the sync mode for production. You can change to the async mode during use based on your business scenario.
 *  4. You can adjust other parameters during use as instructed at https://docs.confluent.io/platform/current/clients/confluent-kafka-dotnet/_site/api/Confluent.Kafka.ProducerConfig.html.
 *
 * Confluent.Kafka reference: https://docs.confluent.io/platform/current/clients/confluent-kafka-dotnet/_site/api/Confluent.Kafka.html
 */


using Confluent.Kafka;

namespace Producer
{
    class Producer
    {
        private static void Main(string[] args)
        {
            var config = new ProducerConfig
            {
                // TODO: Domain name. For more information, visit https://intl.cloud.tencent.com/document/product/614/18940. The private network port is 9095, and the public network port is 9096.
                BootstrapServers = "${domain}:${port}", 
                SaslMechanism = SaslMechanism.Plain,
                SaslUsername = "${logsetID}", // TODO: Logset ID of the topic
                SaslPassword = "${SecurityId}#${SecurityKey}", // TODO: UIN key of the topic
                SecurityProtocol = SecurityProtocol.SaslPlaintext,
                Acks         = Acks.None, // TODO: Assign a value based on the actual use case. Valid values: `Acks.None`, `Acks.Leader`, `Acks.All`.
                MessageMaxBytes = 5242880 // TODO: The maximum size of the request message, which cannot exceed 5 MB.
            };

            // deliveryHandler
            Action<DeliveryReport<Null, string>> handler =
                r => Console.WriteLine(!r.Error.IsError ? $"Delivered message to {r.TopicPartitionOffset}" : $"Delivery Error: {r.Error.Reason}");


            using (var produce = new ProducerBuilder<Null, string>(config).Build())
            {
                try
                {
                    // TODO: Test verification code
                    for (var i = 0; i < 100; i++)
                    {
                        // TODO: Replace the log topic ID
                        produce.Produce("${topicID}", new Message<Null, string> { Value = "C# demo value" }, handler);
                    }
                    produce.Flush(TimeSpan.FromSeconds(10));

                }
                catch (ProduceException<Null, string> pe)
                {
                    Console.WriteLine($"send message receiver error : {pe.Error.Reason}");
                }
            }
        }
    }
}

```
