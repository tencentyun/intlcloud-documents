## Overview

This document uses C++ as an example to describe how to connect to TDMQ for Pulsar to send and receive messages over the HTTP protocol.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed GCC](https://gcc.gnu.org/install/)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-cpp-http-demo.zip)



## Directions

1. Prepare the environment.
 1. Configure dependencies and compile the code for installation as instructed in SDK for C++ Compilation and Installation.
 2. Import relevant header files and dependency libraries to the project.
2. Create the TDMQ client.
<dx-codeblock>
:::  c++
   // Authentication information
   Credential cred = Credential(SECRET_ID, SECRET_KEY);
   
   HttpProfile httpProfile = HttpProfile();
   httpProfile.SetEndpoint(ENDPOINT);
   
   ClientProfile clientProfile = ClientProfile();
   clientProfile.SetHttpProfile(httpProfile);
   // Create the TDMQ client
   TdmqClient client = TdmqClient(cred, REGION, clientProfile);
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
        <td style='text-align:left;'>SECRET_ID、SECRET_KEY</td>
        <td style='text-align:left;'><img src="https://qcloudimg.tencent-cloud.cn/raw/ec875f8da34679a80bd512ac327813a9.png"
                                          referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>ENDPOINT</td>
        <td style='text-align:left;'>API request domain: tdmq.tencentcloudapi.com.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>REGION</td>
        <td style='text-align:left;'>Cluster region. For more regions, see <a href='https://cloud.tencent.com/document/api/1179/46067#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8'>Region List</a>.
        </td>
    </tr>
    </tbody>
</table>
3. Send messages.
<dx-codeblock>
:::  c++
   SendMessagesRequest req = SendMessagesRequest();
   // Set the authorized role key
   req.SetStringToken(token);
   // Set the authorized role name
   req.SetProducerName(userName);
   // Set the topic name in the following format: cluster (tenant) ID/namespace/topic name
   req.SetTopic(topicName);
   // Message content
   req.SetPayload("this is a new message.");
   // Set the message sending timeout period
   req.SetSendTimeout(3000);
   // Send the message
   auto outcome = client.SendMessages(req);
   if (!outcome.IsSuccess()) {
       cout << outcome.GetError().PrintAll() << endl;
       return -1;
   }
   // Get the result
   SendMessagesResponse resp = outcome.GetResult();
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
                src="https://qcloudimg.tencent-cloud.cn/raw/d94994d333555d12304f4737f89d47cd.png" referrerpolicy="no-referrer"
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
:::  c++
   ReceiveMessageRequest req = ReceiveMessageRequest();
   // Set the topic name in the following format: cluster (tenant) ID/namespace/topic name
   req.SetTopic(topicName);
   // Set the subscription name
   req.SetSubscriptionName(subName);
   // Messages received by the consumer will first be stored in the `receiverQueueSize` queue to tune the message receiving rate
   req.SetReceiverQueueSize(10);
   // It is used to determine the position where the consumer initially receives messages. Valid values: Earliest, Latest.
   req.SetSubInitialPosition("Latest");
   
   // Receive messages
   auto outcome = client.ReceiveMessage(req);
   if (!outcome.IsSuccess()) {
       cout << outcome.GetError().PrintAll() << endl;
       return -1;
   }
   // Get the result
   ReceiveMessageResponse resp = outcome.GetResult();
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
:::  c++
   AcknowledgeMessageRequest req = AcknowledgeMessageRequest();
   // Acknowledge the message ID
   req.SetMessageId(messageId);
   // Set the topic name in the following format: cluster (tenant) ID/namespace/topic name
   req.SetAckTopic(topicName);
   // Set the message subscription
   req.SetSubName(subName);
   // Acknowledge messages
   auto outcome = client.AcknowledgeMessage(req);
   if (!outcome.IsSuccess()) {
       cout << outcome.GetError().PrintAll() << endl;
       return -1;
   }
   // Get the result
   AcknowledgeMessageResponse resp = outcome.GetResult();
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


>? Above is a brief introduction to message sending and receiving operations. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-cpp-http-demo.zip) or [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=tdmq&Version=2020-02-17&Action=ModifyCluster&SignVersion=).

