## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for C++ as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- You have installed [GCC](https://gcc.gnu.org/install/).
- You have downloaded the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-cpp-sdk-demo.zip).

## Directions

1. Prepare the environment.
   1. Install RocketMQ-Client-CPP in the client environment as instructed in the [official documentation](https://github.com/apache/rocketmq-client-cpp). **The master branch is recommended**.
   2. Import the header files and dynamic libraries related to RocketMQ-Client-CPP to the project.
2. Instantiate the message producer.
<dx-codeblock>
:::  c++
   // Set the producer group name
   DefaultMQProducer producer(groupName);
   // Set the service access address
   producer.setNamesrvAddr(nameserver);
   // Set user permissions
   producer.setSessionCredentials(
       accessKey,  // Role token
       secretKey, // Role name
       "");
   // Set the full namespace name
   producer.setNameSpace(namespace);
   // Make sure all parameters are configured before the start
   producer.start();
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
<td align="left">groupName</td>
<td align="left">Producer group name, which can be obtained under the <code>Group</code> tab on the <strong>Cluster</strong> page in the console.</td>
</tr>
<tr>
<td align="left">nameserver</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the <strong>Operation</strong> column on the <strong>Cluster</strong> page in the console. Namespace access addresses in new shared or exclusive clusters can be copied from the <strong>Namespace</strong> list. <img src="https://qcloudimg.tencent-cloud.cn/raw/450608d93e6980799de91b27acbe98bc.png" alt=""></td>
</tr>
<tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/cce162feb5e5dd2e4b43b9194ec3f35d.png" alt="img"></td>
</tr>
<tr>
<td align="left">namespace</td>
<td align="left">The namespace name can be copied under the <code>Topic</code> tab on the <strong>Cluster</strong> page in the console, which is in the format of <strong>cluster ID + | + namespace</strong>. <img src="https://qcloudimg.tencent-cloud.cn/raw/084551ffba9253f9d0280d872018289e.png" alt=""></td>
</tr>
</tbody></table>
3. Send messages.
<dx-codeblock>
:::  c++
   // Initialize message content
      MQMessage msg(
          topicName,  // Topic name
          TAGS,		// Message tag
          KEYS,		// Message key
          "Hello cpp client, this is a message."  // Message content
      );
   
      try {
          // Send the message
          SendResult sendResult = producer.send(msg);
          std::cout << "SendResult:" << sendResult.getSendStatus() << ", Message ID: " << sendResult.getMsgId()
              << std::endl;
      } catch (MQException e) {
          std::cout << "ErrorCode: " << e.GetError() << " Exception:" << e.what() << std::endl;
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
<td align="left">Topic name, which can be copied under the <code>Topic</code> tab on the <strong>Cluster</strong> page in the console. <img src="https://qcloudimg.tencent-cloud.cn/raw/307921e6fea2543af0fc5ebc02cb4d21.png" alt=""></td>
</tr>
<tr>
<td align="left">TAGS</td>
<td align="left">A parameter used to set the message tag.</td>
</tr>
<tr>
<td align="left">KEYS</td>
<td align="left">A parameter used to set the message key.</td>
</tr>
</tbody></table>
4. Release the resources.
<dx-codeblock>
:::  c++
   // Release resources
      producer.shutdown();
:::
</dx-codeblock>
5. Initialize the consumer.
<dx-codeblock>
:::  c++
   // Listen on messages
      class ExampleMessageListener : public MessageListenerConcurrently {
      public:
          ConsumeStatus consumeMessage(const std::vector<MQMessageExt> &msgs) {
              for (auto item = msgs.begin(); item != msgs.end(); item++) {
                  // Business
                  std::cout << "Received Message Topic:" << item->getTopic() << ", MsgId:" << item->getMsgId() << ", TAGS:"
                            << item->getTags() << ", KEYS:" << item->getKeys() << ", Body:" << item->getBody() << std::endl;
              }
              // Return CONSUME_SUCCESS if the consumption is successful
              return CONSUME_SUCCESS;
              // Return RECONSUME_LATER if the consumption failed. The message will be consumed again.
              // return RECONSUME_LATER;
          }
      };
   
      // Initialize the consumer
      DefaultMQPushConsumer *consumer = new DefaultMQPushConsumer(groupName);
      // Set the service address
      consumer->setNamesrvAddr(nameserver);
      // Set user permissions
      consumer->setSessionCredentials(
          accessKey,
          secretKey, 
          "");
      // Set the namespace
      consumer->setNameSpace(namespace);
      // Set the instance name
      consumer->setInstanceName("CppClient");
   
      // Register a custom listener function to process the received messages and return the processing results
      ExampleMessageListener *messageListener = new ExampleMessageListener();
      // Subscribe to the message
      consumer->subscribe(topicName, TAGS);
      // Set the message listener
      consumer->registerMessageListener(messageListener);
   
      // After the preparations, you must call the start function before the consumption can start.
      consumer->start();
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
<td align="left">groupName</td>
<td align="left">Consumer group name, which can be obtained under the <code>Group</code> tab on the <strong>Cluster</strong> page in the console.</td>
</tr>
<tr>
<td align="left">nameserver</td>
<td align="left">Cluster access address, which can be copied from <strong>Access Address</strong> in the <strong>Operation</strong> column on the <strong>Cluster</strong> page in the console. Namespace access addresses in new shared or exclusive clusters can be copied from the <strong>Namespace</strong> list. <img src="https://qcloudimg.tencent-cloud.cn/raw/de47c97b9e1609ee6357e28bd7e1ad12.png" alt=""></td>
</tr>
<tr>
<td align="left">secretKey</td>
<td align="left">Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td align="left">accessKey</td>
<td align="left">Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://qcloudimg.tencent-cloud.cn/raw/cce162feb5e5dd2e4b43b9194ec3f35d.png" alt="img"></td>
</tr>
<tr>
<td align="left">namespace</td>
<td align="left">The namespace name can be copied under the <code>Topic</code> tab on the <strong>Cluster</strong> page in the console, which is in the format of <strong>cluster ID + | + namespace</strong>. <img src="https://qcloudimg.tencent-cloud.cn/raw/fc317c3c1dbe637456e45d1974e1c6e4.png" alt=""></td>
</tr>
<tr>
<td align="left">topicName</td>
<td align="left">Topic name, which can be copied under the <code>Topic</code> tab on the <strong>Cluster</strong> page in the console. <img src="https://qcloudimg.tencent-cloud.cn/raw/1eb1505b6a40857b4b9145af8426bf48.png" alt=""></td>
</tr>
<tr>
<td align="left">TAGS</td>
<td align="left">A parameter used to set the tag of messages that are subscribed to.</td>
</tr>
</tbody></table>
6. Release the resources.
<dx-codeblock>
:::  c++
   // Release resources
   consumer->shutdown();
:::
</dx-codeblock>
7. View consumption details. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.

![img](https://qcloudimg.tencent-cloud.cn/raw/1c0aea477bbc02d536589904af6dae27.png)





>?Above is a brief introduction to message publishing and subscription. For more information, see the [demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-cpp-sdk-demo.zip) or [RocketMQ-Client-CPP Examples](https://github.com/apache/rocketmq-client-cpp/tree/master/example).
