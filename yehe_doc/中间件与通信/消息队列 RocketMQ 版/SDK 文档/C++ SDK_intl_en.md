## Overview

This document describes how to use open-source SDK to send and receive messages using the SDK for C++ as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- [You have installed GCC](https://gcc.gnu.org/install/)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-cpp-sdk-demo.zip)

## Directions

### Step 1. Prepare the environment
1. Install RocketMQ-Client-CPP in the client environment as instructed in the [official documentation](https://github.com/apache/rocketmq-client-cpp). **The master branch is recommended**.
2. Import the header files and dynamic libraries related to RocketMQ-Client-CPP to the project.

### Step 2. Produce messages
1. Create message producers.
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
   producer.setNameSpace(nameserver);
   // Make sure all parameters are configured before the start
   producer.start();
:::
</dx-codeblock>
<table>
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>groupName</td>
        <td>Producer group name, which can be obtained under the <b>Group</b> tab on the cluster details page in the console.</td>
    </tr>
    <tr>
        <td>nameserver</td>
				<td>Cluster access address, which can be obtained in the console by clicking <b>Access Address</b> in the <b>Operation</b> column of the cluster list on the <b>Cluster</b> page.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/450608d93e6980799de91b27acbe98bc.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>secretKey</td>
        <td>Role name, which can be copied on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.</td>
    </tr>
    <tr>
        <td>accessKey</td>
        <td>Role token, which can be copied in the <b>Token</b> column on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/f088dfa12f2e659aba5f07cdf8ac953c.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>namespace</td>
        <td>Full namespace name in the format of <code>cluster ID</code> +<code>｜</code>+<code>namespace</code>, which can be copied under the <b>Topic</b> tab on the cluster details page in the console.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/084551ffba9253f9d0280d872018289e.png" style="width: 100%">
        </td>
    </tr>
</table>
2. Send messages.
<dx-codeblock>
:::  c++
   // Initialize message content
   MQMessage msg(
       topicName,  // Topic name
       TAGS,// Message tag
       KEYS,// Message key
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
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>topicName</td>
        <td>Topic name, which can be copied under the <b>Topic</b>tab on the cluster details page in the console.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/307921e6fea2543af0fc5ebc02cb4d21.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>TAGS</td>
        <td>A parameter used to set the message tag.</td>
    </tr>
    <tr>
        <td>KEYS</td>
        <td>A parameter used to set the message key.</td>
    </tr>
</table>
3. Release resources.
<dx-codeblock>
:::  c++
   // Release resources
   producer.shutdown();
:::
</dx-codeblock>

### Step 3. Consume messages
1. Create a consumer.
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
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>groupName</td>
        <td>Consumer group name, which can be obtained under the <b>Group</b> tab on the cluster details page in the console.</td>
    </tr>
    <tr>
        <td>nameserver</td>
        <td>Cluster access address, which can be obtained by clicking <b>Access Address</b> in the <b>Operation</b>column of the cluster list on the <b>Cluster</b> page.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/de47c97b9e1609ee6357e28bd7e1ad12.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>secretKey</td>
        <td>Role name, which can be copied on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.</td>
    </tr>
    <tr>
        <td>accessKey</td>
        <td>Role token, which can be copied in the <b>Token</b> column on the <a href = "https://console.cloud.tencent.com/tdmq/role"><b>Role Management</b></a> page.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/cce162feb5e5dd2e4b43b9194ec3f35d.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>namespace</td>
        <td>Full namespace name in the format of <code>cluster ID</code> +<code>｜</code>+<code>namespace</code>, which can be copied under the <b>Topic</b> tab on the cluster details page in the console.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/fc317c3c1dbe637456e45d1974e1c6e4.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>topicName</td>
        <td>Topic name, which can be copied under the <b>Topic</b> tab on the cluster details page in the console.
            <img src = "https://qcloudimg.tencent-cloud.cn/raw/1eb1505b6a40857b4b9145af8426bf48.png" style="width: 100%">
        </td>
    </tr>
    <tr>
        <td>TAGS</td>
        <td>A parameter used to set the tag of messages that are subscribed to.</td>
    </tr>
</table>
2. Release resources.
<dx-codeblock>
:::  c++
   // Release resources
   consumer->shutdown();
:::
</dx-codeblock>


### Step 4. View consumption details
Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.
![](https://qcloudimg.tencent-cloud.cn/raw/1c0aea477bbc02d536589904af6dae27.png)


>?Above is a brief introduction to message publishing and subscription. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/rocketmq/tdmq-rocketmq-cpp-sdk-demo.zip) or [RocketMQ-Client-CPP Example](https://github.com/apache/rocketmq-client-cpp/tree/master/example).
