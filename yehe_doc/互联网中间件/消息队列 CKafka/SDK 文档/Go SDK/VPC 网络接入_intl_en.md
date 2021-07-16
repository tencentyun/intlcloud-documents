## Overview

This document describes how to access CKafka to send/receive messages with the SDK for Go in a VPC.

## Prerequisites

- [Install Go](https://golang.org/dl/)
- [Download the demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/gokafkademo/VPC)

## Directions

### Step 1. Prepare configurations

1. Upload the `gokafkademo` in the downloaded demo to the Linux server.
2. Log in to the Linux server, enter the `gokafkademo` directory, and run the following command to add the dependency library.

```bash
go get -v gopkg.in/confluentinc/confluent-kafka-go.v1/kafka
```

3. Modify the configuration file `kafka.json`.

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

| Parameters | Description |
| ---------------- | :----------------------------------------------------------- |
| topic             | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/e7d353c89bbb204303501e8366f59d2c.png) |
| bootstrapServers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![img](https://main.qcloudimg.com/raw/88b29cffdf22e3a0309916ea715057a1.png) |
| consumerGroupId  | You can customize it. After the demo runs successfully, you can see the consumer on the **Consumer Group** page. |

### Step 2. Send a message

1. Write the message production program.

   ```go
   package main
   import (
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
       // Set the access point of the corresponding topic, which can be obtained in the console
       "bootstrap.servers": strings.Join(cfg.Servers, ","),
       // If you do not explicitly configure this, the value of 1 will be used by default. You can customize this according to your business conditions
       "acks": 1,
       // Number of retries upon request error. We recommend you set the value to be greater than 0. Retries can ensure as much as possible that the message will not be lost
       "retries": 0,
       // The time between when a request fails and the next time the request is retried
       "retry.backoff.ms": 100,
       // Timeout period of the producer network request
       "socket.timeout.ms": 6000,
       // Set the internal retry interval of the client
       "reconnect.backoff.max.ms": 3000,
   })
   if err != nil {
       log.Fatal(err)
   }
       defer p.Close()
       // Pass the produced message to the report handler
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
       // Send the message asynchronously
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

2. Compile and run the program to send the message.
   ```go
   go run main.go
   ```

3. View the execution result. Below is a sample:
   ```go
   Delivered message to test[0]@628
   Delivered message to test[0]@629
   ```

4. On the **Topic Management** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding topic and click **More** > **Message Query** to view the just sent message.
   ![](https://main.qcloudimg.com/raw/ec5fbf218cf50ff3d760be15f6331867.png)

### Step 3. Consume the message

1. Write the message consumption program.

```go
  package main
  
  import (
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
          // Set the access point of the corresponding topic, which can be obtained in the console
          "bootstrap.servers": strings.Join(cfg.Servers, ","),
          // The set message consumer group
          "group.id":          cfg.ConsumerGroupId,
          "auto.offset.reset": "earliest",
  
          // Consumer timeout period when the Kafka consumer grouping mechanism is used. If the broker does not receive the heartbeat of the consumer within this period, the consumer will be considered to have failed and the broker will initiate rebalance.
          // Currently, this value must be configured between `group.min.session.timeout.ms=6000` and `group.max.session.timeout.ms=300000` on the broker
          "session.timeout.ms": 10000,
      })
  
      if err != nil {
          log.Fatal(err)
      }
      // List of the subscribed message topics
      err = c.SubscribeTopics(cfg.Topic, nil)
      if err != nil {
          log.Fatal(err)
      }
  
      for {
          msg, err := c.ReadMessage(-1)
          if err == nil {
              fmt.Printf("Message on %s: %s\n", msg.TopicPartition, string(msg.Value))
          } else {
              // The client will automatically try to resolve all errors
              fmt.Printf("Consumer error: %v (%v)\n", err, msg)
          }
      }
  
      c.Close()
  }
```

2. Compile and run the program to consume the message.
```bash
  go run main.go
```

3. View the execution result. Below is a sample:
```bash
Message on test[0]@628: Confluent-Kafka
Message on test[0]@629: Golang Client Message
```

4. On the **Consumer Group** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name in **Topic Name**, and click **Query Details** to view the consumption details.
   ![](https://main.qcloudimg.com/raw/27775267907600f4ff759e6a197195ee.png)

