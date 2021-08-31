## Overview
This document describes how to configure SASL authentication and ACL rules in the CKafka console to enhance access control in public/private network transfers and permission control in production and consumption of resources such as topic.
>?
>- Kafka offers various security authentication mechanisms, which mainly fall into the SSL and SASL2 categories. Among them, SASL/PLAIN is an authentication method based on account and password and more commonly used. CKafka supports SASL_PLAINTEXT authentication.
>- An access control list (ACL) helps you define a set of permission rules to allow/deny users to read/write topic resources through IPs.


## Directions

### Step 1. Create an instance
Click **Create** on the instance list page to create and purchase an instance. For more information, please see [Creating Instance](https://intl.cloud.tencent.com/document/product/597/32543).


### Step 2. Configure user information
You can configure user information in two ways: client and CKafka instance.

#### Client configuration
1. On the user management page of the CKafka instance, click **Create** to create a user.
![](https://main.qcloudimg.com/raw/b71f3d8399e2169cff962b3bfaeff85e.png)
2. Enter the username and password and click **Submit**.
![](https://main.qcloudimg.com/raw/d50580170b01896f2070eaf58e64fe9d.png)

#### CKafka instance configuration
1. In the configuration file (see the [sample configuration file](#Sample configuration file) below), add the following configuration:
```
sasl.mechanism=PLAIN
security.protocol=SASL_PLAINTEXT
```
2. Configure the username and password:
```
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="instanceId#admin" password="admin";
```
Among them, the username and password in the `sasl.jaas.config` part are described as follows: 
 - username: **it contains the instance ID and username concatenated with a `#`**. The instance ID is the ID of the CKafka instance that the client needs to connect to (which can be viewed in the Tencent Cloud console), and the username can be configured in the **ACL policy management module in the console**.
 - password: it is the password corresponding to the username.

<span id="example"></span>
**Sample configuration file**
- The name of the producer configuration file is `producer.properties`, and `SASL_PLAINTEXT` is configured as follows:
```
sasl.mechanism=PLAIN
security.protocol=SASL_PLAINTEXT
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="INSTANCE-2#admin" password="admin";
```
- The name of the consumer configuration file is `consumer.properties`, and `SASL_PLAINTEXT` is configured as follows:
```
sasl.mechanism=PLAIN
security.protocol=SASL_PLAINTEXT
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="INSTANCE-2#admin" password="admin";
```

### Step 3. Configure an ACL policy
1. On the ACL policy management page, select the topic resource for which to configure a policy and click **Edit ACL Policy** in the **Operation** column.
2. In the ACL policy creation pop-up window, select/enter the target users and IPs. If you don't select any, the policy will take effect for all users/hosts by default.
    Sample ACL policy: allow/deny user to read/write topic resource through IP.
    ![](https://main.qcloudimg.com/raw/442c5f5bc928701cd1684a116d44bded.png)

>?
- Enabling routing only affects the authentication method during access, while the configured ACL policy takes effect globally.
- If you use the PLAINTEXT method to access Kafka while enabling public network access routing, the ACL previously set for the topics will still take effect. If you want PLAINTEXT access to be unaffected, please add the read/write permissions of all users for the topics that PLAINTEXT needs to access.

### Step 4. Test connectivity
#### Kafka's tool script

Write the configuration required by SASL_PLAINTEXT into `producer.properties` (please see the [sample configuration file](#example) for configuration content), and run the following command to produce messages:
```bash
/yourkafka/bin/kafka-console-producer.sh --broker-list yourservers --topic yourtopic --producer.config producer.properties
```
Write the configuration required by SASL_PLAINTEXT into `consumer.properties` (please see the [sample configuration file](#example) for configuration content), and run the following command to consume messages:
```bash
/yourkafka/bin/kafka-console-consumer.sh --bootstrap-server yourservers --from-beginning --new-consumer --topic yourtopic --consumer.config consumer.properties
```

#### Java client
CKafka's server uses a CA-certified certificate, and Java comes with its own root certificate, so there is no need to specify a certificate.
If you use other modes for access, you only need to replace the relevant configuration.
```java
//SASL_PLAINTEXT
Properties props = new Properties();
props.put("bootstrap.servers", "yourbrokers");
props.put("security.protocol", "SASL_PLAINTEXT");
props.put("sasl.mechanism", "PLAIN");
props.put("session.timeout.ms", 30000);
props.put("key.serializer", "org.apache.kafka.common.serialization.IntegerSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("sasl.jaas.config", "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"yourinstance#yourusername\" password=\"yourpassword\";");
org.apache.kafka.clients.producer.KafkaProducer<Integer, String> producer = new org.apache.kafka.clients.producer.KafkaProducer<>(props);


Properties props = new Properties();
props.put("bootstrap.servers", "yourbrokers");
props.put("security.protocol", "SASL_PLAINTEXT");
props.put("sasl.mechanism", "PLAIN");
props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
props.put("session.timeout.ms", 30000)
props.put("sasl.jaas.config", "org.apache.kafka.common.security.plain.PlainLoginModule required username=\"yourinstance#yourusername\" password=\"yourpassword\";");
org.apache.kafka.clients.consumer.KafkaConsumer<Integer, String> consumer = new org.apache.kafka.clients.consumer.KafkaConsumer<>(props);
```

#### Kafka-Python 1.3.5 client
There are some differences between the configuration parameters of Python and Java. The specific configuration methods are as follows:
```python
#ssl_calfile        PEM trust certificate storage path
#                   Because the server's certificate is root certification, it can be downloaded from https://www.digicert.com/digicert-root-certificates.htm
#yourinstance       The CKafka instance to be connected to, which can be viewed in the Tencent Cloud console
#yourusername       It can be set in the ACL module in the console
#yourpassword       Password of the username
#brokers            Domain name or ip:port corresponding to the instance

#SASL_PLAINTEXT:
producer = KafkaProducer (
    bootstrap_servers=brokers,
    ssl_check_hostname=False,
    security_protocol="SASL_PLAINTEXT",
    sasl_mechanism='PLAIN',
    sasl_plain_username='yourinstance#yourusername',
    sasl_plain_password='yourpassword',
    api_version=(0,10,0)
)

consumer = KafkaConsumer (
   'yourtopic',
    auto_offset_reset='earliest',
    bootstrap_servers=brokers,
    security_protocol="SASL_PLAINTEXT",
    sasl_mechanism='PLAIN',
    sasl_plain_username='yourinstance#youruser',
    sasl_plain_password='yourpassword',
    api_version=(0,10,0)
)

#SASL_SSL:
producer = KafkaProducer(
    bootstrap_servers=brokers,
    security_protocol='SASL_SSL',
    ssl_cafile='DigiCertGlobalRootCA.pem',
    ssl_check_hostname=False,
    sasl_mechanism='PLAIN',
    sasl_plain_username='yourinstance#youruser',
    sasl_plain_password='yourpassword',
    api_version=(0,10,0)
)
consumer = KafkaConsumer (
    'yourtopic',
    auto_offset_reset='earliest',
    bootstrap_servers=brokers,
    security_protocol='SASL_SSL',
    ssl_cafile='DigiCertGlobalRootCA.pem',
    ssl_check_hostname=False,
    sasl_mechanism='PLAIN',
    sasl_plain_username='yourinstance#youruser',
    sasl_plain_password='yourpassword',
    api_version=(0,10,0)
)

#SSL:
producer = KafkaProducer(
    bootstrap_servers=brokers,
    client_id='yourinstance#youruser#yourpassword#yourclientid',
    security_protocol='SSL',
    ssl_check_hostname=False,
    ssl_cafile='DigiCertGlobalRootCA.pem',
    api_version=(0,10,0)
)
consumer = KafkaConsumer (
    'yourtopic',
    auto_offset_reset='earliest',
    bootstrap_servers=brokers,
    client_id='yourinstance#youruser#yourpassword#yourclientid',
    security_protocol='SSL',
    ssl_cafile='DigiCertGlobalRootCA.pem',
    ssl_check_hostname=False,
    api_version=(0,10,0)
)
```
For more configuration and usage, please see [kafka-python API](https://kafka-python.readthedocs.io/en/master/apidoc/modules.html).

#### Go client

```
package main

import (
	"context"
	"log"
	"os"
	"os/signal"
	"sync"
	"syscall"
	"time"

	"github.com/Shopify/sarama"
)

func main() {
	server := []string{"yourckafkavip"}
	groupID := "yourgroupid"
	topic := []string{"yourtopicname"}
	config := sarama.NewConfig()
	// Specify the Kafka version by selecting the version corresponding to the purchased CKafka instance. If you don't specify it, Sarama will use the lowest supported version
	config.Version = sarama.V1_1_1_0
	config.Net.SASL.Enable = true
	config.Net.SASL.User = "yourinstance#yourusername"
	config.Net.SASL.Password = "yourpassword"

	//producer
	proClient, err := sarama.NewClient(server, config)
	if err != nil {
		log.Fatalf("unable to create kafka client: %q", err)
	}
	defer proClient.Close()
	producer, err := sarama.NewAsyncProducerFromClient(proClient)
	if err != nil {
		log.Fatalln("failed to start Sarama producer:", err)
	}
	defer producer.Close()

	go func() {
		ticker := time.NewTicker(time.Second)
		for {
			select {
			case t := <-ticker.C:
				// Produce messages to a topic
				msg := &sarama.ProducerMessage{
					Topic: topic[0],
					Key:   sarama.StringEncoder(t.Second()),
					Value: sarama.StringEncoder("Hello World!"),
				}
				producer.Input() <- msg
			}
		}
	}()
	//consumer group
	consumer := Consumer{
		ready: make(chan bool),
	}
	ctx, cancel := context.WithCancel(context.Background())
	client, err := sarama.NewConsumerGroup(server, groupID, config)
	if err != nil {
		log.Panicf("Error creating consumer group client: %v", err)
	}
	wg := &sync.WaitGroup{}
	wg.Add(1)
	go func() {
		defer wg.Done()
		for {
			// "Consume" needs to be called in an infinite loop. When rebalancing occurs, the consumer session needs to be recreated to get a new "ConsumeClaim"
			if err := client.Consume(ctx, topic, &consumer); err != nil {
				log.Panicf("Error from consumer: %v", err)
			}
			// If "context" is set to cancel, it will exit directly
			if ctx.Err() != nil {
				return
			}
			consumer.ready = make(chan bool)
		}
	}()
	log.Println("Sarama consumer up and running!...")

	sigterm := make(chan os.Signal, 1)
	signal.Notify(sigterm, syscall.SIGINT, syscall.SIGTERM)
	select {
	case <-ctx.Done():
		log.Println("terminating: context cancelled")
	case <-sigterm:
		log.Println("terminating: via signal")
	}
	cancel()
	wg.Wait()
	if err = client.Close(); err != nil {
		log.Panicf("Error closing client: %v", err)
	}
}

// Consumer structure
type Consumer struct {
	ready chan bool
}

// The "Setup" function will be called when a new consumer session is created. The call is before the "ConsumeClaim" call
func (consumer *Consumer) Setup(sarama.ConsumerGroupSession) error {
	// Mark the consumer as ready
	close(consumer.ready)
	return nil
}

// The "Cleanup" function will be called after all "ConsumeClaim" coroutines exit
func (consumer *Consumer) Cleanup(sarama.ConsumerGroupSession) error {
	return nil
}

// "ConsumeClaim" is the function that actually processes messages
func (consumer *Consumer) ConsumeClaim(session sarama.ConsumerGroupSession, claim sarama.ConsumerGroupClaim) error {

	// Note:
	// Do not use a coroutine to start the following code.
	// ConsumeClaim will start a coroutine by itself. For the specific behaviors, please see the source code:
	// https://github.com/Shopify/sarama/blob/master/consumer_group.go#L27-L29
	for message := range claim.Messages() {
		log.Printf("Message claimed: value = %s, timestamp = %v, topic = %s", string(message.Value), message.Timestamp, message.Topic)
		session.MarkMessage(message, "")
	}

	return nil
}
```

