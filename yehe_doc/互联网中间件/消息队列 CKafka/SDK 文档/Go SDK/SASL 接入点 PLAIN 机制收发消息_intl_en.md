## Overview

This document describes how to connect the Go SDK to CKafka via an SASL access point and send and receive messages based on the PLAIN mechanism in a public network environment.

## Prerequisites

- [Install Go](https://golang.org/dl)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)

## Directions

### Step 1. Prepare the Go dependent library

Run the following command to install the Go dependent library:

```bash
go get -v gopkg.in/confluentinc/confluent-kafka-go.v1/kafka
```

### Step 2. Prepare the configuration file

Create a configuration file named `ckafka.json`:

```json
{
  "topic": [
      "test"
  ],
  "sasl": {
      "username": "yourUserName",
      "password": "yourPassword",
      "instanceId":"instanceId"
  },
  "bootstrapServers": [
      "xxx.ap-changsha-ec.ckafka.tencentcloudmq.com:6000"
  ],
  "consumerGroupId": "yourConsumerId"
 }  

```

| Parameter              | Description                                                         |
| :--------------- | :----------------------------------------------------------- |
| topic            | Topic name. You can obtain it on the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka).     |
| sasl.username    | Username. You can set it when creating a user on the **User Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka).                     |
| sasl.password    | User password. You can set it when creating a user on the **User Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka). |
| sasl.instanceId  | Instance ID. You can obtain it on the **Basic Info** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka).     |
| bootstrapServers | SASL access point. You can obtain it in the **Access Mode** area on the **Basic Info** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka). |
| consumerGroupId  | ID of the consumer group.                                               |


### Step 3. Send messages

1. Write a message producer.

```go
package main

import(
	"fmt"
	"gokafkademo/config"
	"log"
	"strings"

	"github.com/confluentinc/confluent-kafka-go/kafka"
)

func main() {

	cfg, err := config.ParseConfig("../../config/kafka.json")
	if err != nil {
		log.Fatal(err)
	}
	
	p, err := kafka.NewProducer(&kafka.ConfigMap{
		// Set the access point. Obtain the access point of the corresponding topic via the console
		"bootstrap.servers": strings.Join(cfg.Servers, ","),
		// The SASL authentication mechanism is PLAIN by default
		"sasl.mechanism": "PLAIN",
		// Configure an ACL policy locally
		"security.protocol": "SASL_PLAINTEXT",
		// Set `username` to a value in the format of `Instance ID` + `#` + `Configured username`, and `password` to a configured password
		"sasl.username": fmt.Sprintf("%s#%s", cfg.SASL.InstanceId, cfg.SASL.Username),
		"sasl.password": cfg.SASL.Password,
	
		// Kafka producer supports 3 ACK mechanisms:
		// -1 or all: the broker responds to the producer and continues to send the next message or next batch of messages only after the leader receives the data and syncs it to followers in all ISRs.
		// This configuration provides the highest data reliability, as messages will never be lost as long as one synced replica survives. Note: this configuration cannot ensure that replicas will be returned after the data is written to all of them.
		// It can be used together with the `min.insync.replicas` parameter at the topic level.
		// 0: the producer continues to send the next message or next batch of messages without waiting for acknowledgement of synchronization completion from the broker. This configuration provides the highest production performance but lowest data reliability (data loss may occur when the server fails. If the leader is dead but the producer is unaware of that, the broker cannot receive messages).
		// 1: the producer sends the next message or next batch of messages after it receives an acknowledgement that the leader has successfully received the data. This configuration is a balance between production throughput and data reliability (messages may be lost if the leader is dead but has not been replicated yet).
		// If you do not specify a value, the default value will be 1. You can customize this parameter according to your business requirements.
		"acks": 1,
		// Number of retries upon request error. It is recommended that you set the parameter to a value greater than 0 to enable retries and ensure to the greatest extent that messages do not get lost.
		"retries": 0,
		// Retry interval upon request failure
		"retry.backoff.ms": 100,
		// Timeout duration of a producer network request
		"socket.timeout.ms": 6000,
		// Set the interval between retries for the client
		"reconnect.backoff.max.ms": 3000,
	})
	if err != nil {
		log.Fatal(err)
	}
	
	defer p.Close()
	
	// Deliver produced messages to the report processor
	go func() {
		for e := range p.Events() {
			switch ev := e.(type) {
			case *kafka.Message:
				if ev.TopicPartition.Error != nil {
					fmt.Printf("Delivery failed: %v\n", ev.TopicPartition)
				} else {
					fmt.Printf("Delivered message to %v\n", ev.TopicPartition)
				}
			}
		}
	}()
	
	// Send messages in async mode
	topic := cfg.Topic
	for _, word := range []string{"Confluent-Kafka", "Golang Client Message"} {
		_ = p.Produce(&kafka.Message{
			TopicPartition: kafka.TopicPartition{Topic: &topic, Partition: kafka.PartitionAny},
			Value:          []byte(word),
		}, nil)
	}
	
	// Wait for message delivery
	p.Flush(10 * 1000)
```

2. Compile and run the program to send messages.
```bash
go run main.go
```

3. View the running result (example).
```bash
Delivered message to test[0]@628
Delivered message to test[0]@629
```

4. On the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the target topic, and click **More** -> **Message Query** to view the message just sent.

### Step 4. Consume messages

1. Create a single consumer.

```go
package main

import(
	"fmt"
	"gokafkademo/config"
	"log"
	"strings"

	"github.com/confluentinc/confluent-kafka-go/kafka"
)

func main() {

	cfg, err := config.ParseConfig("../../config/kafka.json")
	if err != nil {
		log.Fatal(err)
	}
	
	c, err := kafka.NewConsumer(&kafka.ConfigMap{
		// Set the access point. Obtain the access point of the corresponding topic via the console
		"bootstrap.servers": strings.Join(cfg.Servers, ","),
		// The SASL authentication mechanism is PLAIN by default
		"sasl.mechanism": "PLAIN",
		// Configure an ACL policy locally
		"security.protocol": "SASL_PLAINTEXT",
		// Set `username` to a value in the format of `Instance ID` + `#` + `Configured username`, and `password` to a configured password
		"sasl.username": fmt.Sprintf("%s#%s", cfg.SASL.InstanceId, cfg.SASL.Username),
		"sasl.password": cfg.SASL.Password,
		// Set the message consumer group
		"group.id":          cfg.ConsumerGroupId,
		"auto.offset.reset": "earliest",
	
		// Consumer timeout period when Kafka consumer groups are used. If the broker does not receive the heartbeat of the consumer within this period, the consumer will be considered to have failed and the broker will initiate rebalance.
		// Currently, the value must be in the allowable range (6,000-300,000) as configured in the broker configuration by `group.min.session.timeout.ms` and `group.max.session.timeout.ms`.
		"session.timeout.ms": 10000,
		// "group.min.session.timeout.ms": 6000,
		// "group.max.session.timeout.ms": 300000,
		// Client request timeout period. If no response is received after this time elapses, the request will time out and fail.
		"request.timeout.ms": 305000,
		// Set the interval between retries for the client
		"reconnect.backoff.max.ms": 3000,
	})
	
	if err != nil {
		log.Fatal(err)
	}
	// List of message topics subscribed
	err = c.SubscribeTopics([]string{"test", "test-topic"}, nil)
	if err != nil {
		log.Fatal(err)
	}
	
	for {
		msg, err := c.ReadMessage(-1)
		if err == nil {
			fmt.Printf("Message on %s: %s\n", msg.TopicPartition, string(msg.Value))
		} else {
			// The client automatically recovers all errors
			fmt.Printf("Consumer error: %v (%v)\n", err, msg)
		}
	}
	
	c.Close()
}
```


2. Compile and run the program to consume messages.
```bash
go run main.go
```

3. View the running result (example).
```bash
Message on test[0]@628: Confluent-Kafka
Message on test[0]@629: Golang Client Message
```

4. On the **Consumer Group** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name, and click **Query Details** to view the consumption details.
![](https://main.qcloudimg.com/raw/e4a2d799b4b755e53409a2e582ec51f2.png)

