## Overview

This document describes how to use the Go SDK to connect to CKafka via the default access point and send and receive messages in a VPC environment.

## Prerequisites

[Install Go](https://golang.org/dl)

## Directions

### Step 1. Add the Go dependent library

Run the following command to install the Go dependent library:

```bash
go get -v gopkg.in/confluentinc/confluent-kafka-go.v1/kafka
```

### Step 2. Prepare configurations

Create a configuration file named `ckafka.json`:

```json
{
  "topic": [
      "test"
  ],
  "bootstrapServers": [
      "xxx-.ap-changsha-ec.ckafka.tencentcloudmq.com:6000"
  ],
  "consumerGroupId": "yourConsumerId"
 }  

```

| Parameter              | Description                                                         |
| ---------------- | :----------------------------------------------------------- |
| Topic            | Topic name. You can obtain it on the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka).  |
| bootstrapServers | Access point. You can obtain it in the **Access Mode** area on the **Basic Info** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka). |
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
	topic := cfg.Topic[0]
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
	err = c.SubscribeTopics(cfg.Topic, nil)
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

4. On the **Consumer Group** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group name, enter the topic name, and click **Query Details** to view the consumption details.
![](https://main.qcloudimg.com/raw/588994dd93d9454f309564e42f61a0fd.png)

