## Overview

This document describes how to access CKafka to send/receive messages with the SDK for Go through SASL_PLAINTEXT over public network.

## Prerequisites

- [Install Go](https://golang.org/dl)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)
- [Download demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/gokafkademo/PUBLIC_SASL)

## Directions

### Step 1. Prepare the Go dependent library

Download the demo, enter the `gokafkademo` directory, and run the following command to install it.

```bash
go get -v gopkg.in/confluentinc/confluent-kafka-go.v1/kafka
```

### Step 2. Prepare configurations

Create a configuration file named `kafka.json`.

```json
{
  "topic": [
      "xxxx"
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
| topic             | Topic name, which can be copied in **Topic Management** on the instance details page in the console. <br/>![img](https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png) |
| sasl.username    | Username, which is set when the user is created in **User Management** on the instance details page in the console.                     |
| sasl.password    | Password, which is set when the user is created in **User Management** on the instance details page in the console.             |
| sasl.instanceId  | Instance ID, which can be obtained in **Basic Info** on the instance details page in the console.<br/>![](https://main.qcloudimg.com/raw/8bbcbd1ff38405a32caf953dd2809512.png) |
| bootstrapServers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section in **Basic Info** on the instance details page in the console. <br/>![img](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png) |
| consumerGroupId  | You can customize it. After the demo runs successfully, you can see the consumer on the **Consumer Group** page. |

### Step 3. Send messages

1. Write a message production program.

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
  
      cfg, err := config.ParseConfig("../config/kafka.json")
      if err != nil {
          log.Fatal(err)
      }
  
      p, err := kafka.NewProducer(&kafka.ConfigMap{
          // Set the access point of the corresponding topic, which can be obtained in the console
          "bootstrap.servers": strings.Join(cfg.Servers, ","),
          // The SASL authentication mechanism is PLAIN by default
          "sasl.mechanism": "PLAIN",
          // Configure an ACL policy locally
          "security.protocol": "SASL_PLAINTEXT",
          // Set “username” to a value in the format of “instance ID + # + configured username”, and “password” to the configured password
          "sasl.username": fmt.Sprintf("%s#%s", cfg.SASL.InstanceId, cfg.SASL.Username),
          "sasl.password": cfg.SASL.Password,
  
          // Kafka producer supports 3 ACK mechanisms:
          // -1 or all: the broker responds to the producer and continues to send the next message or next batch of messages only after the leader receives the data and syncs it to followers in all ISRs.
          // This configuration provides the highest data reliability, as messages will never get lost as long as one synced replica survives. It should be noted that this configuration cannot guarantee that replicas will be returned after data has been read from or written to all of them.
          // It can be used together with the “min.insync.replicas” parameter at the topic level.
          // 0: the producer continues to send the next message or next batch of messages without waiting for the broker’s acknowledgment of sync. This configuration provides the highest production performance but the lowest data reliability as data may get lost when the server fails. If the leader is dead but the producer is unaware of that, the broker cannot receive messages.
          // 1: the producer sends the next message or next batch of messages after it receives an acknowledgment that the leader has successfully received the data. This configuration is a balance between production throughput and data reliability. Messages may get lost if the leader is dead but has not been replicated yet.
          // If you do not configure this parameter, the default value will be 1. You can customize this according to your business requirements.
          "acks": 1,
          // Number of retries upon request error. It is recommended that you set the parameter to a value greater than 0 to enable retries and guarantee that messages are not lost to the greatest extent possible.
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
  
      // Deliver the produced messages to the report processor
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

3. View the execution result. Below is a sample:

```bash
Delivered message to test[0]@628
Delivered message to test[0]@629
```

4. On the **Topic Management** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding topic, and click **More** > **Message Query** to view the messages just sent.
   ![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)

### Step 4. Consume messages

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
  
      cfg, err := config.ParseConfig("../config/kafka.json")
      if err != nil {
          log.Fatal(err)
      }
  
      c, err := kafka.NewConsumer(&kafka.ConfigMap{
          // Set the access point of the corresponding topic, which can be obtained in the console
          "bootstrap.servers": strings.Join(cfg.Servers, ","),
          // The SASL authentication mechanism is PLAIN by default
          "sasl.mechanism": "PLAIN",
          // Configure an ACL policy locally
          "security.protocol": "SASL_PLAINTEXT",
          // Set “username” to a value in the format of “instance ID + # + configured username”, and “password” to the configured password
          "sasl.username": fmt.Sprintf("%s#%s", cfg.SASL.InstanceId, cfg.SASL.Username),
          "sasl.password": cfg.SASL.Password,
          // The set message consumer group
          "group.id":          cfg.ConsumerGroupId,
          "auto.offset.reset": "earliest",
  
          // Consumer timeout period when the Kafka consumer grouping mechanism is used. If the broker does not receive the heartbeat of the consumer within this period, the consumer will be considered to have failed and the broker will initiate rebalance.
          // Currently, this value must be configured in the broker between 6000 (value of group.min.session.timeout.ms) and 300000 (value of group.max.session.timeout.ms).
          "session.timeout.ms": 10000,
      })
  
      if err != nil {
          log.Fatal(err)
      }
      // List of subscribed message topics
      err = c.SubscribeTopics([]string{"test", "test-topic"}, nil)
      if err != nil {
          log.Fatal(err)
      }
  
      for  {
          msg, err := c.ReadMessage(-1)
          if err == nil {
              fmt.Printf("Message on %s: %s\n", msg.TopicPartition, string(msg.Value))
          } else {
              // The client will automatically try to recover all errors
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

3. View the execution result. Below is a sample:

```bash
Message on test[0]@628: Confluent-Kafka
Message on test[0]@629: Golang Client Message
```

4. On the **Consumer Group** tab page on the instance details page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding consumer group, enter the topic name, and click **View Details** to view the consumption details.
   ![](https://main.qcloudimg.com/raw/22b1e4dd27a79cb96c76f01f2aa7e212.png)
