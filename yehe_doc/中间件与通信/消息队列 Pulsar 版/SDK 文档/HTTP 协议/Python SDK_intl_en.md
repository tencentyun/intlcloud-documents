## Overview

This document uses Python as an example to describe how to connect to TDMQ for Pulsar to send and receive messages over the HTTP protocol.

## Prerequisites

- [You have created the required resources](https://intl.cloud.tencent.com/document/product/1110/42915).
- [You have installed Python](https://www.python.org/downloads/)
- [You have installed pip](https://pip-cn.readthedocs.io/en/latest/installing.html)
- [You have downloaded the demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-python-http-demo.zip)

## Directions

1. Prepare the environment.
   Install the SDK for Python.
   <dx-codeblock>
   :::  shell
   pip install --upgrade tencentcloud-sdk-python
   :::
   </dx-codeblock>
2. Create the TDMQ client.
<dx-codeblock>
:::  python
   # Authentication information
   cred = credential.Credential(SECRET_ID, SECRET_KEY)
   httpProfile = HttpProfile()
   httpProfile.endpoint = ENDPOINT
   
   clientProfile = ClientProfile()
   clientProfile.httpProfile = httpProfile
   # Create the TDMQ client
   client = tdmq_client.TdmqClient(cred, REGION, clientProfile)
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
        <td style='text-align:left;'>TencentCloud API key, which can be copied on the <strong>Access Key</strong> &gt; <strong>API Key Management</strong> page in the <a href='https://console.cloud.tencent.com/cam'>CAM console</a>.
            <img
                    src="https://qcloudimg.tencent-cloud.cn/raw/3d48e4ec199df45055c09f1336d6e2b0.png"
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
:::  python
   # Message sending request parameters
   req = models.SendMessagesRequest()
   params = {
       # Authorized role key
       "StringToken": token,
       # Topic name in the following format: cluster (tenant) ID/namespace/topic name
       "Topic": topicName,
       # Message content
       "Payload": "this is a new message.",
       # Authorized role name
       "ProducerName": userName,
       # Sending timeout period
       "SendTimeout": 3000,
   }
   req.from_json_string(json.dumps(params))
   
   # Send a message
   resp = client.SendMessages(req)
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
                src="https://qcloudimg.tencent-cloud.cn/raw/37b49e64e428275de1fde778e114541b.png" referrerpolicy="no-referrer"
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
:::  python
   # Message receiving request parameters
   req = models.ReceiveMessageRequest()
   params = {
       # Topic name in the following format: cluster (tenant) ID/namespace/topic name
       "Topic": topicName,
       # Subscription name
       "SubscriptionName": subName,
       # Messages received by the consumer will first be stored in the `receiverQueueSize` queue to tune the message receiving rate
       "ReceiverQueueSize": 10,
       # It is used to determine the position where the consumer initially receives messages. Valid values: Earliest, Latest.
       "SubInitialPosition": "Latest"
   }
   req.from_json_string(json.dumps(params))
   
   # Receive messages
   resp = client.ReceiveMessage(req)
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
:::  python
   # Message acknowledging request parameters
   req = models.AcknowledgeMessageRequest()
   params = {
       # ID of the message to be acknowledged
       "MessageId": messageId,
       # Topic name in the following format: cluster (tenant) ID/namespace/topic name
       "AckTopic": topicName,
       # Subscription name
       "SubName": subName
   }
   req.from_json_string(json.dumps(params))
   
   # Acknowledge messages
   resp = client.AcknowledgeMessage(req)
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


>? Above is a brief introduction to message sending and receiving operations. For more information, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/http/tdmq-pulsar-python-http-demo.zip) or [API Explorer](https://console.cloud.tencent.com/api/explorer?Product=tdmq&Version=2020-02-17&Action=ModifyCluster&SignVersion=).

