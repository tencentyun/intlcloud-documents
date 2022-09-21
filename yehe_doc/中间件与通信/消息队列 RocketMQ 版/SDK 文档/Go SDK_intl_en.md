## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Go as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- You have created the required resources as instructed in [Resource Creation and Preparation](https://intl.cloud.tencent.com/document/product/1112/43069).
- You have installed [Go](https://golang.org/dl/).
- You have downloaded the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-go-sdk-demo.zip).

## Directions

1. Run the following command in the client environment to RocketMQ client dependencies.
<dx-codeblock>
:::  go
go get github.com/apache/rocketmq-client-go/v2
:::
</dx-codeblock>
2. Create a producer.
<dx-codeblock>
:::  go
   // Service access address (Note: Add "http://" or "https://" before the access address; otherwise, it cannot be resolved)
      var serverAddress = "https://rocketmq-xxx.rocketmq.ap-bj.public.tencenttdmq.com:9876"
      // Authorize the role name
      var secretKey = "admin"
      // Authorize the role token
      var accessKey = "eyJrZXlJZC...."
      // Full namespace name
      var nameSpace = "rocketmq-xxx|namespace_go"
      // Producer group name
      var groupName = "group1"
      // Create a message producer
      p, _ := rocketmq.NewProducer(
          // Set the service address
          producer.WithNsResolver(primitive.NewPassthroughResolver([]string{serverAddress})),
          // Set ACL permissions
          producer.WithCredentials(primitive.Credentials{
              SecretKey: secretKey,
              AccessKey: accessKey,
          }),
          // Set the producer group
          producer.WithGroupName(groupName),
          // Set the namespace name
          producer.WithNamespace(nameSpace),
          // Set the number of retries upon sending failures
          producer.WithRetry(2),
      )
      // Start the producer
      err := p.Start()
      if err != nil {
          fmt.Printf("start producer error: %s", err.Error())
          os.Exit(1)
      }
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/679d9eb0c39df9722fc8e2e82f52cb46.png" alt="img"></td>
</tr>
<tr>
<td align="left">nameSpace</td>
<td align="left">The namespace name can be copied under the <code>Topic</code> tab on the <strong>Cluster</strong> page in the console, which is in the format of <strong>cluster ID + | + namespace</strong>. <img src="https://qcloudimg.tencent-cloud.cn/raw/823fb2bd90d17ecb24960ffea027a910.png" alt=""></li></td>
</tr>
<tr>
<td align="left">serverAddress</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the <strong>Operation</strong> column on the <strong>Cluster</strong> page in the console. Namespace access addresses in new shared or exclusive clusters can be copied from the <strong>Namespace</strong> list. (<strong>Note: Add `http://` or `https://` before the access address; otherwise, it cannot be resolved.</strong>). <img src="https://qcloudimg.tencent-cloud.cn/raw/5ec413fb25af95bbd7ce9beb17cc62f6.png" alt=""></td>
</tr>
<tr>
<td align="left">groupName</td>
<td align="left">Producer group name, which can be copied under the <strong>Group</strong> tab in the console.</td>
</tr>
</tbody></table>
3. Send messages (using sync sending as an example).
<dx-codeblock>
:::  go
   // Topic name
      var topicName = "topic1"
      // Configure message content
      msg := &primitive.Message{
          Topic: topicName, // Set the topic name
          Body:  []byte("Hello RocketMQ Go Client! This is a new message."),
      }
      // Set tags
      msg.WithTag("TAG")
      // Set keys
      msg.WithKeys([]string{"yourKey"})
      // Send the message
      res, err := p.SendSync(context.Background(), msg)
   
      if err != nil {
          fmt.Printf("send message error: %s\n", err)
      } else {
          fmt.Printf("send message success: result=%s\n", res.String())
      }
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">topicName</td>
<td align="left">Topic name, which can be copied under the <code>Topic</code> tab on the <strong>Cluster</strong> page in the console. <img src="https://qcloudimg.tencent-cloud.cn/raw/2b52e1983fb576cc10b074cd7f1a15a8.png" alt=""></td>
</tr>
<tr>
<td align="left">TAG</td>
<td align="left">Message tag.</td>
</tr>
<tr>
<td align="left">yourKey</td>
<td align="left">Message key.</td>
</tr>
</tbody></table>
Release the resources.
<dx-codeblock>
:::  go
   // Disable the producer
      err = p.Shutdown()
      if err != nil {
          fmt.Printf("shutdown producer error: %s", err.Error())
      }
:::
</dx-codeblock>

>? For more information on async sending and one-way sending, see the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-go-sdk-demo.zip) or [RocketMQ-Client-Go Examples](https://github.com/apache/rocketmq-client-go/tree/master/examples).

4. Create a consumer.
<dx-codeblock>
:::  go
   // Service access address (Note: Add "http://" or "https://" before the access address; otherwise, it cannot be resolved)
      var serverAddress = "https://rocketmq-xxx.rocketmq.ap-bj.public.tencenttdmq.com:9876"
      // Authorize the role name
      var secretKey = "admin"
      // Authorize the role token
      var accessKey = "eyJrZXlJZC...."
      // Full namespace name
      var nameSpace = "rocketmq-xxx|namespace_go"
      // Producer group name
      var groupName = "group11"
      // Create a consumer
      c, err := rocketmq.NewPushConsumer(
          // Set the consumer group
          consumer.WithGroupName(groupName),
          // Set the service address
          consumer.WithNsResolver(primitive.NewPassthroughResolver([]string{serverAddress})),
          // Set ACL permissions
          consumer.WithCredentials(primitive.Credentials{
              SecretKey: secretKey,
              AccessKey: accessKey,
          }),
          // Set the namespace name
          consumer.WithNamespace(nameSpace),
          // Set consumption from the start offset
          consumer.WithConsumeFromWhere(consumer.ConsumeFromFirstOffset),
          // Set the consumption mode (cluster consumption by default)
          consumer.WithConsumerModel(consumer.Clustering),
      )
      if err != nil {
          fmt.Println("init consumer2 error: " + err.Error())
          os.Exit(0)
      }
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/ba6af7b1188b3f5864e037e71743178a.png" alt="img"></td>
</tr>
<tr>
<td align="left">nameSpace</td>
<td align="left">The namespace name can be copied under the <code>Topic</code> tab on the <strong>Cluster</strong> page in the console, which is in the format of <strong>cluster ID + | + namespace</strong>. <img src="https://qcloudimg.tencent-cloud.cn/raw/dd397f141e6388407e99018e7d4fc8a7.png" alt=""></li></td>
</tr>
<tr>
<td align="left">serverAddress</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the <strong>Operation</strong> column on the <strong>Cluster</strong> page in the console. Namespace access addresses in new shared or exclusive clusters can be copied from the <strong>Namespace</strong> list. (<strong>Note: Add `http://` or `https://` before the access address; otherwise, it cannot be resolved.</strong>). <img src="https://qcloudimg.tencent-cloud.cn/raw/baf2bd3e35110f2fae6b936eaa2f723b.png" alt=""></td>
</tr>
<tr>
<td align="left">groupName</td>
<td align="left">Producer group name, which can be copied under the <strong>Group</strong> tab in the console.</td>
</tr>
</tbody></table>
5. Consume the message.
<dx-codeblock>
:::  go
   // Topic name
      var topicName = "topic1"
      // Set the tag of messages that are subscribed to
      selector := consumer.MessageSelector{
          Type:       consumer.TAG,
          Expression: "TagA || TagC",
      }
      // Set the delay level of consumption retry. A total of 18 levels can be set. Below is the relationship between each delay level and the delay time.
      // 1   2   3    4    5   6   7   8   9   10  11  12  13  14   15   16   17  18
      // 1s, 5s, 10s, 30s, 1m, 2m, 3m, 4m, 5m, 6m, 7m, 8m, 9m, 10m, 20m, 30m, 1h, 2h
      delayLevel := 1
      err = c.Subscribe(topicName, selector, func(ctx context.Context,
                                                                    msgs ...*primitive.MessageExt) (consumer.ConsumeResult, error) {
          fmt.Printf("subscribe callback len: %d \n", len(msgs))
      	// Set the delay level for the next consumption
          concurrentCtx, _ := primitive.GetConcurrentlyCtx(ctx)
          concurrentCtx.DelayLevelWhenNextConsume = delayLevel // only run when return consumer.ConsumeRetryLater
   
          for _, msg := range msgs {
              // Simulate a successful consumption after three retries
              if msg.ReconsumeTimes > 3 {
                  fmt.Printf("msg ReconsumeTimes > 3. msg: %v", msg)
                  return consumer.ConsumeSuccess, nil
              } else {
                  fmt.Printf("subscribe callback: %v \n", msg)
              }
          }
          // Simulate a consumption failure. Retry is required.
          return consumer.ConsumeRetryLater, nil
      })
      if err != nil {
          fmt.Println(err.Error())
      }
:::
</dx-codeblock>
<table>
<thead>
<tr>
<th align="left">Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">topicName</td>
<td align="left">Topic name, which can be copied under the <strong>Topic</strong> tab in the console. <img src="https://qcloudimg.tencent-cloud.cn/raw/4b2b11c05edaa3ef5f8be278a1a49852.png" alt=""></td>
</tr>
<tr>
<td align="left">Expression</td>
<td align="left">Message tag.</td>
</tr>
<tr>
<td align="left">delayLevel</td>
<td align="left">A parameter used to set the delay level of consumption retry. A total of 18 delay levels are supported.</td>
</tr>
</tbody></table>
6. Consume messages (the consumer can consume messages only after the messages are subscribed to).
<dx-codeblock>
:::  go
   // Start consumption
      err = c.Start()
      if err != nil {
          fmt.Println(err.Error())
          os.Exit(-1)
      }
      time.Sleep(time.Hour)
      // Release resources
      err = c.Shutdown()
      if err != nil {
          fmt.Printf("shundown Consumer error: %s", err.Error())
      }
:::
</dx-codeblock>
7. View consumption details. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.
 ![img](https://qcloudimg.tencent-cloud.cn/raw/c50484e8f9549063248a4887da9769de.png)

   

>?Above is a brief introduction to how to send and receive messages with the Go client. For more information, see the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-go-sdk-demo.zip) or [Rocketmq-Client-Go Examples](https://github.com/apache/rocketmq-client-go/tree/master/examples).

