## 操作背景

该任务指导您如何在 VPC 环境下使用 Go SDK 接入消息队列 CKafka 版的默认接入点并收发消息。

## 前提条件

[安装 Go](https://golang.org/dl/)

## 操作步骤

### 步骤一：添加依赖库

执行以下命令安装：

```bash
go get -v gopkg.in/confluentinc/confluent-kafka-go.v1/kafka
```

### 步骤二：准备配置

创建配置文件 ckafka.json：

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

| 参数             | 描述                                                         |
| ---------------- | :----------------------------------------------------------- |
| Topic            | Topic 名称。您可在 [CKafka 控制台](https://console.cloud.tencent.com/ckafka) 的 Topic 管理页面获取。 |
| bootstrapServers | 接入点，在 CKafka 控制台的实例详情页面的【基本信息】>【接入方式】获取。 |
| consumerGroupId  | 配置的消费组 ID。                                             |

### 步骤三：发送消息

1. 编写生产消息程序。

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
		// 设置接入点，请通过控制台获取对应Topic的接入点。
		"bootstrap.servers": strings.Join(cfg.Servers, ","),
		// 用户不显示配置时，默认值为1。用户根据自己的业务情况进行设置
		"acks": 1,
		// 请求发生错误时重试次数，建议将该值设置为大于0，失败重试最大程度保证消息不丢失
		"retries": 0,
		// 发送请求失败时到下一次重试请求之间的时间
		"retry.backoff.ms": 100,
		// producer 网络请求的超时时间。
		"socket.timeout.ms": 6000,
		// 设置客户端内部重试间隔。
		"reconnect.backoff.max.ms": 3000,
	})
	if err != nil {
		log.Fatal(err)
	}
	
	defer p.Close()
	
	// 产生的消息 传递至报告处理程序
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
	
	// 异步发送消息
	topic := cfg.Topic[0]
	for _, word := range []string{"Confluent-Kafka", "Golang Client Message"} {
		_ = p.Produce(&kafka.Message{
			TopicPartition: kafka.TopicPartition{Topic: &topic, Partition: kafka.PartitionAny},
			Value:          []byte(word),
		}, nil)
	}
	
	// 等待消息传递
	p.Flush(10 * 1000)
```



2. 编译并运行程序发送消息。
```bash
go run main.go
```

3. 运行结果示例。
```bash
Delivered message to test[0]@628
Delivered message to test[0]@629
```

4. 在 [CKafka 控制台](https://console.cloud.tencent.com/ckafka) 的【topic管理】页面，选择对应的 topic ， 点击【更多】>【消息查询】，查看刚刚发送的消息。
      ![](https://main.qcloudimg.com/raw/7a2410794186b47c9126dbe8b878228d.png)

### 步骤四：消费消息

1. 创建单个 Consumer。

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
		// 设置接入点，请通过控制台获取对应Topic的接入点。
		"bootstrap.servers": strings.Join(cfg.Servers, ","),
		// 设置的消息消费组
		"group.id":          cfg.ConsumerGroupId,
		"auto.offset.reset": "earliest",
	
		// 使用 Kafka 消费分组机制时，消费者超时时间。当 Broker 在该时间内没有收到消费者的心跳时，认为该消费者故障失败，Broker
		// 发起重新 Rebalance 过程。目前该值的配置必须在 Broker 配置group.min.session.timeout.ms=6000和group.max.session.timeout.ms=300000 之间
		"session.timeout.ms": 10000,
		// "group.min.session.timeout.ms": 60000,
		// "group.max.session.timeout.ms": 300000,
		//  客户端请求超时时间，如果超过这个时间没有收到应答，则请求超时失败
		"request.timeout.ms": 305000,
		// 设置客户端内部重试间隔。
		"reconnect.backoff.max.ms": 3000,
	})
	
	if err != nil {
		log.Fatal(err)
	}
	// 订阅的消息topic 列表
	err = c.SubscribeTopics(cfg.Topic, nil)
	if err != nil {
		log.Fatal(err)
	}
	
	for {
		msg, err := c.ReadMessage(-1)
		if err == nil {
			fmt.Printf("Message on %s: %s\n", msg.TopicPartition, string(msg.Value))
		} else {
			// 客户端将自动尝试恢复所有的 error
			fmt.Printf("Consumer error: %v (%v)\n", err, msg)
		}
	}
	
	c.Close()
}
```


2. 编译并运行程序消费消息。
```bash
go run main.go
```

3. 运行结果示例
```bash
Message on test[0]@628: Confluent-Kafka
Message on test[0]@629: Golang Client Message
```

4. 在 [CKafka 控制台](https://console.cloud.tencent.com/ckafka) 的【Consumer Group】页面，选择对应的消费组名称，在主题名称输入topic名称，点击【查询详情】，查看消费详情。
![](https://main.qcloudimg.com/raw/588994dd93d9454f309564e42f61a0fd.png)

