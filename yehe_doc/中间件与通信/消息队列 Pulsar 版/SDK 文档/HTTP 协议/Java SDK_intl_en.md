## Overview

This document uses Java as an example to describe how to connect to TDMQ for Pulsar to send and receive messages over the HTTP protocol.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed JDK 1.8 or later.](https://www.oracle.com/java/technologies/javase-downloads.html)
- [You have installed Maven 2.5 or later.](http://maven.apache.org/download.cgi#)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-java-http-demo.zip)

## Directions

1. Add SDK for Java dependencies first.
<dx-codeblock>
:::  xml
   <dependency>
       <groupId>com.tencentcloudapi</groupId>
       <artifactId>tencentcloud-sdk-java-tdmq</artifactId>
       <!-- go to https://search.maven.org/search?q=tencentcloud-sdk-java and get the latest version. -->
       <!-- Query the latest version at https://search.maven.org/search?q=tencentcloud-sdk-java, which is as follows -->
       <version>3.1.423</version>
   </dependency>
:::
</dx-codeblock>
2. Create the TDMQ client.
<dx-codeblock>
:::  java
   // Instantiate an authentication object. Pass in secretID and secretKey of your Tencent Cloud account as the input parameters and keep them confidential.
   // You can get them at https://console.cloud.tencent.com/cam/capi
   Credential cred = new Credential(secretId, secretKey);
   // (Optional) Instantiate an HTTP option
   HttpProfile httpProfile = new HttpProfile();
   httpProfile.setEndpoint(endpoint);
   // (Optional) Instantiate a client option
   ClientProfile clientProfile = new ClientProfile();
   clientProfile.setHttpProfile(httpProfile);
   // Instantiate the client object of the requested product. `clientProfile` is optional
   TdmqClient client = new TdmqClient(cred, region, clientProfile);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>secretId、secretKey</td>
        <td style='text-align:left;'>TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.cloud.tencent.com/cam'>CAM console</a>.
            <img
                    src="https://qcloudimg.tencent-cloud.cn/raw/4b469f96a2a45a5642fa0087ef07e002.png"
                    referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>endpoint</td>
        <td style='text-align:left;'>API request domain: tdmq.tencentcloudapi.com.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>region</td>
        <td style='text-align:left;'>Cluster region. For more regions, see <a href='https://cloud.tencent.com/document/api/1179/46067#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8'>Region List</a>.
        </td>
    </tr>
    </tbody>
</table>
3. Send messages.
<dx-codeblock>
:::  java
   // Instantiate a request object. Each API corresponds to a request object
   SendMessagesRequest req = new SendMessagesRequest();
   // Set the authorized role key
   req.setStringToken(token);
   // Set the authorized role name
   req.setProducerName(userName);
   // Set the topic name in the following format: cluster (tenant) ID/namespace/topic name
   req.setTopic(topicName);
   // Message content
   req.setPayload("this is a new message.");
   // Set the sending timeout period
   req.setSendTimeout(3000L);
   // The returned `resp` is an instance of `SendMessagesResponse` which corresponds to the request object
   SendMessagesResponse resp = client.SendMessages(req);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>token</td>
        <td style='text-align:left;'>Role key, which can be copied in the <strong>Key</strong> column on the <strong><a href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.
                <img
                src="https://qcloudimg.tencent-cloud.cn/raw/12c36d5b811e9aeb80ca43d22dffd385.png" referrerpolicy="no-referrer"
                alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>userName</td>
        <td style='text-align:left;'>Role name, which can be copied in the <strong>Name</strong> column on the <strong><a href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.
        </td>
    </tr>
    <tr>
        <td style='text-align:left;'>topicName</td>
        <td style='text-align:left;'>Topic name in the following format: cluster (tenant) ID/namespace/topic name, such as `pulsar-xxx/sdk_http/topic1`. You can directly copy it on the <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic Management</a></strong> page in the console.
        </td>
    </tr>
    </tbody>
</table>
4. Consume messages.
<dx-codeblock>
:::  java
   // Instantiate a request object. Each API corresponds to a request object
   ReceiveMessageRequest req = new ReceiveMessageRequest();
   // Set the topic name in the following format: persistent://cluster (tenant) ID/namespace/topic name
   req.setTopic(topicName);
   // Set the subscription name
   req.setSubscriptionName(subName);
   // Messages received by the consumer will first be stored in the `receiverQueueSize` queue to tune the message receiving rate
   req.setReceiverQueueSize(10L);
   // It is used to determine the position where the consumer initially receives messages. Valid values: Earliest, Latest.
   req.setSubInitialPosition("Latest");
   // The returned `resp` is an instance of `ReceiveMessageResponse` which corresponds to the request object
   ReceiveMessageResponse resp = client.ReceiveMessage(req);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>topicName</td>
        <td style='text-align:left;'>Topic name in the following format: cluster (tenant) ID/namespace/topic name, such as `pulsar-xxx/sdk_http/topic1`. You can directly copy it on the <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic Management</a></strong> page in the console.
        </td>
    </tr>
    <tr>
        <td style='text-align:left;'>subName</td>
        <td style='text-align:left;'>Subscription name, which can be copied on the <strong>Cluster</strong> &gt; <strong>Consumer</strong> tab in the console.</td>
    </tr>
    </tbody>
</table>
5. Acknowledge messages.
<dx-codeblock>
:::  java
   // Instantiate a request object. Each API corresponds to a request object
   AcknowledgeMessageRequest req = new AcknowledgeMessageRequest();
   // Set the message ID
   req.setMessageId(messageId);
   // Set the topic name in the following format: persistent://cluster (tenant) ID/namespace/topic name
   req.setAckTopic(topicName);
   // Set the subscription name
   req.setSubName(subName);
   // The returned `resp` is an instance of `AcknowledgeMessageResponse` which corresponds to the request object
   AcknowledgeMessageResponse resp = client.AcknowledgeMessage(req);
:::
</dx-codeblock>
<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>messageId</td>
        <td style='text-align:left;'>Message ID obtained after message consumption.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>topicName</td>
        <td style='text-align:left;'>Topic name in the following format: cluster (tenant) ID/namespace/topic name, such as `pulsar-xxx/sdk_http/topic1`. You can directly copy it on the <strong><a href='https://console.cloud.tencent.com/tdmq/topic'>Topic Management</a></strong> page in the console.
        </td>
    </tr>
    <tr>
        <td style='text-align:left;'>subName</td>
        <td style='text-align:left;'>Subscription name, which can be copied on the <strong>Cluster</strong> &gt; <strong>Consumer</strong> tab in the console.</td>
    </tr>
    </tbody>
</table>

>? Above is a brief introduction to message sending and receiving operations. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-java-http-demo.zip) or [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=tdmq&Version=2020-02-17&Action=ModifyCluster&SignVersion=).
