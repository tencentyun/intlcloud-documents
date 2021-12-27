## Overview

This document describes how to download the demo, perform a simple test, and run a client after you create cluster, namespace, and other resources in the console.

## Prerequisites

- [Install JDK 1.8 or above](https://www.oracle.com/java/technologies/javase-downloads.html)
- [Install Maven 2.5 or later](http://maven.apache.org/download.cgi#)
- [Download the demo](https://tdmq-1300957330.cos.ap-guangzhou.myqcloud.com/TDMQ-demo/tdmq-rocketmq-demo.zip)

## Directions

### Step 1. Add dependencies

Add the following Java dependency library information to the `pom.xml` file:
```xml
<dependency>
    <groupId>org.apache.rocketmq</groupId>
    <artifactId>rocketmq-client</artifactId>
    <version>4.6.1</version>
</dependency>
```

### Step 2. Send a message

1. Create a message sending program ProducerWithNamespace.java and configure related parameters.
   ```java
   import org.apache.rocketmq.acl.common.AclClientRPCHook;
   import org.apache.rocketmq.acl.common.SessionCredentials;
   import org.apache.rocketmq.client.producer.DefaultMQProducer;
   import org.apache.rocketmq.client.producer.SendResult;
   import org.apache.rocketmq.common.message.Message;
   import org.apache.rocketmq.remoting.RPCHook;
   
   public class ProducerWithNamespace {
   
       // Configure the namespace token authenticated in the console as instructed in the documentation. Here, copy the token from **Role Management** and enter it
       // For directions, visit https://intl.cloud.tencent.com/document/product/1113/43126
       private static final String ACL_ACCESS_KEY = "eyJr****";
       // Enter the role name or "rop" (common role name) here
       private static final String ACL_SECRET_KEY = "rop";
       public static void main(String[] args) throws Exception {
   
           // `rocketmq-****|namespace` refers to the namespace name copied on the **Namespace** page in the console, and `producerGroup` refers to the producer group name copied on the **Group** page in the console
           DefaultMQProducer producer = new DefaultMQProducer("rocketmq-xxxx|namespace", "producerGroup", getAclRPCHook());
           // Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster Management** page in the console
           producer.setNamesrvAddr("rocketmq-xxxx.rocketmq.ap-sh.public.tencenttdmq.com:xxxx");
   
           producer.start();
           int total = 0;
           for (int i = 0; i<10; i++) {
               Message message = new Message("topic", "tags", ("Hello world——" + i).getBytes());
               // `topic` refers to the topic name copied on the **Topic** page in the console, and `tags` refers to message tags
               try {
                   SendResult result = producer.send(message);
                   total++;
                   System.out.printf("Topic:%s send success, queueId is: %s%n", message.getTopic(),
                           result.getMessageQueue().getQueueId());
                   Thread.sleep(1000);
               } catch (Exception e) {
                   e.printStackTrace();
               }
           }
           System.out.println("total ===> " + total);
           producer.shutdown();
       }
   
       static RPCHook getAclRPCHook() {
           return new AclClientRPCHook(new SessionCredentials(ACL_ACCESS_KEY, ACL_SECRET_KEY));
       }
   }
   ```
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>ACL_SECRET_KEY</td>
<td>Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td>ACL_ACCESS_KEY</td>
<td>Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png" alt=""></td>
</tr>
<tr>
<td>rocketmq-xxxx|namespace</td>
<td>Namespace name, which can be copied on the <strong>Namespace</strong> page in the console.</td>
</tr>
<tr>
<td>producerGroup</td>
<td>Producer group name, which can be copied on the <strong>Group</strong> page in the console.</td>
</tr>
<tr>
<td>setNamesrvAddr</td>
<td>Cluster access address, which can be obtained from <strong>Access Address</strong> in the **Operation** column on the <strong>Cluster Management</strong> page in the console.</td>
</tr>
<tr>
<td>topic</td>
<td>Topic name, which can be copied on the <strong>Topic</strong> page in the console.</td>
</tr>
<tr>
<td>tags</td>
<td>Tags for message filtering.</td>
</tr>
</tbody></table>
2. Compile and run the ProducerWithNamespace.java program.
3. View the execution result. The result of successful execution is as follows.
```
Topic:topic1 send success, queueId is: 0
Topic:topic1 send success, queueId is: 0
Topic:topic1 send success, queueId is: 1
Topic:topic1 send success, queueId is: 2
Topic:topic1 send success, queueId is: 0
Topic:topic1 send success, queueId is: 1
```



### Step 3. Consume the message

1. Create a message sending program PushConsumerWithNamespace.java and configure related parameters.
   ```java
   import org.apache.rocketmq.acl.common.AclClientRPCHook;
   import org.apache.rocketmq.acl.common.SessionCredentials;
   import org.apache.rocketmq.client.consumer.DefaultMQPushConsumer;
   import org.apache.rocketmq.client.consumer.listener.ConsumeConcurrentlyStatus;
   import org.apache.rocketmq.client.consumer.listener.MessageListenerConcurrently;
   import org.apache.rocketmq.common.consumer.ConsumeFromWhere;
   import org.apache.rocketmq.remoting.RPCHook;
   
   import java.util.concurrent.atomic.AtomicLong;
   
   public class PushConsumerWithNamespace {
   
       // Configure the namespace token authenticated in the console as instructed in the documentation. Here, copy the token from **Role Management** and enter it
       // For directions, visit https://intl.cloud.tencent.com/document/product/1113/43126
       private static final String ACL_ACCESS_KEY = "eyJr****";
       // Enter the role name or "rop" (common role name) here
       private static final String ACL_SECRET_KEY = "rop";
   
       public static void main(String[] args) throws Exception {
           // `rocketmq-xxxx|namespace` refers to the namespace name copied on the **Namespace** page in the console, and `consumerGroup` refers to the consumer group name copied on the **Group** page in the console
           DefaultMQPushConsumer defaultMQPushConsumer = new DefaultMQPushConsumer("rocketmq-xxxx|namespace", "consumerGroup", getAclRPCHook());
           // Cluster access address, which can be obtained from **Access Address** in the **Operation** column on the **Cluster Management** page in the console
           defaultMQPushConsumer.setNamesrvAddr("rocketmq-xxxx.rocketmq.ap-sh.public.tencenttdmq.com:xxxx");
           // `topic` refers to the topic name copied on the **Topic** page in the console
           defaultMQPushConsumer.subscribe("topic", "*");
   
           defaultMQPushConsumer.setConsumeFromWhere(ConsumeFromWhere.CONSUME_FROM_FIRST_OFFSET);
   
           AtomicLong curTime = new AtomicLong(System.currentTimeMillis());
           AtomicLong count = new AtomicLong(0L);
           defaultMQPushConsumer.registerMessageListener((MessageListenerConcurrently)(msgs, context) -> {
               msgs.forEach((msg) -> {
                   System.out.println(" body=" + new String(msg.getBody()));
                   curTime.set(System.currentTimeMillis());
                   count.incrementAndGet();
                   System.out.println("total ====> " + count.get());
               });
               return ConsumeConcurrentlyStatus.CONSUME_SUCCESS;
           });
           defaultMQPushConsumer.start();
       }
   
       static RPCHook getAclRPCHook() {
           return new AclClientRPCHook(new SessionCredentials(ACL_ACCESS_KEY, ACL_SECRET_KEY));
       }
   }
   ```
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>ACL_SECRET_KEY</td>
<td>Role name, which can be copied on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page.</td>
</tr>
<tr>
<td>ACL_ACCESS_KEY</td>
<td>Role token, which can be copied in the <strong>Token</strong> column on the <strong><a href="https://console.cloud.tencent.com/tdmq/role">Role Management</a></strong> page. <img src="https://main.qcloudimg.com/raw/52907691231cc11e6e4801298ba90a6c.png" alt=""></td>
</tr>
<tr>
<td>rocketmq-xxxx|namespace</td>
<td>Namespace name, which can be copied on the <strong>Namespace</strong> page in the console.</td>
</tr>
<tr>
<td>consumerGroup</td>
<td>Consumer group name, which can be copied on the <strong>Group</strong> page in the console.</td>
</tr>
<tr>
<td>setNamesrvAddr</td>
<td>Cluster access address, which can be obtained from <strong>Access Address</strong> in the **Operation** column on the <strong>Cluster Management</strong> page in the console.</td>
</tr>
<tr>
<td>topic</td>
<td>Topic name, which can be copied on the <strong>Topic</strong> page in the console.</td>
</tr>
</tbody></table>
2. Compile and run the PushConsumerWithNamespace.java program.
3. View the execution result. The result of successful execution is as follows.
   ```bash
    body=Hello world——4
   total ====> 1
    body=Hello world——6
   total ====> 2
    body=Hello world——7
    body=Hello world——11
    body=Hello world——8
   ```
4. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq), go to the **Cluster Management** > **Group** page, and view the list of clients connected to the group. Click **View Details** in the **Operation** column to view consumer details.
	 ![](https://main.qcloudimg.com/raw/7187da67219534d767206553e2a383ab.png)
