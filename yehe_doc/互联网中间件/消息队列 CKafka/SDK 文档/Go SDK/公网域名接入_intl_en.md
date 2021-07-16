## Overview

This document describes how to use the client for Go to access the SASL access point of CKafka to send/receive messages through the PLAIN mechanism over the public network.

## Prerequisites

- [Install Go](https://golang.org/dl)
- [Configure an ACL policy](https://intl.cloud.tencent.com/document/product/597/39084)
- [Download the demo](https://github.com/TencentCloud/ckafka-sdk-demo/tree/main/gokafkademo/gongwang)

## Directions

### Step 1. Prepare Go dependency library

Download the demo, enter the `gokafkademo` directory, and run the following command to install it.

```bash
go get -v gopkg.in/confluentinc/confluent-kafka-go.v1/kafka
```

### Step 2. Prepare configurations

Create the configuration file `kafka.json`.

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

| Parameters | Description |
| :--------------- | :----------------------------------------------------------- |
| topic             | Topic name, which can be copied from the **Topic Management** page in the console. <br/>![img](https://main.qcloudimg.com/raw/1b34ab83490f228ba0683609e0202c54.png) |
| sasl.username    | Username, which is set when the user is created on the **User Management** page in the console.             |
| sasl.password    | Password, which is set when the user is created on the **User Management** page in the console.             |
| sasl.instanceId  | Instance ID, which can be obtained in **Basic Info** on the **Instance Details** page in the console.<br/>![](https://main.qcloudimg.com/raw/8bbcbd1ff38405a32caf953dd2809512.png) |
| bootstrapServers | Accessed network, which can be copied from the **Network** column in the **Access Mode** section on the **Instance Details** page in the console. <br/>![img](https://main.qcloudimg.com/raw/afc2a197f4e0646f40aa6280c5f6414d.png) |
| consumerGroupId  | You can customize it. After the demo runs successfully, you can see the consumer on the **Consumer Group** page. |

### Step 3. Send a message

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
          // The SASL authentication mechanism type is `PLAIN` by default
          "sasl.mechanism": "PLAIN",
          // Configure an ACL policy locally.
          "security.protocol": "SASL_PLAINTEXT",
          // `username` is the combination of the `instance ID + # + configured username`, and `password` is the configured password.
          "sasl.username": fmt.Sprintf("%s#%s", cfg.SASL.InstanceId, cfg.SASL.Username),
          "sasl.password": cfg.SASL.Password,
  
          // There are three ack mechanisms for a Kafka producer as described below:
          // -1 or all: the broker responds to the producer and continues to send the next message or next batch of messages only after the leader receives the data and syncs it to the followers in all ISRs.
          // This configuration provides the highest data reliability, and messages will never be lost as long as one synced replica survives. Note: this configuration cannot ensure that replicas will be returned after the data is written to all of them.
          // It can be used together with the `min.insync.replicas` parameter at the topic level.
          // 0: the producer does not wait for acknowledgment of sync completion from the broker before it continues to send the next message or next batch of messages. This configuration has the highest production performance but lowest data reliability (data loss may occur when the server fails. If the leader is dead but the producer is unaware of that, the broker cannot receive messages).
          // 1: the producer sends the next message or next batch of messages after it receives an acknowledgment that the leader has successfully received the data. This configuration is a balance between production throughput and data reliability (messages may be lost if the leader is dead but has not been replicated yet).
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

2. Compile and run the program to send the message.
```bash
go run main.go
```

3. View the execution result. Below is a sample:
```bash
Delivered message to test[0]@628
Delivered message to test[0]@629
```

4. On the **Topic Management** page in the [CKafka console](https://console.cloud.tencent.com/ckafka), select the corresponding topic and click **More** > **Message Query** to view the just sent message.
   ![](https://main.qcloudimg.com/raw/417974c1d8df4a5ff409138e7c6b3def.png)

### Step 4. Consume the message

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
          // The SASL authentication mechanism type is `PLAIN` by default
          "sasl.mechanism": "PLAIN",
          // Configure an ACL policy locally.
          "security.protocol": "SASL_PLAINTEXT",
          // `username` is the combination of the `instance ID + # + configured username`, and `password` is the configured password.
          "sasl.username": fmt.Sprintf("%s#%s", cfg.SASL.InstanceId, cfg.SASL.Username),
          "sasl.password": cfg.SASL.Password,
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
      err = c.SubscribeTopics([]string{"test", "test-topic"}, nil)
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
   ![](https://main.qcloudimg.com/raw/22b1e4dd27a79cb96c76f01f2aa7e212.png)

